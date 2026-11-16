# Media asset hosting

Shareable file host for marketing/media assets (video, image, document) that
are distributed by link instead of uploaded to each external platform.

Pattern: public R2 bucket + custom domain + Worker route that controls
response headers.

Lab implementation: `DevArtsLab/devartslab-media`, serving
`media.devartslab.com`.

## When to use

- Assets shared on external platforms by URL (docs, sites, email, social posts).
- Zero egress-fee delivery; storage billed per R2.
- Files may be public-by-link; no per-viewer authorization needed.

Not for: private assets needing expiring access (use presigned URLs), in-app
uploads needing auth (Worker binding pattern in `reference/cloudflare-catalog`),
embeddable video players (Cloudflare Stream).

## Architecture

- R2 bucket, public access on two endpoints:
  - Custom domain (production links, branded).
  - Managed `r2.dev` URL (testing, previews).
- Worker on route `<domain>/*`, R2 binding, adds headers the bucket alone
  cannot emit.
- Worker routes take precedence over the R2 custom-domain attachment on the
  same hostname.

Header contract:

- `X-Robots-Tag: noindex, nofollow` on every response.
- `Cache-Control` set by the Worker.
- GET/HEAD only; range + conditional requests pass through.
- `robots.txt` object at `Allow: /` so crawlers fetch responses and see the
  noindex header.

## Procedure

Blueprint path (governed orgs): `has_media: true` in project-blueprint
renders `media/` (wrangler.toml + gateway Worker) and
`scripts/provision-media.sh` from the org identity manifest. One command:
`bash scripts/provision-media.sh <zone-id>`.

Manual path (non-blueprint repos, external orgs): parameterize `<bucket>`,
`<domain>`, `<zone>`, `<brand>`. Lab resolution: `<brand>` and apex domain
from `registry/identity/<brand>.json` (D12 manifest); `<zone>` = zone for
that domain; names per `reference/repo-naming`. External orgs supply values
directly. Deployed values live in the instance repo's `wrangler.toml`; it is
the source for that deployment.

1. Create bucket: `wrangler r2 bucket create <bucket>`.
2. Attach domain: `wrangler r2 bucket domain add <bucket> --domain <domain>
--zone-id <zone-id>`; min TLS 1.2.
3. Enable test URL: `wrangler r2 bucket dev-url enable <bucket>`; record the
   `pub-*.r2.dev` hostname.
4. Deploy Worker: R2 binding `MEDIA`, route `<domain>/*`, vars `BRAND_NAME`;
   serve object by key, write `X-Robots-Tag`, pass `range`/`onlyIf` headers to
   `get()`. Reference implementation: `devartslab-media/src/worker.js`.
5. Upload `robots.txt`: `wrangler r2 object put <bucket>/robots.txt --remote`
   with `User-agent: *` / `Allow: /`.

## Gotchas

- `wrangler r2 object put` without `--remote` writes to local simulation
  state, not the bucket.
- Wrangler TOML: keys after `[[r2_buckets]]` belong to that table. Put
  `routes` before the binding block.
- Public-by-link means anyone with the URL can view. No directory listing; an
  object is reachable only by its key.
- Social platforms do not embed external file links as players; they show a
  link card at most. Embedding needs Cloudflare Stream or platform-native
  upload.
