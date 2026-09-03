# Changhyeon Ahn — Personal Portfolio

Source repository for my [GitHub Pages portfolio](https://chang9860.github.io).

I use this site to document what I study and build across Computer Science, AI,
and Software Engineering. Current interests may change over time and do not
define the permanent scope of the site.

## What I Document

- Paper reviews
- Research notes
- Experiments and reproductions
- Projects and research prototypes
- Development and CS study notes

## Website

[https://chang9860.github.io](https://chang9860.github.io)

## Structure

- **Research** — paper reviews, reproductions, experiments, benchmarks, surveys, and research notes
- **Projects** — complete or presentable personal, course, research, open-source, and team projects
- **Devlog** — CS study notes, implementation records, debugging, and software engineering notes
- **CV** — education, experience, selected work, skills, and activities
- **Topics / Tags** — secondary navigation by content type and subject area

Research and Devlog entries are stored in `_posts`, project pages in
`_projects`, and reusable writing templates in `_templates`.

See the [Content Guide](docs/content-guide.md) for naming, front matter,
taxonomy, images, and publishing conventions.

## Tech

- Jekyll
- GitHub Pages
- [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) 4.27.3

## Local Development

This repository uses Ruby and Bundler. The following commands are used by the
current project:

```sh
bundle install
bundle exec jekyll serve
```

To preview posts under `_drafts`:

```sh
bundle exec jekyll serve --drafts
```

## Attribution and License

The site is based on the Minimal Mistakes Jekyll theme by Michael Rose and
contributors. The included theme source remains available under the MIT License;
see [LICENSE](LICENSE) for the copyright notice and license terms.
