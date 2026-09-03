---
title: "CV"
layout: single
permalink: /cv/
author_profile: true
---

## Summary

Computer science student interested in understanding ideas through reading, implementation, and experimentation. This site records that work across research notes, software projects, and development logs.

## Education

GIST

## Experience

It will be soon.

## Selected Projects

{% assign selected_projects = site.projects | where: "featured", true | sort: "featured_order" %}
{% if selected_projects.size > 0 %}
{% for project in selected_projects %}
- [{{ project.title }}]({{ project.url | relative_url }}){% if project.role %} — {{ project.role }}{% endif %}
{% endfor %}
{% else %}
Selected projects will be added as project write-ups are completed.
{% endif %}

## Research

Paper reviews, reproductions, experiments, and research notes are available on the [Research page]({{ '/research/' | relative_url }}).

## Skills

Technical skills will be listed here as the CV is updated.

## Awards / Activities

This section will be added when applicable.

## Links

- [GitHub](https://github.com/chang9860)
- [Research]({{ '/research/' | relative_url }})
- [Projects]({{ '/projects/' | relative_url }})

<!-- Add a PDF link here after uploading assets/files/CV_Changhyeon_Ahn.pdf. -->
