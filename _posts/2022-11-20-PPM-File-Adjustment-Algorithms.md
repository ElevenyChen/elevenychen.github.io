---
layout: post
title:  "PPM File Adjustment Algorithms"
date:   2022-11-20 13:50:39
categories: algorithms
---
<p><small>Because of code confidentiality, this page only demonstrates the framework</small></p>

<h1>PPM File Adjustment Algorithms</h1></p>
The primary image resizing algorithm is based on a seam-carving algorithm. The task of the algorithm set is to apply seam carving for content-aware resizing of images. The core algorithm works by finding and removing “seams” in the image that pass through the least important pixels. For a quick introduction, check out [this video]. </p>
[this video]:  https://www.youtube.com/watch?v=6NcIJXTlugc
<h2>Table of Content</h2></p>
1. Fundations of objects
2. Basic functions



You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help].

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
