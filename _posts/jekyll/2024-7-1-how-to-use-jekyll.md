---
layout: "post"
title: "How To Use Jekyll"
category: Jekyll
---

## 查看网页

1. 打开 `cmd`。
2. 移动到 `JekBlog` 目录下。
3. 输入 `jekyll serve` 命令。

这将启动一个本地服务器，你可以通过访问 `http://localhost:4000` 来查看你的网站。

## 查看草稿效果

如果你想查看草稿的效果，可以使用以下步骤：

1. 打开 `cmd`。
2. 移动到 `JekBlog` 目录下。
3. 输入 `jekyll serve --drafts` 命令。

*草稿的命名不需要日期信息*

## 查看普通页面(如About)

1. 在`JekBlog`目录下创建md文件,`layout`设置为`page`
2. 在`http://localhost:4000`后接上page路径,如`/dir1/my_page`

*文件无命名规范,且可以放在文件夹中*