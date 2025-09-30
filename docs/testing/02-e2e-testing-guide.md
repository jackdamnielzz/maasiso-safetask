# End-to-end (E2E) Testing Guide

Purpose
- Short description of what this manual covers.
  Guide to writing, running, and organizing end-to-end tests using Cypress for critical user journeys, including CI integration and best practices.

Audience
- Who should read this.
  Developers, QA engineers, and maintainers responsible for E2E coverage and CI pipelines.

Prerequisites
- What must be available or configured before following this guide.
  - Node.js and project dependencies installed.
  - Cypress installed (see web/package.json).
  - Firebase emulator running for tests that require backend services (recommended).
  - Access to CI (GitHub Actions) to run tests in pipeline.

Quick start / Steps
1. Step 1 — Start the Firebase emulator (if required): npm run emulators
2. Step 2 — Run Cypress in headed mode for local debugging: npm run cypress:open
3. Step 3 — Run Cypress headless for CI: npm run cypress:run
4. Step 4 — Review test recordings, artifacts, and coverage reports.

Examples / Commands
- Open Cypress test runner:
  npm run cypress:open
- Run headless tests (CI):
  npm run cypress:run -- --browser chrome

Links / Related
- docs/testing/01-unit-testing-guide.md: Unit testing guide
- docs/testing/03-firebase-emulator-testing.md: Firebase emulator testing guide
- web/cypress.config.ts: Cypress configuration file
- .github/workflows/ci.yml: CI pipeline with E2E stages

TODO / Next work
- Add sample tests for core TRA/LMRA flows.
- Document test data seeding and fixture management strategies.
- Add guidance for visual/regression testing and flakiness mitigation.