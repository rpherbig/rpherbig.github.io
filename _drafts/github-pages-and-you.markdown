---
title: GitHub Pages and You
layout: post
---

Blogging should be about the writing, not the mechanism for displaying text. For this grand experiment, the first step is just to get some text served up in the easiest way possible (agile blog design, if you will).

Let's avoid as much work as possible: no custom domain, no hosting, no databse, no theming. How could we possible get away with that? Hint: it's in this post's title.

----------

What is GitHub Pages? If you create a repo with a specific name (username.github.io), the content will be automatically served up at http://username.github.io. It's the kind of URL you don't take home to mother, but it'll work (remember, the emphasis is on the writing). And with GitHub taking care of all the hosting headaches, it's worth it.

GitHub's [own site](https://pages.github.com/) does a good job of explaining it in detail. By the end of their instructions, you will have an externally accessible site and a static index.html page. Pushing to the repo's master branch will automatically update the served content.

Now what? Where to go from here? The end of the GitHub Pages tutorial offers some suggestions: use Jekyll to start a blog, set up a custom URL, or set up some more advanced features like a custom 404.

Since we're going for simplicity, let's start with turning that static index.html into something a bit more useful. Jekyll is a static website generator that was recommended to me, and in turn I recommend it to you.

GitHub Pages and Jekyll were designed to work together. It's [smooth sailing ahead](https://help.github.com/articles/using-jekyll-with-pages/) as long as you aren't using Windows. If you are, batten down the hatches and hang on. I'll try and steer us around any icebergs in my next post.