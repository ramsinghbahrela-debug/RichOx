# RichOx AI — mandatory public release gates

Status: **BLOCKED** until all gates are tested and signed off. The Vercel informational preview is not the finance application.

## 0. Rotate credentials before deployment
An older local `.env` file was found in the owner's file library containing what appear to be real Google OAuth, Gemini, and brokerage integration credentials and an encryption key. Treat those values as exposed. Revoke/rotate them at the issuing providers, audit access where possible, and provision replacements only through Vercel/Neon secret configuration. Do not copy the old `.env` into this repository or logs. Any encrypted data depending on a rotated key needs a planned re-encryption strategy.

## 1. Source and dependency verification
- Import the complete reviewed source to a non-production branch; exclude `.env*` except `.env.example`, SQLite files, backups, uploads, financial data, tokens, and credentials.
- Scan source and Git history for secrets; resolve findings and rotate affected credentials.
- Pin and audit dependencies, build and run tests in CI.

## 2. Database migration
- Inventory all SQLite tables, queries, transactions and migration assumptions.
- Compare against Neon `richox_ai` schema before executing changes.
- Apply additive changes first to an isolated test branch; never run destructive migrations without owner approval and backup.
- Validate numeric precision, date handling, foreign keys, idempotency and rollback.

## 3. Authentication and authorization
- Implement and test Google OAuth with state/nonce, correct redirect URI, secure server-side sessions, session rotation, logout and CSRF defenses.
- Remove any implicit first-user-is-admin bootstrap from the public release.
- Enforce authenticated `user_id` scoping at every query/API boundary; deny cross-user access by default.
- Test with two separate accounts for assets, transactions, budgets, goals, email connections, exports, attachments, and background jobs.
- Encrypt third-party refresh tokens; do not log tokens or expose them to the browser.

## 4. Public launch verification
- Test signup, login, logout, account deletion, error handling, rate limiting, and data isolation end to end.
- Obtain consent and satisfy applicable Google API requirements before Gmail synchronization.
- Verify Vercel runtime compatibility and durable database/session storage.
- Deploy to a staging URL and run smoke tests before production promotion.
- Do not accept real financial records until security checks pass.
