# Deployment Guide

Purpose
- Short description of what this manual covers.
  Instructions for deploying the application to production and staging environments, including Vercel configuration, environment variables, and release procedures.

Audience
- Who should read this.
  DevOps engineers, maintainers, and the repository owner responsible for releases and deployments.

Prerequisites
- What must be available or configured before following this guide.
  - Vercel account connected to the repository.
  - Required environment variables set in Vercel (Firebase keys, Stripe keys, Sentry DSN).
  - Access to the project's Firebase project and service account for server-side operations.
  - CI configured (GitHub Actions) for build and test pipelines.

Quick start / Steps
1. Step 1 — Ensure all tests pass in CI (unit + e2e).
2. Step 2 — Merge feature branch to main/master and create a release PR.
3. Step 3 — Vercel will auto-deploy the preview; verify preview deployment.
4. Step 4 — After verification, promote or merge to production branch to trigger production deployment.
5. Step 5 — Post-deploy checks: health endpoint, Sentry errors, and analytics dashboards.

Examples / Commands
- Trigger local build:
  npm run build --workspace=web
- Promote a preview on Vercel: use Vercel dashboard or CLI:
  vercel --prod

Links / Related
- web/next.config.ts: Production configuration and security headers
- .github/workflows/ci.yml: CI pipeline with deployment stages
- UPTIME_MONITORING.md: Post-deploy monitoring steps
- FIREBASE_SETUP.md: Firebase deployment notes

TODO / Next work
- Add exact list of required environment variables and examples.
- Document rollback procedure for failed deployments.
- Provide a deployment checklist with owner and verification steps.