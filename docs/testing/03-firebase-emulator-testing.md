# Firebase Emulator Testing

Purpose
- Short description of what this manual covers.
  How to use the Firebase Emulator Suite for local development and testing of Authentication, Firestore, and Storage interactions without touching production infrastructure.

Audience
- Who should read this.
  Developers, QA engineers, and contributors writing integration or end-to-end tests that interact with Firebase services.

Prerequisites
- What must be available or configured before following this guide.
  - Node.js and project dependencies installed (run npm install).
  - Firebase CLI installed (firebase-tools).
  - Project configured with emulator ports as in [`firebase.json`](firebase.json:1).
  - Project uses the emulator helper in `web/src/lib/firebase-emulator.ts` for local connections.

Quick start / Steps
1. Step 1 — Install dependencies (if not already): npm install
2. Step 2 — Start emulators: npm run emulators
3. Step 3 — Run unit/integration tests with emulators: npm run test:emulated
4. Step 4 — Run Cypress E2E tests against emulators: npm run emulators:e2e
5. Step 5 — Stop emulators when done: npm run emulators:kill

Examples / Commands
- Start emulators locally:
  npm run emulators
- Run Jest with emulator mode:
  npm run test:emulated
- Run Cypress E2E tests against emulator:
  npm run emulators:e2e

Links / Related
- [`FIREBASE_EMULATOR_GUIDE.md`](FIREBASE_EMULATOR_GUIDE.md:1) - Extended guide and troubleshooting
- [`web/src/lib/firebase-emulator.ts`](web/src/lib/firebase-emulator.ts:1) - Emulator helper code
- [`docs/testing/02-e2e-testing-guide.md`](docs/testing/02-e2e-testing-guide.md:1) - E2E testing guide

TODO / Next work
- Add detailed examples for seeding emulator data and clearing emulator state.
- Include common emulator error messages and fixes.
- Document CI usage patterns for emulator-backed tests.