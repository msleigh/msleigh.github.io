---
layout: post
title:  "Starting with Jekyll"
description: "Getting started with this Jekyll-based GitHub Pages blog"
date:   2022-07-26 22:58:04 +0100
author: msleigh
categories: jekyll update
---
This post is in the `_posts` directory. The site can be rebuilt by running `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated. Since we're using Bundler, `bundle exec jekyll serve`, actually.

Jekyll requires blog post files to be named according to the following format:

`YEAR-MONTH-DAY-title.MARKUP`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file. After that, they include the necessary front matter.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

See [Jekyll docs][jekyll-docs] for more info.

[jekyll-docs]: https://jekyllrb.com/docs/home
