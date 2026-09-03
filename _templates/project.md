---
title: "Project Name"
published: false
project_type: personal
status: ongoing
period: "YYYY.MM–YYYY.MM"
role: "My role or responsibility"
team:
  - name: "Team member"
    role: "Role"
stack:
  - "Technology"
tags:
  - subject-area
featured: false
featured_order:
repo_url:
demo_url:
paper_url:
excerpt: "A concise description of the problem, approach, and outcome."
header:
  teaser:
gallery:
  - url: /assets/images/projects/project-slug/example.png
    image_path: /assets/images/projects/project-slug/example.png
    alt: "Description of the image"
    title: "Optional caption"
related:
  paper_reviews: []
  experiments: []
  devlogs: []
---

<!--
USAGE
1. Copy this file to `_projects/<project-slug>.md`.
2. Keep `published: false` while the write-up is incomplete. Change it to true
   or remove the field when the project is ready to appear on the site.
3. Choose one primary `project_type`, for example: personal, course, web,
   systems, algorithm, research-prototype, reproduction, open-source, or team.
4. Use `tags` for subject areas and technologies. They are intentionally not
   tied to AI and can be changed freely for each project.
5. Set `featured: true` only for projects that should appear in the Featured
   Projects sections. Use `featured_order` to control their order.
6. Remove unused front matter, gallery items, subsections, and sections. For an
   individual project, the `team` field can be removed entirely.
7. Preview with `bundle exec jekyll serve`.

Related research is optional. Each item uses `title` and `url`, for example:

related:
  paper_reviews:
    - title: "Paper Review: Example"
      url: /research/example-review/
  experiments:
    - title: "Reproduction: Example"
      url: /research/example-reproduction/
  devlogs:
    - title: "Implementation Notes"
      url: /devlog/example-notes/

The post title is rendered as the page's H1, so this template starts sections at H2.
-->

## Project Overview

Explain what the project is, who or what it is for, and its current state in a short paragraph.

## Motivation

Why did you choose to build this project? Describe the context and what made it worth pursuing.

## Problem

What concrete user, technical, research, or learning problem were you trying to solve?

## Goals

- Define the main outcome the project should achieve.
- List important functional, performance, research, or learning goals.
- Note explicit non-goals when they clarify the scope.

## My Role

Describe your responsibilities and contributions. For team projects, distinguish your work from the team's overall work.

## Architecture / Design

Explain the system structure, component boundaries, data flow, algorithm design, interfaces, or important design decisions. Add diagrams when they improve understanding.

## Implementation

Describe the core implementation and the parts that required the most reasoning. Link to relevant source files or repositories when available.

## Tech Stack

{% if page.stack %}
{% for technology in page.stack %}
- {{ technology }}
{% endfor %}
{% endif %}

Explain why important technologies were selected when the decision involved meaningful trade-offs.

## Challenges

- What technical, design, collaboration, or evaluation problems occurred?
- Which constraints made them difficult?

## Solutions

Explain how the challenges were addressed, which alternatives were considered, and why the final approach was chosen.

## Results

Describe what was completed and provide evidence where possible: functionality, measurements, evaluation results, users, tests, performance, or research findings.

## Demo

{% if page.demo_url %}[Open the live demo]({{ page.demo_url }}){% endif %}

{% if page.gallery %}{% include gallery caption="Project screenshots and results" %}{% endif %}

Add screenshots, GIFs, videos, command output, or usage examples. Remove the placeholder gallery from the front matter if it is not needed.

## What I Learned

What technical knowledge, design judgment, research practice, or teamwork skill did you gain?

## Limitations

What does the current version not handle? Note technical debt, evaluation gaps, known bugs, scale limits, and assumptions.

## Future Work

- What would you improve next?
- Which extension would provide the most value?

## Related Research

{% if page.related.paper_reviews.size > 0 %}
### Paper Reviews
{% for item in page.related.paper_reviews %}
- [{{ item.title }}]({{ item.url | relative_url }})
{% endfor %}
{% endif %}

{% if page.related.experiments.size > 0 %}
### Experiments / Reproductions
{% for item in page.related.experiments %}
- [{{ item.title }}]({{ item.url | relative_url }})
{% endfor %}
{% endif %}

{% if page.related.devlogs.size > 0 %}
### Devlogs
{% for item in page.related.devlogs %}
- [{{ item.title }}]({{ item.url | relative_url }})
{% endfor %}
{% endif %}

Remove this section if the project has no related research or development entries.

## Links

{% if page.repo_url %}- **Repository:** [Source code]({{ page.repo_url }}){% endif %}
{% if page.demo_url %}- **Demo:** [Live demo]({{ page.demo_url }}){% endif %}
{% if page.paper_url %}- **Paper:** [Related paper]({{ page.paper_url }}){% endif %}
