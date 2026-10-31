# arcma.co

The source of truth for arcma.co: page copy, case studies, journal, design tokens and site code. Git history is the site's changelog.

## How it works

```
content/  ──►  Framer          the live site, until cutover
          ──►  Astro build     previewed on Cloudflare Pages, then live after cutover
```

Every change lands here first. During the Framer period, an agent applies committed changes to Framer through the Framer MCP plugin and mirrors Framer's state back into `framer/`. Edits made directly in the Framer editor are caught on the next sync and recorded as their own commits, so nothing changes on the site without a trace here.

## Making a change

Hand copy to an agent with the page and section it belongs to, or edit the file in `content/` directly on GitHub. Either way the change becomes a commit, and the commit is the record.

## Stages

1. **Framer period (now).** Copy and case studies are updated in place on the existing Framer site.
2. **Rebuild.** An Astro site is built from the same `content/` files and previewed on Cloudflare Pages while Framer stays live.
3. **Cutover.** DNS moves to Cloudflare, old URLs redirect to new ones, and Framer is retired.

Agents working here follow [`AGENTS.md`](AGENTS.md). Structural decisions and their reasons are in [`docs/decisions.md`](docs/decisions.md).
