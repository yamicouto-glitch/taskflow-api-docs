# TaskFlow API Documentation

Public-facing documentation for the TaskFlow API, built with [Mintlify](https://mintlify.com).

## Structure

```
├── docs.json                        # Mintlify site config & navigation
├── openapi.yaml                     # API spec (source of truth for API Reference)
├── introduction.mdx                 # What TaskFlow is, how resources relate
├── quickstart.mdx                   # First request in under 5 minutes
├── guides/
│   ├── core-workflow.mdx            # Project → task dependency & lifecycle
│   ├── task-status.mdx              # Status values, updates, common mistakes
│   └── errors.mdx                   # Every error code, cause, and fix
└── api-reference/
    ├── introduction.mdx             # Auth, base URL, endpoint summary
    ├── projects/create-project.mdx  # Auto-generated from openapi.yaml
    └── tasks/*.mdx                  # Auto-generated from openapi.yaml
```

## How to publish this (step by step)

1. **Create a GitHub repo** and push this folder's contents to it (root of the repo, not a subfolder).
2. **Sign up at [mintlify.com](https://mintlify.com)** (free plan is enough for this).
3. In the Mintlify dashboard, click **Add documentation** → **Import from GitHub** and select your repo.
4. Mintlify will detect `docs.json` automatically and deploy your site to a `*.mintlify.app` URL (or `*.mintlify.dev`, depending on current naming) within a minute or two.
5. Every push to the connected branch redeploys automatically.

### Previewing locally before you push (optional but recommended)

```bash
npm i -g mint
mint dev
```

This runs the site at `http://localhost:3000` so you can check the OpenAPI-generated pages render correctly before deploying.

## Notes on the OpenAPI-generated pages

The five files under `api-reference/` each contain only frontmatter (e.g. `openapi: "POST /projects"`). Mintlify reads `openapi.yaml` (declared in `docs.json`) and auto-generates the parameter tables, request/response schemas, and the interactive "Try it" playground for each one — so those pages don't need hand-written body content, just the routing.

## What I'd do next with more time

- Add response examples for edge cases beyond the ones in the spec (e.g. pagination behavior if the task list grows large — not currently specified).
- Add a short "Postman collection" or `.http` file as a downloadable alternative to the copy-paste cURL examples.
- Add search-friendly frontmatter (`description`) tuned per page once real usage/SEO data is available.
