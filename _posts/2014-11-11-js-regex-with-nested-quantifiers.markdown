---
layout: post
title:  "JavaScript Regexes with nested quantifiers"
date:   2014-11-11 20:48:02
categories: javascript development
---

This is an example to illustrate performance issues caused by regexes qith nested quantifiers. The example and numbers are taken from the book "High Performance JavaScript"

{% highlight javascript %}
n = 15
str = Array(n).join("A") // produces "AAAAAAAAAAAAAAA"
res = str.match(/(A+A+)+B/)
{% endhighlight %}

The worst case complexity of this regex is O(2^n) backtracking steps for the match to fail. 
For n=35 this will require 34 bln backtracking operations which will make most of modern browsers to hang for a while.

The key to preventing this kind of problem is to make sure that two parts of a regex cannot match the same part of a string. For this regex, the fix is to rewrite it as /AA+B/


Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help].

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
