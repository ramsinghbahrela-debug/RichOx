# RichOx AI — Public Release Status

## Goal
Launch a secure personal-finance and personal-chief-of-staff application for individual users, with Google sign-in, optional separately consented Gmail connections, net worth, budgets, investments, goals and manual data entry.

## Environments
- GitHub: `ramsinghbahrela-debug/RichOx` (currently public; protect source and secrets).
- Neon: project `weathered-cherry-61675596`, branch `production`, database `richox_ai`.
- Vercel: `richox-public-preview` is an informational static site, **not the functional app**.
- INOROX website and the original personal RichOx local installation are outside the deployment scope.

## Release blockers
- Import and review sanitized application source without `.env`, `.env.local`, SQLite databases, OAuth refresh tokens, credentials or personal financial records.
- Port the synchronous SQLite data access and all required schema migrations to PostgreSQL; initial Neon database currently has only a subset of tables.
- Use durable server-side sessions, verify Google OAuth signup/login/logout, and enforce authorization on every financial and connected-email resource.
- Verify isolation across two test users, and verify Gmail synchronization with explicit consent and Google API compliance.
- Pass integration, security and deployment smoke tests before accepting public financial data.

Do not advertise the static preview as the live financial application.
