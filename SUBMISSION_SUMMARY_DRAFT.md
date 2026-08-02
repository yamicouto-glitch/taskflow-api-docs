# Rascunho do resumo de submissão

⚠️ Isso é um ponto de partida — ajuste para refletir o que você de fato fez (se testou a API ao vivo, se usou o CLI do Mintlify localmente, quanto tempo levou, etc.). Não envie sem revisar.

---

**Process**

I started by reading the OpenAPI spec closely before writing anything, since the description flagged that most operations depend on each other — that dependency (create a project → create a task → update/delete it) turned out to be the thing worth designing the docs around, not just listing endpoints. I tested each endpoint against the live sandbox server to confirm behavior matched the spec, including the error responses for missing/invalid IDs.

I set up the Mintlify project with two tabs: a "Documentation" tab for conceptual/task-based content (Introduction, Quickstart, and three guides), and an "API Reference" tab generated from the OpenAPI spec for the endpoint-level detail. The reference pages themselves are just routing files — Mintlify auto-generates the parameter tables and interactive playground from `openapi.yaml`.

**Decisions about structure and content, and why**

- **Split conceptual docs from reference docs.** The OpenAPI spec alone tells you *what* each endpoint accepts, but not *when* to call it or *why* an operation might fail. The 404 on a missing `project_id` only makes sense once you understand the dependency chain, so I gave that its own guide (Core Workflow) rather than repeating it on every reference page.
- **A dedicated status guide.** `status` has exactly three valid values and a default that can only be set after creation (never on `POST /tasks`) — that's a common integration mistake, so it got its own short guide with a "common mistakes" section instead of being buried in the reference table.
- **A dedicated errors guide.** All errors share one response shape, so I documented the shape once and mapped every status code to its causes and fixes, rather than repeating the same explanation of `error` and `message` fields under each endpoint.
- **Quickstart uses a full working sequence, not isolated snippets.** Because most calls depend on the previous one's output, showing a create-project → create-task → update-task → list-tasks flow (with the returned IDs threaded through) is more useful than four disconnected "here's how to call this endpoint" examples.

**What I found challenging / would do differently with more time**

- The spec doesn't define behavior for pagination, filtering, or project deletion — I noted these as open questions in the docs (e.g., "no endpoint to delete a project directly") rather than guessing at behavior that isn't specified.
- With more time, I'd add a downloadable Postman collection or `.http` file alongside the copy-paste code samples, and write a couple of end-to-end tutorial pages (e.g., "build a simple CLI task tracker with TaskFlow") to show the API in a more realistic context than isolated requests.
