---
layout: category
title: "Problem Solving"
permalink: /categories/probelm-solving/
category: probelm-solving
---

## 🏆 Problem Solving 관련 글

{% assign category_name = "probelm-solving" %}
{% assign category_posts = site.categories[category_name] %}

{% if category_posts.size > 0 %}
  <ul>
    {% for post in category_posts %}
      <li><a href="{{ post.url | relative_url }}">{{ post.title }}</a> ({{ post.date | date: "%Y-%m-%d" }})</li>
    {% endfor %}
  </ul>
{% else %}
  <p>이 카테고리에 해당하는 게시글이 없습니다.</p>
{% endif %}
