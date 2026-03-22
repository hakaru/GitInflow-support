---
layout: default
title: Blog
lang: en
---

# Blog

{% for post in site.posts_en %}
- [{{ post.title }}]({{ post.url | relative_url }}) — {{ post.date | date: "%B %d, %Y" }}
{% endfor %}

{% if site.posts_en.size == 0 %}
No posts yet. Stay tuned!
{% endif %}
