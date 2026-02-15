---
title: "Research"
layout: single
permalink: /research/
author_profile: true
---

Research notes, paper summaries, and experiment results.

{% assign research_posts = site.categories.Research %}
{% if research_posts %}
{% assign research_posts = research_posts | sort: "date" | reverse %}
{% endif %}
{% if research_posts and research_posts.size > 0 %}
{% for post in research_posts %}
### [{{ post.title }}]({{ post.url }})
<small>{{ post.date | date: site.date_format | default: "%Y-%m-%d" }}</small>

{{ post.excerpt }}

---
{% endfor %}
{% else %}
No research posts yet.
{% endif %}
