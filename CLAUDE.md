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
| `spark/` | Spark Story introduction and quickstart |
| `tutorials/` | Video tutorials (subdivided by tool: blender-workflows, unreal-workflows, jetset, jetset-cine, houdini, tracking-compositing) |
| `images/` | All image assets, organized by category subdirectories |

### Navigation Structure (in docs.json)

Three tabs: **Docs**, **Spark Story**, and **Video Tutorials**. Each tab contains groups, and each group lists page paths. When adding a new page, it must be registered in `docs.json` under the appropriate tab/group or it won't appear in navigation.

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

## Working relationship
- You can push back on ideas-this can lead to better documentation. Cite sources and explain your reasoning when you do so
- ALWAYS ask for clarification rather than making assumptions
- NEVER lie, guess, or make up information
- If you are making an inferrance, stop and ask me for confirmation or say that you need more information

## Project context
- Format: MDX files with YAML frontmatter
- Config: docs.json for navigation, theme, settings
  - See the docs.json schema: https://www.mintlify.com/docs.json
- Components: Mintlify components

## Content strategy
- Document just enough for user success - not too much, not too little
- Prioritize accuracy and usability of information
- Make content evergreen when possible
- Search for existing information before adding new content. Avoid duplication unless it is done for a strategic reason
- Check existing patterns for consistency
- Start by making the smallest reasonable changes

## Frontmatter requirements for pages
- title: Clear, descriptive page title
- description: Concise summary for SEO/navigation

## Writing standards
- Second-person voice ("you")
- Prerequisites at start of procedural content
- Test all code examples before publishing
- Match style and formatting of existing pages
- Include both basic and advanced use cases
- Language tags on all code blocks
- Alt text on all images
- Relative paths for internal links
- Use broadly applicable examples rather than overly specific business cases
- Lead with context when helpful - explain what something is before diving into implementation details
- Use sentence case for all headings ("Getting started", not "Getting Started")
- Use sentence case for code block titles ("Expandable example", not "Expandable Example")
- Prefer active voice and direct language
- Remove unnecessary words while maintaining clarity
- Break complex instructions into clear numbered steps
- Make language more precise and contextual
- Use [Lucide](https://lucide.dev) icon library

### Language and tone standards
- Avoid promotional language. You are a technical writing assistant, not a marketer. Never use phrases like "breathtaking" or "exceptional value"
- Reduce conjunction overuse. Limit use of "moreover," "furthermore," "additionally," "on the other hand." Favor direct, clear statements
- Avoid editorializing. Remove phrases like "it's important to note," "this article will," "in conclusion," or personal interpretations
- No undue emphasis. Avoid overstating importance or significance of routine technical concepts

### Technical accuracy standards
- Verify all links. Every link, both internal and external, must be tested and functional before publication
- Maintain consistency. Use consistent terminology, formatting, and language variety throughout all documentation
- Valid technical references. Ensure all code examples, API references, and technical specifications are current and accurate

### Formatting discipline
- Purposeful formatting. Use bold, italics, and emphasis only when it serves the user's understanding, not for visual appeal
- Clean structure. Avoid excessive formatting. Never use emoji or decorative elements that don't add functional value

### Component introductions
- Start with action-oriented language: "Use [component] to..." rather than "The [component] component..."
- Be specific about what components can contain or do
- Make introductions practical and user-focused

### Property descriptions
- End all property descriptions with periods for consistency
- Be specific and helpful rather than generic
- Add scope clarification where needed (e.g., "For Font Awesome icons only:")
- Use proper technical terminology ("boolean" not "bool")

### Code examples
- Keep examples simple and practical
- Use consistent formatting and naming
- Provide clear, actionable examples rather than showing multiple options when one will do

## Content organization
- Structure content in the order users need it
- Combine related information to reduce redundancy
- Use specific links (direct to relevant pages rather than generic dashboards)
- Put most commonly needed information first

## Git workflow
- NEVER use --no-verify when committing
- Ask how to handle uncommitted changes before starting
- Create a new branch when no clear branch exists for changes
- Commit frequently throughout development
- NEVER skip or disable pre-commit hooks

## Do not
- Skip frontmatter on any MDX file
- Use absolute URLs for internal links
- Include untested code examples
- Make assumptions - always ask for clarification