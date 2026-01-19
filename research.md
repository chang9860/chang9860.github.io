---
title: "Research"
layout: single
permalink: /research/
---

{% for post in site.categories.Research %}
### [{{ post.title }}]({{ post.url }})
<small>{{ post.date | date: "%Y-%m-%d" }}</small>

{{ post.excerpt }}

---
{% endfor %}
