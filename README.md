# DATHEON Full Stack Internship — Four Independent Applications

**Developer:** Emmanuella Adu-Boahene · **GitHub:** [Nyamesem22](https://github.com/Nyamesem22)

This monorepo contains four **standalone, independently built and deployed** DATHEON assessment projects. Each has its own package.json, application code, tests, CI workflow, and Vercel project.

| Assignment | Source | Staging | Production |
| --- | --- | --- | --- |
| Portfolio Website | [Open project](projects/01-portfolio-website) | Pending connection | Pending connection |
| Task Manager | [Open project](projects/02-task-manager) | Pending connection | Pending connection |
| Weather Dashboard | [Open project](projects/03-weather-dashboard) | Pending connection | Pending connection |
| E-Commerce Store | [Open project](projects/04-ecommerce-store) | Pending connection | Pending connection |

## Local development
Install Node.js 22+. Enter a project directory, run `npm install`, `npm run dev`, `npm test`, and `npm run build`.

## Delivery & branches
- `feature/*` → PR into `staging` for development and acceptance checks.
- `staging` → four separate Vercel **preview/staging deployments** (to configure).
- `main` → four separate Vercel **production deployments** (to configure).
- Each project has a path-filtered GitHub Actions quality workflow. Only touched projects' jobs run.
- Do not merge untested code into main. Never commit tokens or .env files.

## DATHEON assessment
Each application should be evaluated independently from the links above. Live URLs will be added when Vercel has been connected and verified. **Scaffolds are not finished assignments.**

See [deployment setup](docs/DEPLOYMENT.md).
