# Migration Plan: Mintlify Starter → Multi-Project Hub

## Phase 1: Backup \& Preserve Starter Content

**Keep the starter examples as reference docs:**

```bash
# In your mintlify-docs repo
mkdir -p _mintlify-starter-examples
mv ai-tools _mintlify-starter-examples/
mv essentials _mintlify-starter-examples/
mv api-reference _mintlify-starter-examples/
mv development.mdx _mintlify-starter-examples/
mv quickstart.mdx _mintlify-starter-examples/
```

**Why**: The starter kit has good examples of Mintlify features you'll want to reference later.

***

### Phase 2: Create Your Project Structure

```bash
# Create directories for each project (lowercase-with-hyphens recommended)
mkdir -p virgo-core/{overview,installation,configuration}
mkdir -p supernova-microk8s-infra/{overview,deployment,troubleshooting}
mkdir -p andromeda-orchestration/{overview,playbooks,modules}
mkdir -p zammad-mcp/{overview,setup,api}

# Create shared/common docs
mkdir -p shared/{contributing,architecture,glossary}

# Keep existing useful dirs
# (images, logo, snippets stay as-is for shared assets)
```

**Final structure:**

```text
mintlify-docs/
├── docs.json                          # Main config (will update)
├── index.mdx                          # Homepage (will update)
├── favicon.svg
├── logo/
│   ├── dark.svg
│   └── light.svg
├── images/                            # Shared images
├── snippets/                          # Shared reusable snippets
├── virgo-core/
│   ├── overview.mdx
│   ├── installation.mdx
│   └── configuration.mdx
├── supernova-microk8s-infra/
│   ├── overview.mdx
│   ├── deployment.mdx
│   └── troubleshooting.mdx
├── andromeda-orchestration/
│   ├── overview.mdx
│   ├── playbooks.mdx
│   └── modules.mdx
├── zammad-mcp/
│   ├── overview.mdx
│   ├── setup.mdx
│   └── api.mdx
├── shared/
│   ├── contributing.mdx
│   ├── architecture.mdx
│   └── glossary.mdx
└── _mintlify-starter-examples/       # Reference only (not in navigation)
```

***

### Phase 3: Create Placeholder Content

**Create stub files for each project** (example for virgo-core):

**`virgo-core/overview.mdx`:**

```mdx
---
title: "Virgo Core Overview"
description: "Core infrastructure components and configuration"
---

# Virgo Core

Virgo Core is the foundational infrastructure layer for The Mothership.

## Purpose

[Describe what Virgo Core does]

## Key Features

- Feature 1
- Feature 2
- Feature 3

## Quick Links

<CardGroup cols={2}>
  <Card title="Installation" icon="download" href="/virgo-core/installation">
    Get started with Virgo Core
  </Card>
  <Card title="Configuration" icon="gear" href="/virgo-core/configuration">
    Configure your deployment
  </Card>
</CardGroup>
```

**Repeat pattern for each project** (andromeda-orchestration, supernova-microk8s-infra, zammad-mcp).

***

### Phase 4: Update `docs.json`

**Replace the entire `docs.json` with your new structure:**

```json
{
  "$schema": "https://mintlify.com/docs.json",
  "theme": "mint",
  "name": "The Mothership",
  "colors": {
    "primary": "#16A34A",
    "light": "#07C983",
    "dark": "#15803D"
  },
  "favicon": "/favicon.svg",
  "logo": {
    "light": "/logo/light.svg",
    "dark": "/logo/dark.svg"
  },
  "navigation": {
    "tabs": [
      {
        "tab": "Projects",
        "groups": [
          {
            "group": "Getting Started",
            "pages": [
              "index",
              "shared/architecture",
              "shared/contributing",
              "shared/glossary"
            ]
          },
          {
            "group": "Virgo Core",
            "pages": [
              "virgo-core/overview",
              "virgo-core/installation",
              "virgo-core/configuration"
            ]
          },
          {
            "group": "Supernova MicroK8s Infrastructure",
            "pages": [
              "supernova-microk8s-infra/overview",
              "supernova-microk8s-infra/deployment",
              "supernova-microk8s-infra/troubleshooting"
            ]
          },
          {
            "group": "Andromeda Orchestration",
            "pages": [
              "andromeda-orchestration/overview",
              "andromeda-orchestration/playbooks",
              "andromeda-orchestration/modules"
            ]
          },
          {
            "group": "Zammad MCP",
            "pages": [
              "zammad-mcp/overview",
              "zammad-mcp/setup",
              "zammad-mcp/api"
            ]
          }
        ]
      }
    ],
    "global": {
      "anchors": [
        {
          "anchor": "GitHub",
          "href": "https://github.com/basher83",
          "icon": "github"
        }
      ]
    }
  },
  "navbar": {
    "links": [
      {
        "label": "Contact",
        "href": "mailto:your-email@example.com"
      }
    ]
  },
  "contextual": {
    "options": [
      "copy",
      "view",
      "chatgpt",
      "claude",
      "perplexity",
      "mcp",
      "cursor",
      "vscode"
    ]
  },
  "footer": {
    "socials": {
      "github": "https://github.com/basher83"
    }
  }
}
```

***

### Phase 5: Update Homepage (`index.mdx`)

**Replace `index.mdx` with project-centric landing:**

```mdx
---
title: "Welcome to The Mothership"
description: "Centralized documentation for infrastructure, orchestration, and tooling"
---

# Welcome to The Mothership

The Mothership is a collection of infrastructure projects, automation tools, and MCP servers for managing DevOps workflows.

## Projects

<CardGroup cols={2}>
  <Card title="Virgo Core" icon="server" href="/virgo-core/overview">
    Core infrastructure components and base configuration
  </Card>
  <Card title="Supernova MicroK8s" icon="cube" href="/supernova-microk8s-infra/overview">
    Kubernetes infrastructure deployment and management
  </Card>
  <Card title="Andromeda Orchestration" icon="diagram-project" href="/andromeda-orchestration/overview">
    Ansible playbooks and Terraform modules for infrastructure automation
  </Card>
  <Card title="Zammad MCP" icon="headset" href="/zammad-mcp/overview">
    Model Context Protocol server for Zammad integration
  </Card>
</CardGroup>

## Quick Start

<AccordionGroup>
  <Accordion title="For DevOps Engineers">
    Start with [Andromeda Orchestration](/andromeda-orchestration/overview) to explore Ansible playbooks and Terraform modules.
  </Accordion>
  <Accordion title="For Platform Engineers">
    Check out [Supernova MicroK8s Infrastructure](/supernova-microk8s-infra/overview) for Kubernetes deployment patterns.
  </Accordion>
  <Accordion title="For AI/MCP Developers">
    Explore [Zammad MCP](/zammad-mcp/overview) for ticketing system integration.
  </Accordion>
</AccordionGroup>

## Architecture

See the [Architecture Overview](/shared/architecture) for how all projects fit together.

## Contributing

Contributions welcome! See [Contributing Guide](/shared/contributing) for details.
```

***

### Phase 6: Setup Multirepo-Action (Later)

**Once you have docs in your actual project repos**, create `.github/workflows/sync-docs.yml` in each source repo:

**Example for Virgo-Core repo:**

```yaml
name: Sync Docs to Mintlify

on:
  push:
    branches: [main]
    paths:
      - 'docs/**'
  workflow_dispatch:

jobs:
  sync-docs:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Sync to mintlify-docs repo
        uses: mintlify/multirepo-action@v1
        with:
          target-repo: basher83/mintlify-docs
          target-path: virgo-core
          source-path: docs
          github-token: ${{ secrets.MINTLIFY_SYNC_TOKEN }}
```

**You'll need to**:

1. Create a Personal Access Token (PAT) with `repo` scope
2. Add it as `MINTLIFY_SYNC_TOKEN` secret in each source repo
3. Add the action to each project repo

***

### Phase 7: Test Locally

```bash
# Start local preview server
mint dev

# Verify at http://localhost:3000:
# - All pages load without 404s
# - Navigation structure is correct
# - Icons render properly
# - No console errors
```

**Why**: Catch configuration errors before deploying to production.

***

### Phase 8: Commit \& Deploy

```bash
# Stage changes
git add .

# Commit with conventional commit style
git commit -m "feat: restructure docs for multi-project hub

- Migrate from starter template to project-specific structure
- Add Virgo Core, Supernova, Andromeda, Zammad MCP sections
- Update navigation in docs.json
- Create new homepage with project cards
- Preserve starter examples in _mintlify-starter-examples/"

# Push to GitHub
git push origin main
```

**Mintlify will auto-deploy** to `themothership.mintlify.app` when you push.

***

## Execution Checklist

- [ ] **Phase 1**: Move starter content to `_mintlify-starter-examples/`
- [ ] **Phase 2**: Create project directories (`virgo-core/`, etc.)
- [ ] **Phase 3**: Create placeholder `.mdx` files in each project dir
- [ ] **Phase 4**: Replace `docs.json` with new navigation structure
- [ ] **Phase 5**: Update `index.mdx` homepage
- [ ] **Phase 6**: (Later) Setup multirepo-action in source repos
- [ ] **Phase 7**: Test locally with `mint dev`
- [ ] **Phase 8**: Commit and push to deploy

***

## Next Steps After Migration

1. **Populate content**: Fill in actual documentation for each project
2. **Add images**: Put project-specific screenshots in `/images/[project-name]/`
3. **Create shared snippets**: Reusable code blocks in `/snippets/`
4. **Setup multirepo sync**: When ready to sync from source repos
5. **Apply for OSS program**: Get that \$30/month discount
6. **Custom domain**: Point `docs.yourdomain.com` to Mintlify

[^1]: https://github.com/basher83/mintlify-docs
