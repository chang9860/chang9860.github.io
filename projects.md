---
title: "Portfolio"
layout: single
permalink: /projects/
author_profile: true
---

Selected portfolio projects.

{% assign portfolio_posts = site.categories.Portfolio %}
{% if portfolio_posts %}
{% assign portfolio_posts = portfolio_posts | sort: "date" | reverse %}
{% endif %}
{% if portfolio_posts and portfolio_posts.size > 0 %}
{% for post in portfolio_posts %}
<article class="home-card">
  <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
  <p class="home-card-meta">{{ post.date | date: site.date_format | default: "%Y-%m-%d" }}</p>
  {% if post.role %}<p class="home-card-meta"><strong>Role:</strong> {{ post.role }}</p>{% endif %}
  {% if post.period %}<p class="home-card-meta"><strong>Period:</strong> {{ post.period }}</p>{% endif %}
  {% if post.stack %}<p class="home-card-meta"><strong>Stack:</strong> {{ post.stack | join: ", " }}</p>{% endif %}
  <p>{{ post.excerpt | strip_html }}</p>
  <p>
    <a href="{{ post.url }}">Details</a>
    {% if post.demo_url %} | <a href="{{ post.demo_url }}">Demo</a>{% endif %}
    {% if post.repo_url %} | <a href="{{ post.repo_url }}">Code</a>{% endif %}
  </p>
</article>
{% endfor %}
{% else %}
No portfolio posts yet.
{% endif %}
