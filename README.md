# Vertra Cloud Docs

Official documentation for [Vertra Cloud](https://vertracloud.app), a Brazilian application hosting
platform (PaaS): deploy from GitHub or a zip file, isolated containers, managed databases, file
storage, snapshots, a CLI and a VS Code extension. Discord, WhatsApp and Telegram bots are
first-class workloads.

Published at [docs.vertracloud.app](https://docs.vertracloud.app) (Mintlify). The documentation is written in English.

## Structure

```
docs/
├── introduction.mdx        # Platform introduction
├── overview.mdx            # Feature overview
├── plans-and-limits.mdx    # Plans and limits — public mirror of the knowledge base
├── how-to-host.mdx         # Deploy guide (zip)
├── configuration.mdx       # App configuration file and limits
├── deploy-github.mdx       # Deploy from GitHub
├── github-actions.mdx      # Deploy with GitHub Actions
├── applications.mdx        # Applications
├── databases.mdx           # Databases
├── sites.mdx               # Static sites
├── workspaces.mdx          # Workspaces and teams
├── plan-downgrade.mdx      # Plan downgrade
├── cli.mdx                 # CLI
├── sdks.mdx                # JavaScript, Python and Go SDKs
├── mcp.mdx                 # MCP server for AI agents
├── vscode-extension.mdx    # VS Code extension
├── common-errors.mdx       # Common errors and fixes
├── changelog.mdx           # Changelog (index)
├── changelog/              # Changelog entries, dated by delivery
├── guides/                 # Guides (the "Guides" tab in docs.json)
├── tutorials/              # Tutorials by language
├── api-reference/          # REST API reference (errors.mdx: full error catalog)
└── knowledge-base.mdx      # Public knowledge base (/knowledge-base route)
```

## Two rules that break the docs if ignored

- **`plans-and-limits.mdx` mirrors `knowledge-base.mdx`.** If a product number changes in the
  knowledge base, update that page in the same change.
- **A page missing from `docs.json` has no URL.** Mintlify only builds routes for pages listed in
  `navigation`, so an orphan `.mdx` file is invisible to users and crawlers.
