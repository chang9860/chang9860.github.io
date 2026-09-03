---
title: "Projects"
layout: single
permalink: /projects/
author_profile: true
---

Projects are complete or presentable outcomes from personal work, courses, research prototypes, paper reproductions, open-source contributions, and team projects.

{% assign featured_projects = site.projects | where: "featured", true | sort: "featured_order" %}
{% if featured_projects.size > 0 %}
## Featured Projects

<div class="content-grid">
  {% for project in featured_projects %}
    {% include content-card.html entry=project show_type=true show_role=true show_stack=true show_links=true %}
  {% endfor %}
</div>
{% endif %}

{% assign all_projects = site.projects | sort: "title" %}
{% assign other_projects = all_projects | where_exp: "project", "project.featured != true" %}
{% if other_projects.size > 0 %}
{% if featured_projects.size > 0 %}
## More Projects
{% else %}
## All Projects
{% endif %}

<div class="content-grid">
  {% for project in other_projects %}
    {% include content-card.html entry=project show_type=true show_role=true show_stack=true show_links=true %}
  {% endfor %}
</div>
{% elsif all_projects.size == 0 %}
<p class="empty-state">Project write-ups will be added as implementations reach a presentable stage.</p>
{% endif %}
