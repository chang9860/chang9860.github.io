# Content Guide

이 문서는 이 포트폴리오에 Research, Project, Devlog 콘텐츠를 지속적으로 추가하기 위한 실용적인 작성 가이드다. 글의 성격이 여러 영역에 걸칠 수 있으므로 분류를 지나치게 엄격하게 적용하지 않는다. 독자가 글의 목적과 결과를 가장 자연스럽게 이해할 수 있는 위치를 선택한다.

## 콘텐츠 구분

| 구분 | 주로 기록하는 내용 | 저장 위치 |
| --- | --- | --- |
| Research | 논문 리뷰, 재현, 실험, benchmark, 기술 조사, 연구 노트 | `_posts` |
| Projects | 직접 만든 완성된 결과물, prototype, 수업·팀·오픈소스 프로젝트 | `_projects` |
| Devlog | CS 학습 노트, 개발 기록, debugging, 도구와 기술 사용 경험 | `_posts` |

일반적인 발전 과정은 다음과 같지만 반드시 이 순서를 따를 필요는 없다.

```text
Paper Review → Reproduction → Experiment → Project
```

- 논문을 읽고 이해·평가한 글은 **Paper Review**로 작성한다.
- 논문의 방법이나 결과를 직접 구현하고 확인했다면 **Reproduction**으로 작성한다.
- 재현에서 출발했더라도 독립적인 가설이나 설정을 검증한다면 **Experiment**로 작성한다.
- 여러 구현과 실험을 바탕으로 사용하거나 시연할 수 있는 결과물을 만들었다면 **Project**로 정리할 수 있다.
- 공부 과정이나 구현 중 배운 내용을 짧게 남기는 편이 자연스럽다면 **Devlog**로 작성한다.

## 1. Paper Review 작성 방법

범용 템플릿은 `_templates/research-paper-review.md`에 있다.

1. 템플릿을 `_drafts`로 복사한다.
2. front matter의 논문 정보와 tag를 수정한다.
3. 필요하지 않은 본문 섹션은 삭제한다.
4. `--drafts` 옵션으로 확인한다.
5. 완성되면 날짜가 포함된 이름으로 `_posts`에 옮긴다.

```powershell
Copy-Item _templates/research-paper-review.md _drafts/paper-slug.md
bundle exec jekyll serve --drafts
Move-Item _drafts/paper-slug.md _posts/2026-09-03-paper-slug.md
```

기본 front matter:

```yaml
---
title: "Paper Review: Paper Title"
date: 2026-09-03
categories:
  - Research
research_type: paper-review
tags:
  - paper-review
  - subject-area
excerpt: "논문의 핵심 기여를 설명하는 한 문장"
paper:
  title: "Full Paper Title"
  authors: ["Author One", "Author Two"]
  venue: "Conference or Journal"
  year: 2026
paper_url: "https://..."
code_url:
---
```

## 2. Experiment / Reproduction 작성 방법

템플릿은 `_templates/research-experiment.md`에 있다. 작성 과정은 Paper Review와 동일하며 글의 목적에 따라 `research_type`만 선택한다.

```yaml
research_type: experiment
```

```yaml
research_type: reproduction
```

성능이나 동작 비교가 중심이라면 다음 값을 사용할 수 있다.

```yaml
research_type: benchmark
```

작성 시작:

```powershell
Copy-Item _templates/research-experiment.md _drafts/experiment-slug.md
bundle exec jekyll serve --drafts
```

기본 front matter:

```yaml
---
title: "Experiment: Topic"
date: 2026-09-03
categories:
  - Research
research_type: experiment
tags:
  - experiment
  - subject-area
excerpt: "실험의 목적과 주요 결과"
repo_url:
series:
related:
  paper_review:
  reproduction:
  previous_experiment:
  project:
---
```

## 3. Project 작성 방법

Project는 블로그 글이 아니라 `_projects` collection에 저장한다. 템플릿은 `_templates/project.md`에 있다.

```powershell
Copy-Item _templates/project.md _projects/project-slug.md
bundle exec jekyll serve
```

작성 중에는 다음 값을 유지한다.

```yaml
published: false
```

공개할 때 `published: true`로 바꾸거나 이 필드를 제거한다. Home의 Featured Projects에 표시하려는 프로젝트만 `featured: true`로 설정한다.

기본 front matter:

```yaml
---
title: "Project Name"
published: false
project_type: personal
status: ongoing
period: "2026.03–2026.09"
role: "My role"
stack:
  - "Technology"
tags:
  - subject-area
featured: false
featured_order:
repo_url:
demo_url:
paper_url:
excerpt: "문제, 접근 방법, 결과를 요약한 짧은 설명"
header:
  teaser:
---
```

`project_type`에는 `personal`, `course`, `web`, `systems`, `algorithm`, `research-prototype`, `reproduction`, `open-source`, `team` 등 프로젝트를 가장 잘 설명하는 값을 하나 선택한다.

## 4. Devlog 작성 방법

템플릿은 `_templates/devlog.md`에 있다. Devlog도 `_drafts`에서 작성한 뒤 `_posts`로 옮긴다.

```powershell
Copy-Item _templates/devlog.md _drafts/devlog-slug.md
bundle exec jekyll serve --drafts
Move-Item _drafts/devlog-slug.md _posts/2026-09-03-devlog-slug.md
```

기본 front matter:

```yaml
---
title: "Topic"
date: 2026-09-03
categories:
  - Devlog
devlog_type: study-note
tags:
  - subject-area
  - technology
series:
series_order:
project:
excerpt: "글의 핵심 내용을 설명하는 짧은 문장"
---
```

`devlog_type`은 `study-note`, `implementation`, `debugging`, `framework`, `language`, `infrastructure`, `engineering-note` 등에서 선택하거나 필요에 맞는 값을 사용할 수 있다.

## 5. Category 사용 원칙

Category는 글의 주제가 아니라 사이트의 큰 콘텐츠 영역을 나타낸다.

- 논문, 연구, 실험, 기술 조사: `Research`
- 공부와 개발 과정의 기록: `Devlog`
- Project는 `_projects` collection을 사용하므로 category가 필요하지 않다.

가능하면 `_posts` 글 하나에는 주된 category 하나만 사용한다. 현재 permalink가 category를 포함하므로 게시 후 category를 바꾸면 URL이 달라질 수 있다. 이미 공개한 글의 category를 변경해야 한다면 먼저 기존 URL과 동일한 `permalink`를 명시한다.

```yaml
permalink: /research/original-slug/
```

Category 이름은 기존 구조와 맞게 `Research`, `Devlog`처럼 대소문자를 유지한다.

## 6. Tag 사용 원칙

Tag는 분야, 기술, 개념을 표현하는 보조 탐색 수단이다. Research Hub와 Tags 페이지는 실제로 사용된 tag를 자동으로 표시한다.

권장 규칙:

- 소문자 kebab-case를 사용한다: `operating-systems`, `software-engineering`
- 너무 넓은 tag와 너무 세부적인 tag를 과도하게 함께 넣지 않는다.
- 한 글에 핵심 tag 3~6개 정도를 우선한다.
- 같은 개념에 여러 표기를 만들지 않는다: `database`와 `databases` 중 하나를 일관되게 사용한다.
- 연재 순서는 tag 대신 `series`, `series_order`로 관리한다.
- 새로운 분야가 생기면 별도 설정 없이 새 tag를 사용할 수 있다.

예시:

```yaml
tags:
  - paper-review
  - distributed-systems
  - consensus
```

## 7. 이미지 저장 위치 및 사용 방법

새 이미지는 콘텐츠별 디렉터리에 모아 둔다.

```text
assets/images/research/<post-slug>/
assets/images/projects/<project-slug>/
assets/images/devlog/<post-slug>/
```

Markdown에서 다음처럼 사용한다.

```md
![Architecture diagram]({{ '/assets/images/research/post-slug/architecture.png' | relative_url }})
```

규칙:

- 웹 경로에는 역슬래시(`\`)가 아니라 슬래시(`/`)를 사용한다.
- 파일명은 가능하면 소문자 kebab-case로 작성한다.
- 의미 있는 alt text를 작성한다.
- 원본이 지나치게 크다면 웹에서 볼 수 있는 크기로 줄인다.
- Project 카드 대표 이미지는 `header.teaser`에 지정한다.

```yaml
header:
  teaser: /assets/images/projects/project-slug/teaser.png
```

여러 이미지는 Project 템플릿의 `gallery` 예시를 사용할 수 있다.

## 8. 내부 글 링크하는 방법

본문에서는 공개 URL과 `relative_url` 필터를 사용한다.

```md
[Related Paper Review]({{ '/research/paper-slug/' | relative_url }})
[Related Project]({{ '/projects/project-slug/' | relative_url }})
[Related Devlog]({{ '/devlog/devlog-slug/' | relative_url }})
```

Experiment는 선택적인 `related` 필드로 연결할 수 있다.

```yaml
related:
  paper_review: /research/paper-slug/
  previous_experiment: /research/previous-experiment/
  project: /projects/project-slug/
```

Project는 여러 관련 글을 배열로 연결할 수 있다.

```yaml
related:
  paper_reviews:
    - title: "Paper Review: Example"
      url: /research/paper-slug/
  experiments:
    - title: "Experiment: Example"
      url: /research/experiment-slug/
  devlogs:
    - title: "Implementation Notes"
      url: /devlog/devlog-slug/
```

관련 글이 없다면 필드를 비우거나 제거해도 된다.

## 9. 새 글 파일명 규칙

Research와 Devlog는 Jekyll post 규칙을 따른다.

```text
_posts/YYYY-MM-DD-short-descriptive-slug.md
```

예시:

```text
_posts/2026-09-03-paper-title-review.md
_posts/2026-09-04-database-benchmark.md
_posts/2026-09-05-rust-debugging-notes.md
```

Project는 날짜 없이 안정적인 slug를 사용한다.

```text
_projects/project-slug.md
```

파일명 규칙:

- 영어 소문자와 숫자, 하이픈을 사용한다.
- 공백과 밑줄은 새 파일에서 사용하지 않는다.
- 게시 후에는 URL 보존을 위해 파일명과 category를 가급적 변경하지 않는다.
- 제목은 바꿀 수 있지만 공개 URL은 안정적으로 유지한다.

## 10. Front Matter 체크리스트

새 글을 공개하기 전에 다음을 확인한다.

- `title`이 구체적인가?
- `date`와 파일명의 날짜가 일치하는가?
- `categories`가 `Research` 또는 `Devlog`로 올바른가?
- `research_type` 또는 `devlog_type`이 글의 성격을 설명하는가?
- tag 표기가 기존 글과 일관적인가?
- `excerpt`가 목록 카드에서 이해할 수 있는 한두 문장인가?
- 내부 링크와 이미지 경로가 실제로 존재하는가?
- Project라면 `published`, `featured`, `status` 값이 의도한 상태인가?

마지막으로 로컬에서 확인한다.

```powershell
bundle exec jekyll serve --drafts
```

공개 빌드와 가까운 조건을 확인하려면 다음 명령을 사용할 수 있다.

```powershell
bundle exec jekyll build --safe
```
