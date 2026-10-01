# Event Studio

Private local implementation of the canonical Notion build pack v2 (1 October 2026). Source copies are in `docs/spec/00.md` through `13.md`. This is under active development; consult `docs/IMPLEMENTATION_STATUS.md` for accurate completion states.

## Local setup

Node 22.23.3, pnpm 9.15.9 and Docker are required. Nothing in this repository deploys publicly by default. Use synthetic images only.

```bash
cp .env.example .env
pnpm install --frozen-lockfile
docker compose up -d postgres redis objectstore mailpit
pnpm db:migrate
pnpm db:seed
pnpm dev
pnpm worker
```

Web: http://127.0.0.1:3100. Mailpit and storage ports are described in compose.yaml. Seeded credentials are generated uniquely into ignored `.local/demo-accounts.json`; never use these in production. Staff email verification and recent TOTP MFA are enforced server side. Production activation remains blocked by approved model, privacy, retention, seller, payment, messaging and infrastructure gates.

Run `pnpm lint`, `pnpm typecheck`, `pnpm test`, `pnpm test:integration`, `pnpm test:security`, `pnpm test:e2e`, `pnpm build`, `pnpm doctor` and `pnpm models:verify`. Model verification is expected to fail while official artifact hashes and approvals are missing. This must never silently enable mock recognition in production.

See module status files and release evidence for actual executed versus unrun checks. No legal compliance, real recognition accuracy, live payment or deployment success is claimed by a local test run.
