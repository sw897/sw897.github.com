---
layout: page
title: sw897的博客
description: "sw897的博客，技术，人文，随笔"
keywords: "技术，人文，随笔"
tagline: 技术，人文，随笔
---
{% include JB/setup %}

## 文章列表
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


