# DATHEON Full Stack Internship — Four Standalone Applications

**Developer:** Emmanuella Adu-Boahene • [GitHub profile](https://github.com/Nyamesem22)

A single assessment repository containing **four independently deployable applications**. Each application has its own source code, dependencies, tests, CI workflow, Cloudflare Pages project, and separate staging/production configuration.

| Project | Source | Staging | Production |
| --- | --- | --- | --- |
| Portfolio Website | [View source](projects/01-portfolio-website) | Pending Cloudflare setup | Pending Cloudflare setup |
| Task Manager | [View source](projects/02-task-manager) | Pending Cloudflare setup | Pending Cloudflare setup |
| Weather Dashboard | [View source](projects/03-weather-dashboard) | Pending Cloudflare setup | Pending Cloudflare setup |
| E-Commerce Store | [View source](projects/04-ecommerce-store) | Pending Cloudflare setup | Pending Cloudflare setup |

## Infrastructure
- **Hosting:** Cloudflare Pages — four separate projects linked to this monorepo.
- **Backend APIs:** Cloudflare Pages Functions, added when each feature needs server-side operations.
- **Database:** Neon PostgreSQL (server-side only; no secrets in frontend code).
- **DB environments:** Isolated development/staging and production databases, using separate Neon branches or projects for each application that requires persistence.
- **CI:** Separate path-filtered GitHub Actions tests/builds in `.github/workflows/`.
- **CD:** Cloudflare Pages Git integration per project, `main` production and `staging` preview. Configure build-watch path rules to skip unrelated projects.

## Branch policy
Develop on `feature/*` → PR into `staging` → QA → PR into `main`. `main` is not modified by setup commits until review.

## Local run
Each application: `cd projects/<folder>` then `npm install && npm run dev`; test with `npm test` and build with `npm run build`.

**Status:** Initial working scaffolds only, not completed DATHEON assignments. Hosting and Neon connections are not yet provisioned.

See [Cloudflare hosting and Neon setup](docs/DEPLOYMENT.md).
