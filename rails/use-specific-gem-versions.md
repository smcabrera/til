# Use specific gem versions

This is something I actually learned a little bit ago but I thought I'd add it now. Previously I've always just added a new gem by going to my gemfile and adding the line:

```
gem 'gemname'
```

to the bottom. I figured out that I should probably put development specific gems with their own kind but that's about it. I knew that it was possible to use specific versions of gems but I didn't know why you'd want to do that.

Then recently I encountered problems when I started working on something I hadn't worked on in a while and my gems suddenly stopped working. It wasn't a nightmare, but it was a slight hassle as I had to go figure out what versions of each gem I needed. All this could have been avoided by locking down my gem versions when I first add them.

For instance if you're using rspec you can add it like this:

```
  gem 'rspec-rails', '~> 3.1.0'
```
and the little squiggly arrow will say go grab the latest version of rspec that's greater than or equal to 3.1.0 but less than version 3.2.0. Now sure maybe at some point you want the latest version of this gem, and obviously you want minor bug fixes but this is a good compromise for making sure that you'll get the newest version that isn't likely to break your setup. Because of the way versions are set, they're basically set so that within the second number things shouldn't break.

So if you just add the latest version of the gem when you first add it you can be confident that it will keep working in the future. If you want an upgraded version you can always do that, but this is a sensible default. The [rubygems](http://www.rubygems.org) site makes this easy since you can just type in the name of a gem and it will give you something you can click on and automatically copy the code for adding the latest version of the gem to your gemfile. Nice and easy.

## Gemrat
In case you're lazy there's actually a gem called gemrat which will do this for you. Install it with ```gem install gemrat``` and then when you need to add a new gem to your project you just call ```gemrat gemname``` and you'll get the latest version. You can specify options to make it pessimistic (the setting I used above) or optimistic. Upon running the command the gem will be added to your gemfile and bundle will be run so that the gem will automatically be installed.


