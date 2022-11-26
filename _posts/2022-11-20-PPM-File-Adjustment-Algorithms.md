---
layout: post
title:  "PPM File Adjustment Algorithms"
date:   2022-11-20 13:50:39
categories: algorithms
---
<small>Because of code confidentiality, this page only demonstrates the framework</small>
<br>
<br>
<h1>PPM File Adjustment Algorithms</h1>
The primary image resizing algorithm is based on a seam-carving algorithm. The task of the algorithm set is to apply seam carving for content-aware resizing of images. The core algorithm works by finding and removing “seams” in the image that pass through the least important pixels. For a quick introduction, check out [this video][video-link].
<br>
<br>
For example:
![cv-demo](elevenychen.github.io/static/projects/pv-demo.png)
<br>
<h2>Table of Content</h2>
1. Fundations of objects
2. Basic functions



You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.


{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

[video-link]:  https://www.youtube.com/watch?v=6NcIJXTlugc
