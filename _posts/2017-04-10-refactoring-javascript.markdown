---
title: Refactoring JavaScript - a play in three acts
layout: post
---

# Act 1, the setup

Once upon a time, there was a JavaScript codebase. This codebase used the *function expression* syntax:

```javascript
const returnTheNumberOne = () => 1;
```

For reasons that aren't relevant to this blog post, I needed to replace this with the *function declaration* syntax:

```javascript
function returnTheNumberOne()
{
  return 1;
}
```

# Act 2, the confrontation

Usually some clever find-and-replace (read: regular expressions), mixed with a bit of manual labor, would take care of this quickly enough. I started down that path with a few minutes of tinkering.

> Some people, when confronted with a problem, think “I know, I'll use regular expressions.”  Now they have two problems.
> [Jamie Zawinski](http://regex.info/blog/2006-09-15/247)

It didn't take me long to realize I needed to find a better way:
* The codebase had different types of *function expressions*, which meant I would need to write several different regular expressions.
* This same transform would be used later on a different codebase, so I wanted something flexible and repeatable.
* There was also a good chance that someone else would be doing this next time, so I wanted something others could understand easily.

# Act 3, the resolution

Enter [JSCodeShift](https://github.com/facebook/jscodeshift), stage left. JSCodeShift turns JavaScript files into an [abstract-syntax tree](https://en.wikipedia.org/wiki/Abstract_syntax_tree) (AST). This provides an object model that can be used to do more complicated transforms than could be done on context-less text.

The wonderful [AST Explorer](http://astexplorer.net/) will show what the AST looks like for both our input and target. I've marked up the ASTs from the two code snippets above to show how they are related. This should help explain what needs to be transformed and how.

![](/images/AST_to_code_mapping.png)

A codemod is JavaScript code which will operate on the nodes in the AST. Typically, it will find nodes that match some pattern and replace them with something else. At a high level, it could look something like this:

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

Using the AST for the input code, the target is any *VariableDeclaration* node which contains an *ArrowFunctionExpression* node.

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

According to the AST for the target code, what we found will be replaced with a *FunctionDeclaration* node. If we created this node by hand, we would have to manage a lot of AST-related details: line numbers, object references, parent relationships, etc. Luckily JSCodeShift provides builder functions such as `j.functionDeclaration(...)` to do that for us. According to the [FunctionDeclaration definition](https://github.com/benjamn/ast-types/blob/master/def/core.js#L174-L177), that node is built with `id`, `params`, and `body`. We can get those from the *VariableDeclaration* and *ArrowFunctionExpression* nodes we found above.

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

It can take a little while to write a codemod, so a find/replace can still be faster in simple cases. There are also some cases in which small text changes result in significant changes to the AST that would require writing a second codemod. Analyzing the AST from this snippet is left as an exercise to the reader:

```javascript
const helper = require('helper');

const helper = require('helper').foo;
```

Also, the way code comments are handled surprised me: they are properties of the closest node in the AST. That means they must be copied manually if you are changing that node.

JSCodeShift makes difficult or complicated code transforms much easier. The resulting code is far more readable than a regex. And when best practices change in the future, the codemod is easy to revisit, understand, and update for the new standard. The neverending march of progress just got easier.

JSCodeShift is a powerful new tool in our toolbox, though not one we'll use every day.

-----

Links used in this post:
* [Wikipedia page for abstract-syntax tree](https://en.wikipedia.org/wiki/Abstract_syntax_tree) (AST)
* [JSCodeShift on GitHub](https://github.com/facebook/jscodeshift)
* [AST Explorer](http://astexplorer.net/)
* [AST type definitions](https://github.com/benjamn/ast-types/tree/master/def)
