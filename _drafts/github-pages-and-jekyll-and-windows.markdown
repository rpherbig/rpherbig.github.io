---
title: GitHub Pages and Jekyll and Windows, Oh My!
layout: post
---

You may have heard of a small company based out of Albuquerque, Micro-Soft. If you haven't, don't feel bad. They're a pretty small player in the market (just buy some stock now, I hear they're going to have a huge IPO in '86).

It's important to note that Jekyll doesn't officially support Windows. But they have endorsed a guide by [@juthilo](https://twitter.com/juthilo) that "seems to work for most": http://jekyll-windows.juthilo.com/.

Don't get excited yet, because if you followed my advice and use GitHub Pages, that link is just a red herring, much like Communism ([according to Wadsworth](http://www.imdb.com/title/tt0088930/quotes)).

== Something

TODO: PUT THE OTHER STEPS IN HERE

Instead of running "gem install jekyll", run "gem install bundler".

Then create a file in your repo named Gemfile. Put the following in it:
{% highlight ruby %}
source 'https://rubygems.org'
gem 'github-pages'
gem 'wdm', '>= 0.1.0' if Gem.win_platform?
{% endhighlight %}

Then run "bundle install". This will ensure that we are using the same version of everything as GitHub.

TODO: PUT THE OTHER STEPS IN HERE
- NOTE PYGMENTS IS THE ONLY OPTION FOR GITHUB PAGES

TODO: See what a "jekyll new" _config.yml has, and compare to my current version

== Start using Jekyll

Markdown
http://daringfireball.net/projects/markdown/syntax

http://jekyllrb.com/docs/quickstart/

http://jekyllrb.com/docs/structure/

http://mike-rogers.github.io/2013/11/23/jekyll-and-pdus-for-fun-and-profit/

https://arktronic.com/weblog/2014-08-09/new-blog-and-new-tea/

https://help.github.com/articles/using-jekyll-with-pages/

== Known issues

TODO: Rewrite this section - it's still worth mentioning
Note: if you run Jekyll and your highlighter is rouge, you may get an error that looks like this:
Configuration file: c:/Users/rpherbig/Documents/GitHub/rpherbig.github.io/_confi
g.yml
            Source: c:/Users/rpherbig/Documents/GitHub/rpherbig.github.io
       Destination: c:/Users/rpherbig/Documents/GitHub/rpherbig.github.io/_site
      Generating...
  Liquid Exception: cannot load such file -- rouge in _posts/2014-11-14-welcome-
to-jekyll.markdown
c:/Ruby21-x64/lib/ruby/2.1.0/rubygems/core_ext/kernel_require.rb:55:in `require'
: cannot load such file -- rouge (LoadError)

What this says is that it cannot find the rouge gem.

What it means is that the a gem you installed (in this case, rouge) was pre-compiled and not ruby-2.0 compatible. The fix is to instead install the rouge gem via "gem install rouge --platform=ruby", which will force recompilation. See https://github.com/brianmario/yajl-ruby/issues/116 for more details.

== Ruby and JRuby

First, a note on gem.exe. If you have jruby installed, running gem at a command prompt may very well use jruby's gem.exe rather than ruby's (due to the quirks of the PATH environment variable). This generally doesn't cause a problem, but you may see an error that looks like this:
        ERROR: Failed to build gem native extension.

    C:/jruby/bin/jruby.exe extconf.rb
NotImplementedError: C extension support is not enabled. Pass -Xcext.enabled=true to JRuby or set JRUBY_OPTS.

This occurs because jruby's gem.exe does not support native C extensions. The fix is to install the gem via "/c/path/to/ruby/installation/bin/gem install gemname".

Now that we have that out of the way, onward!



http://jekyllthemes.org/



Don't commit to any particular topic as the next post.
