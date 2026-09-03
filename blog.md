---
title: "Devlog"
layout: single
permalink: /blog/
author_profile: true
---

Notes from studying computer science and building software: concepts, implementation details, debugging, frameworks, systems, languages, and engineering practices.

{% assign os_notes = site.posts | where: "series", "ban-hyokyung-os" | sort: "series_order" %}
{% if os_notes.size > 0 %}
## Series

### Operating Systems Lecture Notes

반효경 운영체제 강의의 챕터별 학습 기록입니다.

<ol class="series-list">
  {% for post in os_notes %}
    <li><a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>
  {% endfor %}
</ol>
{% endif %}

{% assign devlog_posts = site.posts | where_exp: "post", "post.categories contains 'Devlog'" | sort: "date" | reverse %}
{% if devlog_posts.size > 0 %}
## All Devlogs

<div class="content-grid content-grid--single">
  {% for post in devlog_posts %}
    {% include content-card.html entry=post show_type=true %}
  {% endfor %}
</div>
{% else %}
<p class="empty-state">Devlog entries will appear here.</p>
{% endif %}

For future entries, see the [Devlog writing template]({{ '/devlog-template/' | relative_url }}).
