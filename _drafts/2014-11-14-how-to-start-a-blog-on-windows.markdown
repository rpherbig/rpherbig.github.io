Start a blog, they said.

Write a blog post, they said.

I'd rather be sailing. http://rpgcodex.net/phpBB/images/avatars/gallery/Warcraft%202/footman.png

It's 2014. How hard can it be to get some text to appear on a web page? Harder than I expected, but only becuause I'm using Windows.

== Ruby and JRuby

First, a note on gem.exe. If you have jruby installed, running gem at a command prompt may very well use jruby's gem.exe rather than ruby's (due to the quirks of the PATH environment variable). This generally doesn't cause a problem, but you may see an error that looks like this:
        ERROR: Failed to build gem native extension.

    C:/jruby/bin/jruby.exe extconf.rb
NotImplementedError: C extension support is not enabled. Pass -Xcext.enabled=tru
e to JRuby or set JRUBY_OPTS.

This occurs because jruby's gem.exe does not support native C extensions. The fix is to install the gem via "/c/path/to/ruby/installation/bin/gem install <gemname>".

Now that we have that out of the way, onward!

== Install Jekyll

We will be roughly following the instructions at http://jekyll-windows.juthilo.com/, but with some a few changes.

I've had success with ruby 2.1.4, jekyll 2.4.0, wdm 0.1.0, and rouge 1.7.2. I recommend using rouge over pygments for now, mainly to reduce the setup complexity. You can always switch to pygments later.


== Start using Jekyll

http://jekyllrb.com/docs/quickstart/

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