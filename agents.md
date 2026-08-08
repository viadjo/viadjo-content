# Content Repository Guide

This repository contains all text content for ViaDjo, structured as markdown files with YAML frontmatter. It is consumed as a git submodule by downstream projects (website, documents).

## Structure

```
content/
├── en/                    # English
│   ├── pages/             # Page content (home, privacy, terms, 10-steps)
│   ├── services/          # Service descriptions (buying, selling, investing)
│   ├── tips/              # Real estate tip articles
│   └── testimonials/      # Client reviews
└── nl/                    # Dutch (same structure)
```

## Content format

All files use markdown with YAML frontmatter:

```markdown
---
title: Page Title
---

Content in markdown.
```

### Home page (`content/{lang}/pages/home.md`)

Uses `## section_name` headers to define named content blocks (`hero`, `about_lead`, etc.).

### Services (`content/{lang}/services/*.md`)

Frontmatter: `title`, `icon`. Two sections: `## summary` and `## details`.

### Tips (`content/{lang}/tips/*.md`)

Frontmatter: `title`, `slug`, `order`, `summary`. Body contains the full article.

### Testimonials (`content/{lang}/testimonials/*.md`)

Frontmatter: `cite`. Body contains the quote text.

### Templates (`content/{lang}/templates/*.md`)

Legal document templates use markdown with YAML frontmatter. The frontmatter contains metadata, variable defaults, and structured data (arrays). All visible text lives in the markdown body.

Components use `{{variable}}` for data injection — these indicate where the React component inserts dynamic values (user input, API data, form fields). Don't change the variable names without coordinating with the build script (`src/lib/template-parser.ts` in viadjo-documents).

Format conventions:
- `# TITLE` — document title
- `## Section Name` (non-numbered) — named blocks (Partijen, Bijlagen)
- `## N. Section Title` — numbered legal sections
- `### Sub-heading` — sub-sections
- `{{variable_name}}` — dynamic content injection point
- `{{if:key}} text {{endif}}` — conditional text block (shown/hidden by component)
- `| Column1 | Column2 |` — table column headers
- `Label: {{variable}}` — labeled form fields

## Bilingual

English in `content/en/`, Dutch in `content/nl/`. Same file structure, keep translations consistent.

## Important

This content is channel-neutral — it feeds multiple outputs (website, documents, social media). Avoid website-specific formatting or references.
