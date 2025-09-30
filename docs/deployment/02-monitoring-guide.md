# Monitoring Guide

Purpose
- Short description of what this manual covers.
  Guide for setting up monitoring and alerting for the application (Sentry, Vercel Analytics, Uptime checks, and logs).

Audience
- Who should read this.
  DevOps engineers, maintainers, and on-call personnel responsible for observing production health.

Prerequisites
- What must be available or configured before following this guide.
  - Sentry account and DSN for the project.
  - Vercel project access and analytics enabled.
  - Uptime monitoring service account or configuration (UptimeRobot, Pingdom).
  - Access to logs (Vercel, Firebase, or external log aggregator).

Quick start / Steps
1. Step 1 — Configure Sentry DSN and integrate with client/server instrumentation (see web/src/instrumentation.ts).
2. Step 2 — Enable Vercel Analytics and review Core Web Vitals dashboards.
3. Step 3 — Configure uptime checks for homepage and health endpoints.
4. Step 4 — Set up alerting rules in Sentry and Uptime service for critical errors and downtime.
5. Step 5 — Create runbooks for common incidents and assign on-call rotations.

Examples / Commands
- Example Sentry environment variable:
  SENTRY_DSN=https://examplePublicKey@o0.ingest.sentry.io/0
- Health check endpoint to monitor:
  GET /api/health

Links / Related
- UPTIME_MONITORING.md: Existing uptime monitoring notes
- web/src/instrumentation.ts: Sentry instrumentation
- docs/deployment/01-deployment-guide.md: Deployment and post-deploy checks

TODO / Next work
- Add alert severity matrix and escalation policies.
- Provide concrete examples of Sentry alert rules and thresholds.
- Document log retention and aggregation strategy.