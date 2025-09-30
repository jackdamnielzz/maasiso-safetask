# Firebase Admin Guide

Purpose
- Short description of what this manual covers.
  Guide for backend maintainers to configure and operate the Firebase Admin SDK, service accounts, custom claims, and server-side utilities used by the project.

Audience
- Who should read this.
  Backend developers, operators, and system owners responsible for server-side integration with Firebase (Admin SDK, Cloud Functions, server processes).

Prerequisites
- What must be available or configured before following this guide.
  - Service account JSON or environment variables containing Firebase credentials.
  - Access to the Firebase Console for the project (hale-ripsaw-403915).
  - Familiarity with Node.js, TypeScript, and server-side deployment processes.
  - Installed dependencies: firebase-admin package.

Quick start / Steps
1. Step 1 — Obtain service account credentials from Firebase Console.
2. Step 2 — Store credentials securely (CI secrets, environment variables).
3. Step 3 — Initialize SDK using singleton pattern (see web/src/lib/firebase-admin.ts).
4. Step 4 — Use helper functions: setCustomClaims(), verifyIdToken(), manage users.
5. Step 5 — Deploy any server-side functions or services that require Admin SDK access.

Examples / Commands
- Initialize Admin SDK (pseudo):
  import admin from 'firebase-admin'
  admin.initializeApp({ credential: admin.credential.cert(JSON.parse(process.env.FIREBASE_SERVICE_ACCOUNT_KEY)) })

- Set custom claim example (pseudo API):
  await admin.auth().setCustomUserClaims(uid, { role: 'admin', orgId: 'org_123' })

Links / Related
- web/src/lib/firebase-admin.ts: Admin SDK helper implementation
- FIREBASE_SETUP.md: Project Firebase setup and deployment notes
- docs/backend/03-database-management.md: Database maintenance guide
- firestore.rules: Firestore security rules

TODO / Next work
- Add concrete code snippets copied from web/src/lib/firebase-admin.ts.
- Document recommended secret rotation policy and example CI/CD usage.
- Add troubleshooting section for common Admin SDK errors (permission denied, invalid credentials).