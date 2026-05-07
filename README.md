

### AppCompiler — Natural Language → Executable App Schema

> **AI Platform Engineer Internship Demo** · Multi-stage pipeline that converts plain English app descriptions into validated, executable JSON configurations.

🔗 **Live Demo**: [your-username.github.io/appcompiler](https://your-username.github.io/appcompiler)

---

## What it does

AppCompiler is a **compiler for software generation**. It takes a natural language description like:

> *"Build a CRM with login, contacts dashboard, role-based access (admin/sales/viewer), premium plan with Stripe payments. Admins see analytics."*

...and produces a complete, validated, executable configuration covering:
- **UI schema** — pages, components, layouts, field bindings
- **API schema** — endpoints, methods, auth, request/response bodies
- **Database schema** — tables, columns, FK relations, indexes
- **Auth config** — roles, permissions, JWT config, route guards
- **Business logic** — event-driven rules, premium gating, role access

---

## Architecture: 4-Stage Pipeline

```
Natural Language
      │
      ▼
┌─────────────────────┐
│  Stage 1            │  Intent Extraction
│  Intent Extractor   │  NL → entities, roles, flows, features, ambiguities
└──────────┬──────────┘
           │ structured intent JSON
           ▼
┌─────────────────────┐
│  Stage 2            │  System Design
│  System Designer    │  Intent → pages, API groups, DB tables, auth strategy
└──────────┬──────────┘
           │ architecture blueprint JSON
           ▼
┌─────────────────────┐
│  Stage 3            │  Schema Generation
│  Schema Generator   │  Full ui_config + api_config + db_schema + auth_config
└──────────┬──────────┘
           │ complete schema JSON
           ▼
┌─────────────────────┐
│  Stage 4            │  Validation & Repair Engine ← most important
│  Validator          │  Cross-layer consistency · auto-repair · exec readiness
└──────────┬──────────┘
           │
           ▼
   Validated Executable
       Schema JSON
```

### Why multi-stage (not a single prompt)?

A single prompt produces unstructured, inconsistent output that can't be trusted. This pipeline:

1. **Stage 1** acts as the **lexer/parser** — extracts structured intent, flags ambiguities rather than hallucinating
2. **Stage 2** acts as the **AST builder** — constructs a proper architecture that each subsequent stage can reference
3. **Stage 3** acts as the **code generator** — each output section (ui_config, api_config, db_schema) is generated with access to the architecture, so cross-references exist
4. **Stage 4** acts as the **linker/verifier** — checks that API endpoints reference real DB tables, UI fields bind to real API endpoints, auth roles are consistent everywhere

This mirrors how a real compiler works (lex → parse → IR → optimize → link).

---

## Validation & Repair Engine

The most important part. Stage 4 checks:

| Check | What it verifies |
|-------|-----------------|
| `ui_to_api` | Every UI field's `api_binding` maps to a real endpoint in `api_config` |
| `api_to_db` | Every endpoint's `db_operations` reference real tables in `db_schema` |
| `auth_consistency` | Roles in `ui_config.guards`, `api_config.roles`, and `auth_config.roles` are consistent |
| `business_logic` | Business logic rules reference valid tables and endpoints |

When issues are found, they are **auto-repaired where possible** — not a brute-force full retry. Each repair is logged with the specific action taken and the layer it affected.

Output includes:
- `consistency_score` (0–1)
- `issues[]` with severity (error/warning/info) + layer + auto_repaired flag
- `repairs_made[]` with specific action taken
- `execution_readiness.score` + `ready_to_deploy` boolean

---

## Schema Contract

The final output is a strict JSON contract:

```json
{
  "metadata": { "version": "1.0", "app_name": "...", "generated_at": "..." },
  "ui_config": {
    "pages": [{
      "id": "...", "route": "...", "guards": ["..."],
      "sections": [{
        "fields": [{ "id": "...", "api_binding": "POST /api/v1/contacts" }]
      }]
    }]
  },
  "api_config": {
    "endpoints": [{
      "id": "...", "method": "POST", "path": "/api/v1/contacts",
      "db_operations": [{ "table": "contacts", "operation": "INSERT" }]
    }]
  },
  "db_schema": {
    "tables": [{ "name": "contacts", "columns": [...] }]
  },
  "auth_config": {
    "roles": [{ "name": "admin", "permissions": ["contacts:read", "contacts:write"] }],
    "guards": [{ "route": "/admin/*", "required_roles": ["admin"] }]
  },
  "business_logic": [...]
}
```

---

## Tech Stack

- **Frontend**: Vanilla HTML/CSS/JS — single file, zero dependencies, deployable anywhere
- **AI**: Anthropic Claude (claude-sonnet-4) via `/v1/messages` API with streaming
- **Pipeline**: 4 sequential stages with structured prompts and JSON schema enforcement
- **Validation**: Custom cross-layer consistency engine in Stage 4

---

## Running locally

1. Clone the repo
2. Open `index.html` in a browser
3. Enter your Anthropic API key (stored in localStorage)
4. Enter an app description and hit Compile

No build step. No server. No dependencies.

---

## Deployment (GitHub Pages)

1. Push `index.html` to a GitHub repo
2. Go to Settings → Pages → Deploy from main branch
3. Your live URL: `https://your-username.github.io/repo-name`

---

## Evaluation Framework

The app includes a built-in eval tab showing:

| Metric | Description |
|--------|-------------|
| Total latency | End-to-end pipeline time |
| Per-stage latency | Breakdown with visual bar chart |
| Consistency score | Cross-layer validation score (0–100%) |
| Output complexity | Entity count, endpoint count, table count, etc. |
| Issues found / repaired | Count + auto-repair rate |
| Deployment readiness | Boolean + blockers list |
| Assumptions made | What the compiler inferred from vague input |
| Ambiguities flagged | What the compiler couldn't resolve without clarification |

---

## Failure Handling

| Input type | Behavior |
|------------|----------|
| Vague prompt | Stage 1 extracts what it can, populates `ambiguities[]` with unclear requirements |
| Conflicting requirements | Stage 4 flags as `error` severity issues, attempts repair |
| Missing info | Stage 1 makes reasonable assumptions, documents them in `assumptions[]` |
| Invalid JSON from API | Extraction attempts JSON recovery from partial response; fails gracefully with error message |

---

## Cost vs Quality Tradeoff

| Model | Latency | Cost/run | Output quality |
|-------|---------|----------|----------------|
| claude-haiku-4 | ~8s | ~$0.002 | Good for simple apps |
| **claude-sonnet-4** | ~25s | ~$0.04 | Best balance (current) |
| claude-opus-4 | ~60s | ~$0.20 | Marginal gain for most inputs |

The 4-stage pipeline adds latency vs a single prompt but delivers significantly better cross-layer consistency because each stage can reference prior structured output rather than hallucinating it.

---

## License

MIT
