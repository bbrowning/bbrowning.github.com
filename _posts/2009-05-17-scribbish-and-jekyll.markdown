---
title: Scribbish and Jekyll

layout: post
---

I really wanted a minimalistic, simple theme for my blog. After looking around a bit I settled on [Scribbish][], a popular theme in the Ruby world with packages for Typo, Mephisto, and WordPress. Unfortunately there's no package for Jekyll so I decided to try and port it myself.

[scribbish]: http://quotedprintable.com/pages/scribbish

Both Mephisto and Jekyll use the Liquid templating engine so the port was pretty straightforward. It's still a work-in-progress but the basics are finished.

Jekyll has an include tag to create reusable components but, unlike Mephisto's, you can't directly pass variables to the included file. This is fairly easy to workaround by using Liquid's `assign` tag or explicitly looping over a collection of objects instead of using Mephisto's shortcuts. For example:

**Jekyll**
{% highlight text %}
{ % for post in site.posts % }
  { % include post.html % }
{ % endfor % }
{% endhighlight %}

**Mephisto**
{% highlight text %}
{ % include 'article' with articles % }
{% endhighlight %}

*There shouldn't be a space between the brackets and percent signs but I had to add one for display reasons*

The Jekyll include tag looks for an `_includes` directory at the root source directory. However, if you try to use the include tag from an already included file there's a bug where it looks for `_includes/_includes/included_file.html`. To workaround this for now I just created a symlink in the `_includes` directory to itself.
{% highlight text %}
cd _includes && ln -s . _includes
{% endhighlight %}

Take a look at this blog's [source][blog_source], particularly the \_layouts and \_includes directories, if you'd like to use the Scribbish theme for your own Jekyll-based blog.

[blog_source]: http://github.com/bbrowning/bbrowning.github.com/tree/master
