Start a blog, they said.

Write a blog post, they said.

I'd rather be sailing. http://rpgcodex.net/phpBB/images/avatars/gallery/Warcraft%202/footman.png

It's 2014. How hard can it be to get some text to appear on a web page? Harder than I expected, but only because I'm using Windows.

== Ruby and JRuby

First, a note on gem.exe. If you have jruby installed, running gem at a command prompt may very well use jruby's gem.exe rather than ruby's (due to the quirks of the PATH environment variable). This generally doesn't cause a problem, but you may see an error that looks like this:
        ERROR: Failed to build gem native extension.

    C:/jruby/bin/jruby.exe extconf.rb
NotImplementedError: C extension support is not enabled. Pass -Xcext.enabled=true to JRuby or set JRUBY_OPTS.

This occurs because jruby's gem.exe does not support native C extensions. The fix is to install the gem via "/c/path/to/ruby/installation/bin/gem install gemname".

Now that we have that out of the way, onward!

== Install Jekyll

GitHub Pages and Jekyll? That's easy, GitHub will walk you through it: https://help.github.com/articles/using-jekyll-with-pages/

Jekyll and Windows? Not as easy, since Jekyll doesn't officially support Windows. But Jekyll has endorsed a guide by @juthilo that "seems to work for most": http://jekyll-windows.juthilo.com/

Now we get to the fun part: GitHub Pages and Jekyll and Windows. That's just crazy talk. Luckily I'm crazy enough to keep trying until it works.

TODO: PUT THE OTHER STEPS IN HERE

Instead of running "gem install jekyll", run "gem install bundler".

Then create a file in your repo named Gemfile. Put the following in it:
source 'https://rubygems.org'
gem 'github-pages'
gem 'wdm', '>= 0.1.0' if Gem.win_platform?

Then run "bundle install". This will ensure that we are using the same version of everything as GitHub.

TODO: PUT THE OTHER STEPS IN HERE
- NOTE PYGMENTS IS THE ONLY OPTION FOR GITHUB PAGES

TODO: See what a "jekyll new" _config.yml has, and compare to my current version

== Start using Jekyll

http://jekyllrb.com/docs/quickstart/

TODO: Generalize this section - it's still worth mentioning
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