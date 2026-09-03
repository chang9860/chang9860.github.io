---
title: "Research"
layout: single
permalink: /research/
author_profile: true
---

This hub collects paper reviews, reproductions, experiments, benchmarks, technical surveys, research notes, and longer-running research projects across different areas of computer science.

Research entries use three simple dimensions:

- **Category** defines the main site section: `Research`
- **Research type** describes the kind of work, such as `paper-review`, `reproduction`, or `experiment`
- **Tags** describe subjects and technologies and can grow freely over time

{% assign research_posts = site.posts | where_exp: "post", "post.categories contains 'Research'" | sort: "date" | reverse %}
{% assign research_type_groups = research_posts | group_by: "research_type" | sort: "name" %}

{% if research_posts.size > 0 %}
## Latest Research

<div class="content-grid content-grid--single">
  {% for post in research_posts limit: 5 %}
    {% include content-card.html entry=post show_type=true %}
  {% endfor %}
</div>

## Browse by Content Type

<ul class="taxonomy__index">
  {% for research_group in research_type_groups %}
    {% assign type_name = research_group.name | default: "research-note" %}
    <li>
      <a href="#type-{{ type_name | slugify }}">
        <strong>{{ type_name | replace: "-", " " | capitalize }}</strong>
        <span class="taxonomy__count">{{ research_group.items.size }}</span>
      </a>
    </li>
  {% endfor %}
</ul>

## Browse by Topic

{% assign sorted_tags = site.tags | sort %}
{% assign research_tag_count = 0 %}
<ul class="taxonomy__index">
  {% for tag in sorted_tags %}
    {% assign tagged_research = tag[1] | where_exp: "post", "post.categories contains 'Research'" %}
    {% if tagged_research.size > 0 %}
      {% assign research_tag_count = research_tag_count | plus: 1 %}
      <li>
        <a href="{{ '/tags/' | relative_url }}#{{ tag[0] | slugify }}">
          <strong>{{ tag[0] }}</strong>
          <span class="taxonomy__count">{{ tagged_research.size }}</span>
        </a>
      </li>
    {% endif %}
  {% endfor %}
</ul>

{% if research_tag_count == 0 %}
<p class="empty-state">Topic links will appear automatically when Research posts add tags.</p>
{% endif %}

{% for research_group in research_type_groups %}
  {% assign type_name = research_group.name | default: "research-note" %}
  <section id="type-{{ type_name | slugify }}" class="taxonomy__section">
    <h2 class="archive__subtitle">{{ type_name | replace: "-", " " | capitalize }}</h2>
    <div class="entries-list">
      {% for post in research_group.items %}
        {% include archive-single.html type="list" %}
      {% endfor %}
    </div>
    <a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: "Back to Top" }} &uarr;</a>
  </section>
{% endfor %}

<p>
  Continue exploring through the site-wide
  <a href="{{ '/categories/' | relative_url }}">category</a> and
  <a href="{{ '/tags/' | relative_url }}">tag</a> archives.
</p>
{% else %}
## Start Here

<p class="empty-state">Research entries will appear here as papers are reviewed, results are reproduced, and experiments are completed.</p>

- Use `research_type: paper-review` for a paper review.
- Use `research_type: reproduction` for a reproduction attempt.
- Use `research_type: experiment` or `benchmark` for technical experiments.
- Use `research-note`, `technical-survey`, or `research-project` when those better describe the work.
{% endif %}
