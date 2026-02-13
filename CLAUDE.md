# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the **Lightcraft Docs** site — technical documentation for the Lightcraft virtual production ecosystem (Jetset, Autoshot, and related workflows). Built with **Mintlify** and deployed at `https://docs.lightcraft.pro/`.

Products documented:
- **Jetset** — iOS app for virtual production and real-time compositing
- **Jetset Cine** — Advanced cinema-grade features for Jetset
- **Autoshot** — Desktop post-production tool bridging 3D tools (Blender, Unreal, After Effects, Nuke) with Jetset

## Development Commands

```bash
# Install Mintlify CLI
npm i -g mintlify

# Start local dev server (run from repo root where docs.json lives)
mintlify dev

# If dev server fails, reinstall dependencies
mintlify install
```

Deployment is automatic — pushing to the `main` branch triggers production deployment via the Mintlify GitHub App.

## Architecture

**This is a Mintlify documentation site, not a traditional code project.** There is no package.json, build system, or test suite. The entire site is defined by `.mdx` content files and a single `docs.json` configuration.

### Key Files

- **`docs.json`** — Central configuration: site metadata, color theme, navigation structure (tabs → groups → pages), navbar, footer. Page references omit the `.mdx` extension.
- **`snippets/`** — Reusable MDX components imported into pages.

### Content Organization

Content directories map to documentation sections:

| Directory | Content |
|-----------|---------|
| `equipment/` | Hardware checklists (stage, rigging, camera, iPhone) |
| `setup/` | Initial setup guides (network, iCloud, project creation) |
| `create-usd/blender/` | Blender USD/USDZ creation workflows |
| `create-usd/unreal/` | Unreal USD creation workflows |
| `autoshot/` | Autoshot application documentation |
| `jetset-cine/` | Jetset Cine features and reference |
| `compositing/` | Tracking and compositing workflows (AE, Nuke, SynthEyes) |
| `debugging/` | Troubleshooting guides |
| `editorial/avid/` | Avid editorial workflows |
| `tutorials/` | Video tutorials (subdivided by tool: blender-workflows, unreal-workflows, jetset, jetset-cine, houdini, tracking-compositing) |
| `office-hours/` | Office hours recordings organized by year |
| `images/` | All image assets, organized by category subdirectories |

### Navigation Structure (in docs.json)

Three tabs: **Docs**, **Video Tutorials**, **Office Hours**. Each tab contains groups, and each group lists page paths. When adding a new page, it must be registered in `docs.json` under the appropriate tab/group or it won't appear in navigation.

## Content Conventions

### MDX Page Structure

Every `.mdx` file starts with YAML frontmatter:

```yaml
---
title: 'Page Title'
description: 'Short description for SEO/metadata'
---
```

### Video Embeds

Tutorial pages embed Descript videos with this pattern:

```html
<iframe src="https://share.descript.com/embed/{ID}" width="640" height="360" frameborder="0" allowfullscreen></iframe>
```

Most tutorial pages follow the structure: intro text → video embed → `# Transcription` section → step-by-step content with images.

### Image References

- Store images in `/images/{category}/` matching the content directory structure
- Embed with: `<img src="/images/category/filename.png" style={{ borderRadius: '0.5rem' }} />`
- JSX-style `style` attribute (double curly braces) is required in MDX

### Mintlify Components

Available callout components: `<Tip>`, `<Note>`, `<Warning>`, `<CodeGroup>`. Use these for highlighted information blocks.

### Reusable Snippets

Import shared content from `snippets/`:
```mdx
import SnippetIntro from '/snippets/snippet-intro.mdx';
```
