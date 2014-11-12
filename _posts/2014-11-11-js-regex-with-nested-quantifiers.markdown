---
layout: post
title:  "JavaScript Regexes with nested quantifiers"
date:   2014-11-11 20:48:02
categories: javascript development
---

This is an example to illustrate performance issues caused by regexes with nested quantifiers. The example and numbers are taken from the [high-performance-js]["High Performance JavaScript"]

{% highlight javascript %}
n = 15
str = Array(n).join("A") // produces "AAAAAAAAAAAAAAA"
res = str.match(/(A+A+)+B/)
{% endhighlight %}

The worst case complexity of this regex is O(2^n) backtracking steps for the match to fail. 
For n=35 this will require 34 bln backtracking operations which will make most of modern browsers to hang for a while.

The key to preventing this kind of problem is to make sure that two parts of a regex cannot match the same part of a string. For this regex, the fix is to rewrite it as /AA+B/


JS Perf which compares the first regex with the second: [js-perf-link][]




[high-performance-js]: http://www.amazon.com/Performance-JavaScript-Faster-Application-Interfaces/dp/059680279X
[js-perf-link]: http://jsperf.com/regex-with-nested-quantifiers
