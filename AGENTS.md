# AGENTS.md

Rules for any AI agent working in this repository: Claude Code, Codex, or anything else. `CLAUDE.md` imports this file, so there is one rulebook.

## What this repo is

The source of truth for arcma.co: page copy, case studies, journal, design tokens and site code. Git history is the site's changelog.

Until cutover, the live site runs on Framer, and Framer is a render target. Every change lands here first and is then applied to Framer. After cutover, this repo builds and deploys the site itself.

## Ownership

- **Alyssa authors all copy.** Place it exactly as given. Never rewrite, tighten, re-punctuate or "improve" anything in `content/`. If something looks wrong (a typo, a slot that will overflow its layout, a broken link), flag it and leave the text as written.
- Agents own structure, code, design implementation and the Framer sync.
- Alyssa publishes. Agents never publish the Framer site or merge to production without her say-so.

## Layout

| Path | Holds |
|---|---|
| `content/pages/` | Page copy. One YAML file per page, keyed by section, then slot |
| `content/cases/` | Case studies. One Markdown file each |
| `content/journal/` | Journal articles. One Markdown file each |
| `framer/` | Mirror of the live Framer project: page XML, CMS items, styles, code components, and `slots.yaml`, which links each content key to its Framer layer |
| `docs/decisions.md` | Decision log. Read it before changing structure; append to it when you make a structural call |
| `CHANGELOG.md` | What went live, by publish date |

Create a directory only when it has real content. No placeholder files.

## Framer sync protocol

Framer is reached through the Framer MCP plugin ("Tommy's MCP"), which must be open in the ARCMA project in the Framer editor. The plugin can only read a page's or component's text after it has been opened in the editor that session; unopened pages come back flattened with empty text. Ask Alyssa to click through the pages you need before reading them.

`framer/slots.yaml` maps every content key to its Framer layer (`node`) and, for component properties, the property id (`field`). CMS collections map frontmatter keys to field ids the same way.

1. **Read before writing.** Fetch the target node with `getNodeXml` and compare it with its mirror in `framer/`. If they differ, someone edited in the Framer editor: commit the live state first as `sync(framer): capture editor changes`.
2. **Commit the content change** in `content/`.
3. **Apply it** with `updateXmlForNode` (or `upsertCMSItem` for CMS content). Reuse existing containers. New containers lose the template's animations.
4. **Re-read the node** and update its mirror in `framer/`, in the same commit as the content change.

The mirror replaces timestamped backups: any earlier state of a node is in git history and can be restored with `updateXmlForNode`.

Stage 1 scope is copy and CMS content only. Do not build new components or layouts in Framer; that work happens in the rebuild.

## Commits

Format: `type(scope): summary`, one logical change per commit.

| Type | For |
|---|---|
| `copy` | Page copy (`copy(home): replace hero headline`) |
| `case` | Case studies |
| `journal` | Journal articles |
| `design` | Tokens, type, layout |
| `feat`, `fix` | Site code |
| `sync` | Framer mirror updates with no content change |
| `docs`, `chore` | Everything else |

End the body with where the change stands: `Applied: Framer` or `Pending: Framer`.

## Changelog

`CHANGELOG.md` records what went live, newest first, grouped by publish date. Changes committed but not yet published sit under `Unreleased`. When Alyssa publishes, move them under the date.

## Design

- Three typefaces, three roles: Eros for display (ligatures on), Kobe for structural labels and navigation (all caps, open font style 1), Garamond for all reading text.
- Grounds alternate between obsidian, parchment and bronze. Never monolithic dark.
- Colors, type sizes and spacing come from the design tokens once they exist. No hardcoded values in components.
