# consensus-center-docs

Source for the official Consensus Center technical documentation. The site is built with [Mintlify](https://mintlify.com) — content lives in `.mdx` files and the structure is defined in `docs.json`.

Consensus Center is building a clinical infrastructure layer for preventive precision health: a deterministic, evidence-linked engine that turns biological data into traceable clinical states, with AI used for workflow and licensed clinicians making every medical decision. This repository holds the **Technical Whitepaper** — the semi-technical reference that explains that architecture to developers, clinicians, investors, and partners.

## What's documented here

- **Introduction** (`index.mdx`, `clinical-problem.mdx`) — the core thesis, what the Consensus Engine is and is not, the six design principles, and the clinical problem of preventive interpretation without over-diagnosis, bias, or unsafe automation.
- **Architecture** (`architecture/`) — the system overview and engine flow, the 67-table engine schema, runtime facts and decision traceability, and the technology stack and dependencies.
- **Clinical methodology** (`clinical/`) — the calibration methodology, ancestry/genotype/phenotype and context inputs, clinical guardrails and engine states, and evidence management and scientific defensibility.
- **Governance & safety** (`governance/`) — physician-in-the-loop governance, validation strategy, AI-agent architecture, treatment and protocol governance beyond GLP-1, security and data governance, the operating model, and release/deployment/rollback.
- **For stakeholders** (`stakeholders/`) — due diligence readiness and the final synthesis of the technical thesis.

## How the repo is organized

The site is content-first: each section of the whitepaper is a top-level directory of `.mdx` pages, and `docs.json` is the single source of truth that wires those pages into the sidebar groups, theme, colors, and metadata. Adding a page means dropping an `.mdx` file into the relevant directory and registering its path under `navigation.groups` in `docs.json` — nothing else routes content.

A few supporting conventions sit alongside the content directories:

- **Branding and styling** (logo, favicon, theme colors, fonts) are configured in `docs.json` and the `logo/` and `images/` directories, layered on top of the default Mintlify theme.
- **Excluded files** are listed in `.mintignore`, so non-published assets are kept out of the build.
- **AI authoring support** — a bundled Mintlify skill under `.claude/skills/` provides component reference, writing standards, and workflow guidance for AI coding tools.
- **Quality gates** — build validation (`mint validate`) and broken-link detection (`mint broken-links`) run against the whole tree, so new content is checked the same way as existing content.

Every page carries `title`, `description`, and `keywords` frontmatter, uses sentence-case headings, and favors built-in Mintlify components (callouts, cards, steps, tabs, accordions, tables) over raw markup.

## Local development

Requires Node `>=18.17` and the [Mintlify CLI](https://www.npmjs.com/package/mint). From the repo root (where `docs.json` lives):

```sh
npm i -g mint
mint dev          # start the dev server at http://localhost:3000
```

Other useful commands:

```sh
mint validate     # validate that the docs build cleanly
mint broken-links # detect broken internal links
mint update       # update the CLI if the dev server won't start
```

## Contributing

- Edit or add `.mdx` pages, then register them under `navigation.groups` in `docs.json` so they appear in the sidebar.
- Keep clinical claims accurate and cautious: preserve the whitepaper's boundaries (decision support, not autonomous diagnosis or prescribing) and leave any unverified item marked with a `{/* TODO */}` comment rather than presenting it as fact.
- Run `mint validate` and `mint broken-links` before opening a PR.
- Open a PR against `main`; the docs deploy from there automatically once the [Mintlify GitHub app](https://dashboard.mintlify.com/settings/organization/github-app) is connected.
