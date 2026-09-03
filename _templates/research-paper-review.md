---
title: "Paper Review: Paper Title"
date: YYYY-MM-DD
categories:
  - Research
research_type: paper-review
tags:
  - paper-review
  - subject-area
excerpt: "A one-sentence summary of the paper and its main contribution."
paper:
  title: "Full Paper Title"
  authors:
    - "Author One"
    - "Author Two"
  venue: "Conference, journal, or archive"
  year: YYYY
paper_url: "https://..."
code_url:
project:
series:
---

<!--
USAGE
1. Copy this file to `_drafts/<paper-slug>.md` while writing.
2. Replace every placeholder in the front matter. Keep `categories: [Research]`
   and `research_type: paper-review` so the review appears in the Research page.
3. Replace `subject-area` with any relevant subject tags. Add or remove tags freely;
   examples include operating-systems, databases, software-engineering, hci,
   machine-learning, or generative-ai.
4. Preview drafts with `bundle exec jekyll serve --drafts`.
5. When ready, move the file to `_posts/YYYY-MM-DD-<paper-slug>.md`.

The post title is rendered as the page's H1, so this template starts sections at H2.
Not every paper needs every section. Remove empty subsections or entire sections
that do not help explain the paper. In particular, Ablation / Analysis,
Connection to My Work, and Reproduction are optional.
-->

## Paper Information

- **Title:** {{ page.paper.title }}
- **Authors:** {{ page.paper.authors | join: ", " }}
- **Venue:** {{ page.paper.venue }}
- **Year:** {{ page.paper.year }}
- **Paper:** [Link]({{ page.paper_url }})
{% if page.code_url %}- **Code:** [Link]({{ page.code_url }}){% endif %}

## One-line Summary

Explain the paper and its main contribution in one sentence.

## Motivation

Why is this problem important? What practical or scientific need motivates it?

## Problem

What limitation, gap, or unresolved question in existing methods does the paper address?

## Key Idea

Describe the central insight in your own words.

## Method

Explain the overall method and how its components work together.

<!-- Keep only the subsections that fit the paper. -->

### Architecture

### Algorithm

### Objective / Loss

### Training

### Inference

### Dataset

## Experiments

What questions do the experiments test? Describe datasets, baselines, metrics, and evaluation settings when relevant.

## Results

Summarize the main quantitative and qualitative results. Distinguish reported evidence from your interpretation.

## Ablation / Analysis

What do the ablations, sensitivity studies, error analyses, or case studies reveal?

## Strengths

- What is convincing, useful, or especially well designed?
- Which claims are supported clearly?

## Limitations

### Limitations Stated by the Authors

- What limitations or future work does the paper acknowledge?

### My Assessment

- What additional weaknesses, assumptions, risks, or missing evaluations do you see?

## What I Learned

What concepts, methods, or research practices became clearer after reading this paper?

## My Thoughts

Record opinions, questions, disagreements, and points that remain unclear.

## Connection to My Work

How could this paper inform a current or future project? Remove this section if there is no useful connection.

## Reproduction

Remove this section if you did not run or implement the work.

### Environment

### Implementation

### Experiment

### Result

### Difference from the Paper

## Next Questions

- What research questions follow from this paper?
- Which related or cited papers should be read next?

## References

- Add related papers, documentation, datasets, and implementation links used in the review.
