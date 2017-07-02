---
layout: post
title: URLSession example
---

最简单的使用URLSession就是配合使用GET，扔下网址，直接召唤，例子如下：

<script src="https://gist.github.com/KrisYu/1be1400c254d0ccda77f10cd7473503a.js"></script>


升级一点，结合iTunes Search API的例子，这里可以看几个点：

- url可以用URLComponents和URLQueryItem结合来看
- 这个static参数最后一个pass in是一个 escaping 的 completionHandler
- dump可以展示一个更好的print效果、
- 也可以用中文搜索，可以看iTunes Search API的页面看更多定制

<script src="https://gist.github.com/KrisYu/10764e91331b3ddd1dcab5efa1aa6d9d.js"></script>

