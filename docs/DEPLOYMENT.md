# Cloudflare Pages and Neon PostgreSQL deployment guide

## Monorepo deployment design
Create four **independent Cloudflare Pages projects** with Git integration, all connected to `Nyamesem22/Datheon-FullStack-Intenship`. Do not connect this repository to Vercel.

| Pages project name (suggested) | Root directory | Build command | Output directory |
| --- | --- | --- | --- |
| datheon-portfolio | `projects/01-portfolio-website` | `npm run build` | `dist` |
| datheon-task-manager | `projects/02-task-manager` | `npm run build` | `dist` |
| datheon-weather | `projects/03-weather-dashboard` | `npm run build` | `dist` |
| datheon-ecommerce | `projects/04-ecommerce-store` | `npm run build` | `dist` |

Use Node.js 22 where supported. Each project installs and builds independently, with `package.json` in its own root.

## Branch and deployment controls
For each Cloudflare Pages project:
1. Set **Production branch = main** (not staging).
2. Under branch controls, include `staging` as a Preview branch; configure the `staging` branch alias URL (usually `staging.<project>.pages.dev`) after a successful deployment. Verify actual URLs.
3. Configure **Build watch paths** to include only that project's `projects/<name>/**` plus any future shared packages it uses, excluding unrelated app changes.
4. Configure build/deploy protections. The four GitHub Actions workflows handle independent tests and builds; Cloudflare Pages Git integration handles deployment.
5. Record verified staging and production URLs in root and per-project README files. These are intentionally not invented here.

Cloudflare docs: https://developers.cloudflare.com/pages/configuration/monorepos/ and https://developers.cloudflare.com/pages/configuration/git-integration/.

## PostgreSQL with Neon
The current apps are frontend-first starter implementations. **No live Neon database connection or data migration is performed by this setup.** Add a server-side API through Cloudflare Pages Functions as persistence features are implemented. Never place `DATABASE_URL` in Vite `VITE_*` environment variables, source control, or frontend bundles.

Recommended isolation: one logical database per app, with distinct production and staging Neon projects or Neon database branches, plus separate roles and credentials. Keep distinct Cloudflare production vs preview secrets. Never reuse a production connection string for staging.

For Cloudflare-to-Neon connections, choose **Hyperdrive** (recommended for SQL connection pooling/latency) or Neon's `@neondatabase/serverless` driver from server-side Functions. Exact bindings and drivers should be configured when server endpoints are implemented. Docs: https://developers.cloudflare.com/workers/databases/third-party-integrations/neon/ and https://developers.cloudflare.com/hyperdrive/examples/connect-to-postgres/postgres-database-providers/neon/.

### Optional database per task
- Portfolio: no DB required for static pages; Neon only if adding contact submissions, CMS, or authenticated admin.
- Task Manager: Neon for user tasks, accounts and persisted CRUD; current starter uses browser localStorage.
- Weather: Neon only for saved favorite cities, settings, or query history; live weather comes from Open-Meteo.
- E-Commerce: Neon for catalog, inventory, users, carts and orders. Current checkout is demonstration only.

### Security and release checklist
- Do not expose production database credentials to preview or client.
- Use parameterized SQL, migration files, access controls, and minimal-privilege roles.
- Plan independent database migrations for each application. Never run destructive schema migrations automatically against production.
- Separate backup and restore strategy; verify staging does not contain live customer data.
- Protect `main` and `staging` with GitHub rulesets. Note that path-filtered workflows may be skipped, so create a required aggregate gate when enforcing checks.
- Promote code only after CI and staging verification; production and staging data must remain independent.
