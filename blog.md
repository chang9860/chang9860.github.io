---
title: "Project Devlog"
layout: single
permalink: /blog/
author_profile: true
---

Project development log and iteration notes.

Use this writing template: [Devlog Template](/devlog-template/)

{% assign devlog_posts = site.categories.Devlog %}
{% if devlog_posts %}
{% assign devlog_posts = devlog_posts | sort: "date" | reverse %}
{% endif %}
{% if devlog_posts and devlog_posts.size > 0 %}
{% for post in devlog_posts %}
### [{{ post.title }}]({{ post.url }})
<small>{{ post.date | date: site.date_format | default: "%Y-%m-%d" }}</small>
{% if post.project %}<small> | Project: {{ post.project }}</small>{% endif %}
{% if post.sprint %}<small> | Sprint: {{ post.sprint }}</small>{% endif %}

{{ post.excerpt }}

---
{% endfor %}
{% else %}
No devlog posts yet.
{% endif %}
