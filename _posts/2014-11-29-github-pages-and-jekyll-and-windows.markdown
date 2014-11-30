---
title: GitHub Pages and Jekyll and Windows, Oh My!
layout: post
---

You may have heard of a small company based out of Albuquerque: Micro-Soft. Don't feel bad if you haven't, they're a pretty small company (but keep an eye on them, I hear they're going to have a huge IPO in '86). Because they're such a small player in the market, Jekyll doesn't officially support their operating system. However, Jekyll has endorsed a guide by [@juthilo](https://twitter.com/juthilo) that "[seems to work for most](http://jekyll-windows.juthilo.com/)".

Don't get too excited though, because if you followed my advice and used GitHub Pages, that link is just a red herring (much like Communism, [according to Wadsworth](http://www.imdb.com/title/tt0088930/quotes)). What follows is cherry-picking parts of several guides to get it all working.

## The Setup

The zeroth thing you'll need to do is [setup your GitHub Pages repository]({% post_url 2014-11-23-github-pages-and-you %}) and clone it locally (left as an exercise to the reader).

The first thing you'll need to do is install Ruby. Follow the instructions on only [page one](http://jekyll-windows.juthilo.com/1-ruby-and-devkit/) of juthilo's guide, then return here.

Second, we're going to install Jekyll, but we're going to do so in a way that is compatible with Pages. Create a file in your repo named `Gemfile` and put the following in it:
{% highlight ruby %}
source 'https://rubygems.org'
gem 'github-pages'
gem 'wdm', '>= 0.1.0' if Gem.win_platform?
{% endhighlight %}

Now open a command prompt (I suggest GitBash), navigate to your repo, and run `gem install bundler`, then `bundle install`. This will take a little while, but it ensures that we are only using gems allowed by Pages (one of which is Jekyll itself) and the appropriate versions thereof. GitHub is very restrictive as to what gems you can use with Pages, and rightfully so since the code will be running on their servers.

Now run `jekyll new .` to create your site with a bunch of defaults. You can now build your site locally before publishing by running `jekyll serve` and opening `http://localhost:4000` in a browser. By using `serve`, changes to files will be updated immediately - just refresh the page. You can push a changeset to GitHub when you are happy with the result and it will be published to your site.

Technically, you can stop now. You have the tools to manage your blog. However, if you want to use syntax highlighting there's one more hoop to jump through. Otherwise you can skip the next section.

## Syntax Highlighting

[Page three](http://jekyll-windows.juthilo.com/3-syntax-highlighting/) of juthilo's guide has a nice comparison of two popular syntax highlighters (Pygments and Rouge). However, Pages does not support Rouge, so the decision is made for us.

Go ahead and follow the instructions on only [page three](http://jekyll-windows.juthilo.com/3-syntax-highlighting/) of juthilo's guide, choosing Pygments and skipping Rouge.

If you accidentally set your highlighter to Rouge, you'll get an email from GitHub saying that deployment of your site failed, but with an empty error message (needless to say, it took me a while to figure that one out).

## Start using Jekyll

Here are some of the more interesting files/directories in your repo right now:

* `_posts/` contains your posts. By default it has one named `Welcome to Jekyll` that you may or may not want to keep.

* `_site/` contains the static HTML for your site, if you built it locally by running `jekyll build`.

* `.gitignore` specifies files that Git should ignore. You should add `_site` to it.

* `_config.yml` stores, you guessed it, configuration. You should update the placeholders with something more useful.

* `about.md` is your "About" page. You should update it with something more useful.

* `README.md` was created when you made the repo on GitHub, and has nothing to do with Jekyll. It is only visible when someone browses GitHub, not your site. Nonetheless, you should update it.

* More information can be found on the [official Jekyll site](http://jekyllrb.com/docs/structure/).

To publish a new post, simply create a files in `_posts/`. Files in this directory must be named `YEAR-MONTH-DAY-title.extension`, where extension is either of the two supported formats ([.markdown](http://daringfireball.net/projects/markdown/) or [.textile](http://redcloth.org/textile)). More information can be found on the [official Jekyll site](http://jekyllrb.com/docs/posts/).

## Drafts

If you're like me and have multiple machines, you may be interested in the "drafts" functionality offered by Jekyll (drafts are simply unpublished posts).

Create a `_drafts/` directory and commit your works-in-progress to it. These files will not be shown on your site, but you can now leverage the power of git while you work on your future posts.

You can preview your drafts locally by adding the `--drafts` switch when you build or serve Jekyll. Drafts will then show up as if they were published posts. This switch is local only - it does not affect how your site will deploy to Pages.

To publish a draft, simply run `git mv _drafts/title.extension _posts/YEAR-MONTH-DAY-title.extension` and commit/push. Adding the date to the file's new name is mandatory.

## What's Next?

This was the easy part. Now you need to fill your blog with content!

But as for your site, there's a lot you can do. One of my coworkers started tracking his [professional development projects](http://mike-rogers.github.io/pages/pdu.html). Another wrote a [neat Jekyll theme](http://jekyllthemes.org/themes/lagom/).

As for me, I'm not sure what I'll do next. Off the top of my head, I want to look into a few things: custom domains, analytics, and RSS vs Atom. But I make no promises as to where the Muses take me next. If you have a suggestion or request, feel free to drop me a line (check the footer for my contact info).
