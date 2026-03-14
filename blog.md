---
layout: page
title: 技术文章
permalink: /blog/
---

<ul class="post-list">
  {% for post in site.posts %}
  <li>
    <span class="post-date">{{ post.date | date: "%Y-%m-%d" }}</span>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
  </li>
  {% endfor %}
</ul>

{% if site.posts.size == 0 %}
<p>暂无文章，敬请期待。</p>
{% endif %}
