---
title: Refactoring: a play in three parts
layout: post
---

# Act 1, the setup

Once upon a time, there was a JavaScript codebase. This codebase used the *function expression* syntax:

```javascript
const functionName = () => 1;
```

In this example, `functionName` is a function that returns the integer 1.

For [various](http://stackoverflow.com/questions/33040703/proper-use-of-const-for-defining-functions-in-javascript) and [sundry](https://medium.freecodecamp.com/constant-confusion-why-i-still-use-javascript-function-statements-984ece0b72fd) reasons, I needed to replace this with the *function declaration* syntax:

```javascript
function functionName() {
  return 1;
}
```

# Act 2, the confrontation

Usually some clever find-and-replace (read: regular expressions), mixed with a bit of manual labor, would take care of this quickly enough. I started down that path with a few minutes of tinkering.

> Some people, when confronted with a problem, think “I know, I'll use regular expressions.”  Now they have two problems.
> [Jamie Zawinski](http://regex.info/blog/2006-09-15/247)

I realized I needed to find a better way:
* The codebase contained different forms of *function expressions*, which meant I would need to write several different regular expressions.
* This same transform would be needed later for a different codebase, so I needed something repeatable.
* There was also a good chance that someone else would be doing this next time, so I needed something others could understand easily.

# Act 3, the resolution

Enter [JSCodeShift](https://github.com/facebook/jscodeshift), stage left. JSCodeShift turns JavaScript files into an [abstract-syntax tree](https://en.wikipedia.org/wiki/Abstract_syntax_tree) (AST). We will then need to write a *codemod* which will find and replace nodes in the AST. At a high level, our *codemod* will look something like this:

```javascript
module.exports = (file, api) {
  const j = api.codeshift;
  const root = j(file.source);

  function replaceNode(nodePath) {
    ...
  }

  return root.find(...)
             .replaceWith(replaceNode)
             .toSource();
}
```

Step one is to determine what we need to match in the AST. Using the wonderful [AST Explorer](http://astexplorer.net/), we can see the AST for a *function expression*:

```json
{
  "type": "Program",
  "body": [
    {
      "type": "VariableDeclaration",
      "declarations": [
        {
          "type": "VariableDeclarator",
          "id": {
            "type": "Identifier",
            "name": "functionName"
          },
          "init": {
            "type": "ArrowFunctionExpression",
            "expression": true,
            "params": [],
            "body": {
              "type": "Literal",
              "value": 1
            }
          }
        }
      ],
      "kind": "const"
    }
  ]
}
```

Now we know we need to find a *VariableDeclaration* node which contains an *ArrowFunctionExpression* node:

```javascript
return root.find(j.VariableDeclaration, {
              declarations: [{
                init: {
                  type: 'ArrowFunctionExpression'
                }
              }]
            })
           .replaceWith(...)
           .toSource();
```

Step two is to determine what our replacement node needs to look like. As before, we can see the AST for a *function declaration*:

```json
{
  "type": "Program",
  "body": [
    {
      "type": "FunctionDeclaration",
      "id": {
        "type": "Identifier",
        "name": "functionName"
      },
      "params": [],
      "body": {
        "type": "BlockStatement",
        "body": [
          {
            "type": "ReturnStatement",
            "argument": {
              "type": "Literal",
              "value": 1
            }
          }
        ]
      }
    }
  ]
}
```

Now we know we need to output a *FunctionDeclaration* node. We do not want to create one manually, instead using the *builder* that JSCodeShift provides: `j.functionDeclaration(...)`. According to the [FunctionDeclaration definition](https://github.com/benjamn/ast-types/blob/master/def/core.js#L174-L177), we will need to provide `id`, `params`, and `body`. We can get those from the *VariableDeclaration* and *ArrowFunctionExpression* nodes we found above.

```javascript
function replaceNode(nodePath) {
  const { node } = nodePath;
  const variableDeclarator = node.declarations[0];
  const arrowFunctionExpression = variableDeclarator.init;

  return j.functionDeclaration(
            variableDeclarator.id,
            arrowFunctionExpression.params,
            arrowFunctionExpression.body);
}

return root.find(...)
           .replaceWith(replaceNode)
           .toSource();
```

# Conclusion

JSCodeShift makes difficult or complicated code transforms much easier. The resulting code is far more readable than a regex.

However, it can take a little while to write a *codemod*, so a find/replace can still be faster in simple cases. There are also some cases in which small text changes result in significant changes to the AST, for example:

```javascript
const helper = require('helper');

const helper = require('helper').foo;
```

JSCodeShift is a powerful new tool in our toolbox, though not one we'll use every day.
