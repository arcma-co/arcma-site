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

### 007 · Social links: Instagram and LinkedIn only, for now
**2026-10-30**

Every social icon on the site points to ARCMA's Instagram or LinkedIn, from `content/site.yaml`. Template icons for YouTube, Facebook and Threads are hidden, not deleted (listed under `hidden` in `framer/slots.yaml`). On case study pages the Threads icon became the LinkedIn icon, so every page offers the same two.

*Why:* The template icons linked to bare youtube.com, facebook.com and threads.com. ARCMA has no channels there yet.

### 008 · No social icons on the site; email is the only contact shown
**2026-10-30 · supersedes 007**

Every social icon is hidden: the social groups on /case-studies, /journal, /about and the case study pages, and the Instagram and LinkedIn icons in the Book A Session section. The envelope icon and every email link stay. The footer's icons are hidden by hand in Framer, because the plugin can't reach the footer.

The Instagram and LinkedIn profiles stay in `content/site.yaml`. The rebuild declares them as the organization's profiles in the page metadata (`sameAs`), so search engines and AI answers still connect them to ARCMA without a visible icon.

*Why:* A single direct line reads as more premium than a row of exits. Decided by Alyssa.


### 009 · One footer site-wide: the homepage footer replaces "Get ARCMA Transmissions"
**2026-11-03**

The homepage footer (mark, "Begin the conversation →", site links, legal line on the gradient) now closes every page. On the other pages it comes from the Page Template, without the cream "Something brought you here" card: The Work and Contact already open their Book A Session section with that line, so the card would repeat it. The newsletter sign-up from the old footer moves into the new one as a row above the legal line, still posting to the HubSpot relay. The CTA line is set in Kobe caps (Body Caps), Kobe's role for structural labels. The old footer stays in the template, hidden, and its layout is in `framer/archive/`.

Requested by Alyssa as an exception to decision 002 (no new Framer layouts in stage 1).

*Why:* Two different footers made the site feel like two sites. The homepage version is quieter and leads with the conversation.
