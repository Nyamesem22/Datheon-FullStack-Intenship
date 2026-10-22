# Weather Dashboard

Standalone DATHEON application in the shared monorepo.

## Run locally
```bash
npm install
npm run dev
npm test
npm run build
```

## Deployment configuration
- Hosting: Cloudflare Pages (not connected yet)
- Git repository: `Nyamesem22/Datheon-FullStack-Intenship`
- Pages project root: `projects/03-weather-dashboard`
- Production branch: `main`; production URL: pending
- Staging preview branch: `staging`; staging URL: pending
- Build command: `npm run build` → output `dist`
- CI: dedicated GitHub Actions workflow

## PostgreSQL persistence
Neon PostgreSQL is the database provider for any required persistent backend features. Use only server-side Cloudflare Pages Functions or Workers and separately provisioned staging and production credentials. **No live Neon database is connected to this starter yet.**

See [Deployment guide](../../docs/DEPLOYMENT.md).
