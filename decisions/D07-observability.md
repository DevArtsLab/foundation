# D7. Observability pipeline

Default: Workers Logs and Traces enabled on every Worker; one lab Tail
Worker attached to every Worker for the audit trail (Appendix B); Logpush to
R2 for retention beyond 7 days; Analytics Engine for metering. OTel export
is evaluated per client when they operate their own observability stack.

Coverage by platform: Workers get this pipeline. Vercel deployments rely on
platform runtime logs; no SDK. Apps on other hosts (Netlify, Fly.io, AWS,
Hugging Face, Railway) get Sentry error-only SDK: no tracing, no Replay,
DSN via secret binding, never committed. Enforcement: the project-blueprint
web scaffold ships `observability` enabled; a fleet audit flags any Worker
missing it.
