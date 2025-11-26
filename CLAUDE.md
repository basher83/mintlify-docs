# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Mintlify documentation site using MDX for content. The site configuration lives in `docs.json`.

## Development Commands

```bash
# Install Mintlify CLI (required once)
npm i -g mint

# Start local preview server at http://localhost:3000
mint dev

# Update CLI if dev environment has issues
mint update
```

## Architecture

- `docs.json` - Site configuration (name, colors, navigation, logos, footer)
- `*.mdx` files - Documentation pages using MDX (Markdown + JSX components)
- `snippets/` - Reusable content fragments imported into pages
- `api-reference/openapi.json` - OpenAPI spec for auto-generated API docs
- `images/`, `logo/` - Static assets

### Navigation Structure

Navigation is defined in `docs.json` under `navigation.tabs`. Each tab contains groups of pages. Page paths in navigation reference MDX files without the `.mdx` extension.

## Content Guidelines

### Page Structure

Every MDX page requires YAML frontmatter:

```yaml
---
title: "Page title"
description: "Page description"
---
```

### Available Components

Use Mintlify components for structured content:

- **Callouts**: `<Note>`, `<Tip>`, `<Warning>`, `<Info>`, `<Check>`
- **Code**: `<CodeGroup>` for multi-language, `<RequestExample>`/`<ResponseExample>` for APIs
- **Structure**: `<Steps>`, `<Tabs>`, `<Accordion>`, `<AccordionGroup>`
- **Cards**: `<Card>`, `<CardGroup>`, `<Columns>`
- **API docs**: `<ParamField>`, `<ResponseField>`, `<Expandable>`
- **Media**: `<Frame>` for images, `<Tooltip>`, `<Latex>`

### Writing Style (from .cursor/rules)

- Write in second person ("you"), active voice, present tense
- Lead with most important information
- Use `<Steps>` for procedures, `<Tabs>` for platform-specific content
- Wrap images in `<Frame>` components
- Include alt text for accessibility
