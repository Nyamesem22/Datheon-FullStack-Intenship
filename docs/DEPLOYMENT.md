# Deployment instructions

Create **four separate Vercel projects** connected to this same GitHub repository, each with its own root directory:

- Portfolio Website: `projects/01-portfolio-website`
- Task Manager: `projects/02-task-manager`
- Weather Dashboard: `projects/03-weather-dashboard`
- E-Commerce Store: `projects/04-ecommerce-store`

For each Vercel project set **Production Branch = main** and framework preset **Vite**; build command `npm run build`, output directory `dist`. Staging is a stable preview deployment of the `staging` branch: configure a branch-specific preview domain/alias within Vercel, or use a custom staging domain. The default per-commit preview URL is not stable. Add the actual verified URLs to the root README.

CI workflows run on each project's changed paths and do not deploy on their own. **Vercel's Git integration** handles actual deployment after connecting the four projects. Turn on ignored-build-step/monorepo filtering in Vercel to avoid unnecessary deployments when unrelated projects change. Verify staging environment variables are separated from production.

Protect `main` and `staging` in GitHub Settings → Rules → Rulesets, with PR requirements, no force-push/delete, and appropriate checks. A required always-running aggregate gate is recommended before enforcing path-filtered checks (otherwise unaffected required jobs may remain pending). Do not require approving your own PR if you are the only contributor and no second reviewer is available.
