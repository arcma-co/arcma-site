# Content

Everything a visitor reads on arcma.co. Alyssa writes it; agents place it exactly as written.

## Site-wide: `site.yaml`

Facts used on many pages: the contact address and social profiles. Every email link and social icon on the site points here.

## Pages: `pages/<page>.yaml`

One file per page. Top-level keys are the page's sections in the order they appear; nested keys are the slots inside each section.

```yaml
hero:
  headline: |-
    LEAD FROM
    THE SOURCE
  body: |-
    First paragraph.

    Second paragraph.
  cta:
    label: spiral in
    href: /contact
```

- Text that runs over one line starts with `|-` on the key's line and is indented below it. Line breaks are kept exactly; nothing needs quoting.
- Single-line text sits after the colon. If it starts with a quote mark or contains `: `, wrap it in single quotes: `quote: '"Everything is aligned."'`.
- Write display lines in the case they should read. Some Framer styles also force capitals.
- Each key maps to one Framer layer through `framer/slots.yaml`. A new key needs a matching layer, so new sections are a design change as well as a copy change.

## Shared sections: `sections/<name>.yaml`

Sections that appear on several pages, like the Book A Session block at the foot of the homepage, The Work and Contact. Same format as pages; one edit changes every page that uses it.

## Case studies: `cases/<name>.md`

Frontmatter holds the short fields; the body holds the long-form text.

```markdown
---
title: 'Structural Coherence: Multi-Acquisition Integration'
slug: structural-coherence          # the URL: /case-studies/<slug>
draft: false                        # true keeps it off the live site
intro: The summary shown on the card.
tags: [merger, acquisition]
quote: '"The pull quote."'
---

<!-- framer:lead -->
## The Field
...
```

The `<!-- framer:... -->` lines mark which rich-text block of the current Framer template each part fills: `lead`, `text-a`, `text-b`. They are invisible on the page. They go away when the case template is redesigned.

## Journal: `journal/<name>.md`

Same shape as case studies. Not yet imported from Framer.

## Formatting inside text

`*italic*`, `**bold**`, `[link text](https://…)`. In case-study bodies, a line ending in `\` is a line break inside a paragraph.
