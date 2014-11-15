Start a blog, they said.

Write a blog post, they said.

I'd rather be sailing. http://rpgcodex.net/phpBB/images/avatars/gallery/Warcraft%202/footman.png

It's 2014. How hard can it be to get some text to appear on a web page? Harder than I expected, but only becuause I'm using Windows.

== Install Jekyll

Follow the instructions at http://jekyll-windows.juthilo.com/

I had success with ruby 2.1.4, jekyll 2.5.1, wdm 0.1.0, and rouge 1.7.2. I recommend using rouge over pygments for now, mainly to reduce the setup complexity. You can always switch to pygments later.

Note, during the "gem install jekyll" step, if you have jruby installed (say, for a previous project), you may very well get an error that looks like this:
ERROR:  Error installing jekyll:
        ERROR: Failed to build gem native extension.

    C:/jruby/bin/jruby.exe extconf.rb
NotImplementedError: C extension support is not enabled. Pass -Xcext.enabled=tru
e to JRuby or set JRUBY_OPTS.

   (root) at C:/jruby/lib/ruby/shared/mkmf.rb:8
  require at org/jruby/RubyKernel.java:1065
   (root) at C:/jruby/lib/ruby/shared/rubygems/core_ext/kernel_require.rb:1
   (root) at extconf.rb:1

What this says is that jruby does not support native C extensions.

What this means to you is that due to the quirks of the PATH environment variable, you're using jruby's gem.exe instead of ruby's. The fix is to instead install the jekyll gem via "/c/path/to/ruby/installation/bin/gem install jekyll". This is the only gem I encountered that required this - wdm, rouge, and so on were fine with jruby's gem.exe.

== Start using Jekyll

http://jekyllrb.com/docs/quickstart/