# Source register and verification log

All sources read on 2026-10-21 in markdown form. Re-verify per Section 2.2.

| Topic                            | URL                                                                                     |
| -------------------------------- | --------------------------------------------------------------------------------------- |
| Workers limits                   | <https://developers.cloudflare.com/workers/platform/limits/>                            |
| Workers pricing                  | <https://developers.cloudflare.com/workers/platform/pricing/>                           |
| Storage selection                | <https://developers.cloudflare.com/workers/platform/storage-options/>                   |
| Wrangler configuration           | <https://developers.cloudflare.com/workers/wrangler/configuration/>                     |
| Previews                         | <https://developers.cloudflare.com/workers/previews/>                                   |
| Previews resources and limits    | <https://developers.cloudflare.com/workers/previews/resources/>                         |
| Workflows limits                 | <https://developers.cloudflare.com/workflows/reference/limits/>                         |
| Rules of Workflows               | <https://developers.cloudflare.com/workflows/build/rules-of-workflows/>                 |
| Queues limits                    | <https://developers.cloudflare.com/queues/platform/limits/>                             |
| D1 limits                        | <https://developers.cloudflare.com/d1/platform/limits/>                                 |
| D1 Time Travel                   | <https://developers.cloudflare.com/d1/reference/time-travel/>                           |
| Durable Objects limits           | <https://developers.cloudflare.com/durable-objects/platform/limits/>                    |
| Durable Objects best practices   | <https://developers.cloudflare.com/durable-objects/best-practices/>                     |
| Agents SDK                       | <https://developers.cloudflare.com/agents/>                                             |
| MCP on Cloudflare                | <https://developers.cloudflare.com/agents/model-context-protocol/>                      |
| AI Gateway features              | <https://developers.cloudflare.com/ai-gateway/>                                         |
| Sandboxes overview               | <https://developers.cloudflare.com/sandbox/>                                            |
| Dynamic Workers                  | <https://developers.cloudflare.com/dynamic-workers/>                                    |
| Containers                       | <https://developers.cloudflare.com/containers/>                                         |
| Workers for Platforms            | <https://developers.cloudflare.com/cloudflare-for-platforms/workers-for-platforms/>     |
| Cloudflare for SaaS              | <https://developers.cloudflare.com/cloudflare-for-platforms/cloudflare-for-saas/>       |
| Secrets Store, Workers           | <https://developers.cloudflare.com/secrets-store/integrations/workers/>                 |
| Workers secrets                  | <https://developers.cloudflare.com/workers/configuration/secrets/>                      |
| Workers Logs                     | <https://developers.cloudflare.com/workers/observability/logs/workers-logs/>            |
| Tail Workers                     | <https://developers.cloudflare.com/workers/observability/logs/tail-workers/>            |
| Workers Logpush                  | <https://developers.cloudflare.com/workers/observability/logs/logpush/>                 |
| OpenTelemetry export             | <https://developers.cloudflare.com/workers/observability/exporting-opentelemetry-data/> |
| Analytics Engine                 | <https://developers.cloudflare.com/analytics/analytics-engine/>                         |
| Workers Builds                   | <https://developers.cloudflare.com/workers/ci-cd/builds/>                               |
| Versions, deployments, rollbacks | <https://developers.cloudflare.com/workers/versions-and-deployments/>                   |
| Static Assets                    | <https://developers.cloudflare.com/workers/static-assets/>                              |
| Next.js on Workers (vinext)      | <https://developers.cloudflare.com/workers/framework-guides/web-apps/nextjs/>           |
| Access                           | <https://developers.cloudflare.com/cloudflare-one/access-controls/>                     |
| Data Localization Suite          | <https://developers.cloudflare.com/data-localization/>                                  |
| Workers security model           | <https://developers.cloudflare.com/workers/reference/security-model/>                   |
| Cloudflare API limits            | <https://developers.cloudflare.com/fundamentals/api/reference/limits/>                  |
| Cloudflare skills bundle         | <https://github.com/cloudflare/skills>                                                  |
| cagent (docker-agent)            | <https://github.com/docker/docker-agent>                                                |

Added revision 3 (read 2026-10-25):

| Topic                               | URL                                                                      |
| ----------------------------------- | ------------------------------------------------------------------------ |
| shadcn registry directory           | <https://ui.shadcn.com/docs/directory>                                   |
| shadcn registry authentication      | <https://ui.shadcn.com/docs/registry/authentication>                     |
| shadcn registry namespaces          | <https://ui.shadcn.com/docs/registry/namespace>                          |
| Cloudflare Secrets Store (overview) | <https://developers.cloudflare.com/secrets-store/>                       |
| Flagship feature flags              | <https://developers.cloudflare.com/flagship/>                            |
| GitHub Actions secrets              | <https://docs.github.com/en/actions/concepts/security/secrets>           |
| Devin secrets and site cookies      | <https://docs.devin.ai/product-guides/secrets>                           |
| Devin environment best practices    | <https://docs.devin.ai/enterprise/environment-management/best-practices> |
| SOPS                                | <https://github.com/getsops/sops>                                        |
| 1Password service accounts          | <https://www.1password.dev/service-accounts>                             |

Re-verified 2026-10-26 (DEV-109 daily pass; Workers limits, Workers pricing,
D1 limits, Durable Objects limits, Queues limits, Workflows limits, Previews;
URLs unchanged from the register above). Corrections applied: D1 databases per
account is raisable by request; cheat sheet rows added for D1 2 MB row size,
Queues per account, and Workflows concurrent instances.

Re-verified 2026-10-27 (DEV-109 daily pass; AI Gateway features, unified
API, and REST API docs; Agents docs and the cloudflare/agents repo; AI
Search docs; Flagship docs and beta changelog; Browser Run rename
changelog; Dynamic Workers docs; Sandbox SDK 1.0 preview docs; Workers for
Platforms limits, bindings, and Outbound Workers docs; workers-sdk issue
13840). Corrections applied: Workflow bindings attachable in WfP
namespaces; AI Gateway dynamic routes available via the REST API; MCP
`createMcpHandler` is Streamable HTTP only (SSE deprecated); cron triggers
unsupported on WfP user Workers; Flagship marked public beta.

Re-verified 2026-10-29 (DEV-109 daily pass; Sections 4.8-4.12 plus dependent
rows: Observability pricing, Workers Logs, Workers Traces, OTel export, Tail
Workers docs, Workers Logpush pricing, WfP observability docs, Secrets Store
API scopes, D1 Time Travel and limits, Workflows pricing, limits, and the
2026-09-10 retention changelog, R2 S3 API matrix and release notes, AI Gateway
DLP, Guardrails, Unified Billing and pricing, Static Assets billing, Email
Service platform, pricing, and 2026-04-16 beta changelog, Agents email and
push docs, vinext repo, Next.js and OpenNext guides, Vinext 1.0 blog post).
Corrections applied: Workflows completed-state retention default is 7 days on
Paid for Workflows created on or after 2026-09-10 (30-day max); R2 has no
S3-style object versioning; Secrets Store scopes expanded beyond `workers`
and `ai_gateway`; Workers Logs gains the new Observability rates effective
2026-12-01; Email Sending priced and still public beta; Vinext 1.0 released
2026-09-28 and is the Cloudflare-recommended Next.js path.

Re-verified 2026-10-30 (DEV-109 daily pass; Section 1.2 second-platform
candidates: cognizant-ai-lab/neuro-san repository and releases, n8n
changelog, license FAQ, editions, and self-hosting docs, docker/compose
releases and compose-spec repository). No corrections; all three named
roles remain accurate. Decision-grade notes: Neuro-SAN is actively
maintained but still pre-1.0 (0.7.x, Apache-2.0); n8n stable is on the 2.x
line and the Sustainable Use License permits lab-built client workflows
only while clients cannot edit them (client-edited automation, embedding,
or white-label use requires a commercial license); Docker Compose is on
major version 5 (v5.6.1, 2026-10-21; the v2 line ended at 2.40.3 on
2025-10-30).

Re-verified 2026-10-31 (DEV-109 daily pass; D11, D14, D15 external anchors:
shadcn components.json, namespace, and authentication docs plus the registry
directory, getsops/sops releases, FiloSottile/age releases, ollama/ollama
releases; Secrets Store facts already covered by the 2026-10-29 pass).
Corrections applied: the source-register SOPS URL moved from the archived
age-sops/sops repo (last push 2025-01-06) to getsops/sops in this file and
CONFIG-AND-SECRETS; D11 authentication methods extended (basic auth and
query-param credentials, GitHub registries as `owner/repo` sources with `gh`
or `GH_TOKEN` for private repos) and registry items now list AI prompts.
No decision change: D11, D14, and D15 all hold. Tooling anchors: SOPS
v3.13.3 (2026-07-23, active), age v1.3.2 (2026-08-29; v1.3.0 added
post-quantum recipients), Ollama v0.40.13 (2026-10-28, very active).

Re-verified 2026-11-01 (DEV-109 daily pass; Sections 4.1-4.3, 4.7, 12, 13:
Workers limits and pricing, D1 limits and pricing, Durable Objects limits,
Queues limits, Workflows limits, KV limits, Previews, API rate limits, and
the 2026-10-30 D1 query-result-size changelog). Corrections applied: D1
databases per account is now 1,000,000 on Paid with the first 100,000
included and 0.10 per month each above (was 50,000 raisable by request);
D1 enforces a 50 MB maximum query result size from 2026-11-04; Queues per
account is a billed default (10,000, then 0.10 per month per queue, no hard
cap); cheat sheet gained the interval-dependent cron CPU row (30 s under
1-hour intervals, 15 min at 1-hour or longer). Everything else held:
Workers CPU, memory, subrequest, worker-count, worker-size, cron-count,
static-asset, wall-time, and request-body limits; Workers request, CPU,
Logs, and Logpush pricing (worked estimates match Cloudflare's published
examples); D1 size, Time Travel, query, column, parameter, statement, row,
and duration limits; Durable Object storage, class, throughput, and
WebSocket limits; Queues message, retry, batch, throughput, retention,
backlog, and consumer limits; Workflows step, payload, state, sleep,
concurrency, and creation-rate limits; Previews requirements and limits.

---
