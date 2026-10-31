# Decisions

Structural decisions about arcma.co and why they were made. Newest last. Append, never rewrite: if a decision changes, add a new entry that supersedes the old one.

---

### 001 · This repository is the source of truth
**2026-10-30**

All copy, case studies, design tokens and code live here, and git history is the changelog. Framer is a render target until cutover. Changes land here first and are then applied to Framer.

*Why:* Work on the site has moved between several Claude and Codex sessions, and no single one held the full state. A repository holds it for every session and records every change.

### 002 · Stage 1 changes copy and CMS content only
**2026-10-30**

While the site is on Framer, updates are limited to text in existing layers and CMS items. No new Framer components or layouts.

*Why:* Anything built in Framer is rebuilt in the Astro site. Copy and CMS content carry over unchanged.

### 003 · Framer state is mirrored in `framer/`, not backed up by timestamp
**2026-10-30**

`framer/` keeps the current state of the Framer project: the project map with color and text styles (`project.xml`), each page's layer XML (`pages/`), each CMS collection's items (`cms/`), and the slot map linking content keys to layers (`slots.yaml`). It is updated in the same commit as each change. Code components are mirrored when the rebuild starts porting them.

*Why:* Git history already holds every earlier state, so a diff shows exactly what changed in Framer and any node can be restored from history. Timestamped backup files would duplicate that and pile up.

### 004 · Page copy in YAML, long-form in Markdown
**2026-10-30**

Pages are YAML files keyed by section and slot. Case studies and journal articles are Markdown with frontmatter.

*Why:* Page copy is short text in fixed slots, which YAML maps cleanly to layers. Cases and articles are prose. Astro reads both formats natively, so neither needs converting at rebuild.

### 005 · Private repository
**2026-10-30**

*Why:* The repo will hold licensed font files, unpublished case material and draft copy.

### 006 · Rebuild target: Astro on Cloudflare Pages
**2026-10-17 · status: under evaluation**

Rebuild the site in Astro, deploy to Cloudflare Pages from this repository, and keep Framer live until cutover.

*Why:* Lower cost than Framer, code that is owned outright, and a build workflow that fits Claude Code. See the ARCMA Site Rebuild Launch Plan (October 17, 2026).
