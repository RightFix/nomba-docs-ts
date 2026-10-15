# nomba-docs-ts

Documentation site for [`nomba-ts`](../nomba-ts) — the unofficial TypeScript SDK for the Nomba payments API. Static HTML, no build step, deployed on Vercel at <https://nomba-ts.vercel.app>.

## Structure

| File | Contents |
|------|----------|
| `index.html` | Overview, install snippet, feature grid |
| `getting-started.html` | Install, async client, error handling, response shape, checkout example, validation |
| `features.html` | Pagination, card-payment flow, payment verification, webhooks, validation, reliability, concurrency |
| `resources.html` | Full API reference — every SDK method grouped by resource, with HTTP verb + path |
| `changelog.html` | Version history (mirrors SDK releases) |
| `assets/style.css`, `assets/app.js` | Shared styles and sidebar toggle |
| `robots.txt`, `sitemap.xml` | SEO plumbing for the Vercel deployment |

## Preview locally

Any static server works, e.g. from this directory:

```bash
npx serve .
# or
python3 -m http.server 8080
```

Then open `http://localhost:8080` (or `:3000` for `serve`).

## Updating the docs

The reference page is hand-maintained. When the SDK changes, keep these in sync:

1. **Method counts** — `index.html` (feature grid + intro), `resources.html` headline, and each section's `N methods` line. Count with:
   ```bash
   cd ../nomba-ts/src/resources && grep -c "  async " *.ts
   grep -c "ledger-row" ../../nomba-docs-ts/resources.html  # must match the total
   ```
2. **Sidebar version stamps** — every page has `unofficial · vX.Y.Z` in `.brand-sub`; bump together with the SDK version.
3. **`changelog.html`** — add a section per release; old entries are history, don't rewrite them.
4. **Examples** — `getting-started.html` checkout example must use valid `allowedPaymentMethods` values (`Card`, `Transfer`, …) and `features.html` must reflect current auth/retry/webhook behavior.

## Deploy

Pushing to the connected branch redeploys on Vercel automatically. `sitemap.xml` lists all five pages — add new pages there if any are created.
