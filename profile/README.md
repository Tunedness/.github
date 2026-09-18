# Tunedness

**Infrastructure for AI systems that have to run in someone else's building.**

Tunedness builds the layer underneath AI applications: the gateway that carries the
model traffic, the endpoint that serves the context, the proxy that inspects what a
tool returns, the breaker that stops a loop before it bills you for it.

Everything here is **self-hosted and open source**, and starts with one
`docker compose up`. No control plane to phone home to, no gate on the core, no lock
to a single model provider.

---

## Flagship projects

Each of these has its own organization and its own site.

### [Ragmux](https://github.com/Ragmux) · [ragmux.com](https://ragmux.com)

**Self-hosted AI gateway.** One OpenAI-compatible API in front of OpenAI, Anthropic,
Gemini, DeepSeek, Ollama and any vLLM-style server — with retrieval built in, so a
project's own documents are searched and injected before the request ever leaves your
network. Provider credentials are encrypted at rest and never reach the client. Users,
model connections, projects, documents, chunks, vectors and request logs all live in
one PostgreSQL database with pgvector: no Redis, no separate vector store.

Per-project API keys, rate limits and token budgets, request-level metrics, and an
embedded admin dashboard that is also a REST API.

`Go` · `AGPL-3.0-or-later` · [github.com/Ragmux/ragmux](https://github.com/Ragmux/ragmux)

### [Contextator](https://github.com/Contextator) · [contextator.com](https://contextator.com)

**Self-hosted, multi-tenant MCP documentation server.** Give a project its document
sources — a mounted folder, a git repository, an uploaded archive, a Notion workspace —
and it becomes its own [Model Context Protocol](https://modelcontextprotocol.io)
endpoint that Claude Code, Claude Desktop, Cursor and other agents can search
semantically. One URL per project, fully isolated: a client on `/mcp/billing` never
sees `/mcp/mobile`.

Embeddings are generated locally on the CPU by default, covering 100 languages, so
nothing has to leave the machine. Incremental indexing, accounts and roles, optional
bearer auth per endpoint. Ships as one Docker container holding both the database and
the app.

`TypeScript` · `AGPL-3.0-or-later` · [github.com/Contextator/Contextator](https://github.com/Contextator/Contextator)

---

## Also in the open

Two smaller tools, developed in this organization, that sit on the agent's tool path
rather than the model path. Both are pre-release: they run from a clone today and are
not on npm yet.

### [McpGuard](https://github.com/Tunedness/McpGuard)

**A security proxy between an AI client and its MCP servers.** It sees every tool call
and every result: scans returned content for prompt injection with a deterministic rule
engine, masks PII on the way through, applies per-tool and per-role access rules, pins
each server's tool definitions so a rug-pull cannot happen quietly, and writes every
decision to a hash-chained, tamper-evident audit log. No code change on either side —
point the client at McpGuard instead of the server.

Measured on the corpus committed to the repository: 100% catch rate in-sample at 0.0%
false positives, p95 scan latency under 20 ms up to ~64 KB, byte-identical verdicts
across platforms.

`TypeScript` · `Apache-2.0`

### [AgentFuse](https://github.com/Tunedness/AgentFuse)

**A circuit breaker for an agent's tool calls.** A transparent MCP proxy that sees every
`tools/call` and decides whether it happens: it stops semantic loops — the agent asking
the same thing over and over in slightly different words — enforces per-session budgets,
and applies per-tool allow / deny / approve rules. When something trips, the agent gets
a refusal it can read and act on instead of another wasted round trip.

Framework-agnostic on purpose: LangGraph, CrewAI, the Claude Agent SDK or a hand-rolled
loop, as long as the tools are reached over MCP. Default mode is `warn` — it observes
and reports before it breaks anything.

`TypeScript` · `Apache-2.0`

---

## How the pieces sit

```
  Model traffic                    Tool and context traffic

  your application                 your agent
        │                                │  MCP
        ▼                                ▼
  ┌───────────┐                    ┌───────────┐
  │  Ragmux   │  keys server-side, │ AgentFuse │  loops, budgets,
  │           │  RAG on the way in │           │  per-tool rules
  └───────────┘                    └───────────┘
        │                                │
        ▼                                ▼
  OpenAI · Anthropic · Gemini      ┌───────────┐
  DeepSeek · Ollama · vLLM         │ McpGuard  │  injection scan,
                                   │           │  PII mask, audit log
                                   └───────────┘
                                         │
                                         ▼
                                   MCP servers —
                                   Contextator among them
```

Each tool is useful on its own and none of them requires the others. They share
conventions, not a runtime.

---

## How we build

- **Self-hosted by default.** Your keys, your documents, your database. Where a hosted
  option exists it is a convenience, never the only path.
- **One container where one is enough.** A dependency you have to operate is part of
  the price of the tool.
- **Measured, not claimed.** Detection rates and latencies come from benchmarks
  committed to the repository, with the corpus and the caveats next to the numbers —
  including when a target was missed.
- **Observe before enforce.** Anything that can block traffic starts in a mode that
  only watches, so you can measure your own traffic before tightening.
- **No lock-in.** OpenAI-compatible surfaces, open protocols, plain PostgreSQL.

## Licensing

| Project | License |
| --- | --- |
| Ragmux, Contextator | AGPL-3.0-or-later — a commercial license is available |
| McpGuard, AgentFuse | Apache-2.0 |

## Contributing and contact

Issues, discussions and pull requests belong in the repository they are about. The
org-wide [contributing guide](https://github.com/Tunedness/.github/blob/main/CONTRIBUTING.md),
[code of conduct](https://github.com/Tunedness/.github/blob/main/CODE_OF_CONDUCT.md) and
[security policy](https://github.com/Tunedness/.github/blob/main/SECURITY.md) live in
this organization's [`.github`](https://github.com/Tunedness/.github) repository.

Please do not open a public issue for a vulnerability — the security policy explains
how to report one privately.

---

Projects under the [Tunedness](https://tunedness.com) umbrella are built by
[Muhammet Şafak](https://www.muhammetsafak.com.tr/en/).
