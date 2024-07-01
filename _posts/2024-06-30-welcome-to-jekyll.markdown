---
layout: post
title:  "Welcome to Jekyll!"
date:   2024-06-30 22:39:34 +0800
categories: jekyll update
---
My Note here!
Frontmatter 是 Jekyll 网站生成器用来存储页面或帖子的元数据的一种机制。它位于 Markdown 文件的顶部，被三条短横线（---）包围。在这个例子中，Frontmatter 包含了以下键值对：

layout: 指定了使用哪个布局模板。在这个例子中，它的值是 post，意味着这个页面将使用 _layouts/post.html 模板进行渲染。
title: 页面或帖子的标题。这里的标题是 "Welcome to Jekyll! Hi"。
date: 帖子的发布日期和时间。格式为 年-月-日 时:分:秒 +时区，在这个例子中是 2024-06-30 22:39:34 +0800。
categories: 用于对帖子进行分类的类别。这里的类别是 jekyll update。

Frontmatter 允许你为每个页面或帖子指定一系列配置选项和变量，这些变量可以在页面的其他部分或者在布局模板中被引用。Jekyll 会解析这些 Frontmatter 配置，以决定如何构建和渲染页面。

You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

Jekyll requires blog post files to be named according to the following format:

`YEAR-MONTH-DAY-title.MARKUP`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file. After that, include the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
