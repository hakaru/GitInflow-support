---
layout: default
title: ブログ
lang: ja
---

# ブログ

{% for post in site.posts_ja %}
- [{{ post.title }}]({{ post.url | relative_url }}) — {{ post.date | date: "%Y年%m月%d日" }}
{% endfor %}

{% if site.posts_ja.size == 0 %}
まだ記事はありません。お楽しみに！
{% endif %}
