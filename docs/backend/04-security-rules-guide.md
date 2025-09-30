# Security Rules Guide

Purpose
- Short description of what this manual covers.
  Overview and best practices for Firestore and Storage security rules, including examples, common pitfalls, testing, and deployment steps.

Audience
- Who should read this.
  Backend developers and security engineers responsible for writing, testing, and deploying Firebase security rules.

Prerequisites
- What must be available or configured before following this guide.
  - Familiarity with Firestore security rules language.
  - Access to `firestore.rules` and `storage.rules` files in the repository.
  - Firebase CLI installed to test and deploy rules with emulators.
  - Access to the project's Firebase Console if deploying to non-emulator environments.

Quick start / Steps
1. Step 1 — Review current rules in `firestore.rules` and `storage.rules`.
2. Step 2 — Run the Firebase emulator to test rules locally: npm run emulators
3. Step 3 — Write unit tests for rules using @firebase/rules-unit-testing or integration tests against the emulator.
4. Step 4 — Validate rule behavior with representative test users and custom claims (orgId, role).
5. Step 5 — Deploy rules to production after passing tests:
   firebase deploy --only firestore:rules,storage:rules

Examples / Commands
- Run emulators:
  npm run emulators
- Deploy rules:
  firebase deploy --only firestore:rules,storage:rules
- Example rule snippet (pseudo):
  match /organizations/{orgId}/users/{userId} {
    allow read: if request.auth != null && request.auth.token.orgId == orgId;
    allow write: if request.auth.token.role == 'admin' || request.auth.uid == userId;
  }

Links / Related
- firestore.rules: Current Firestore rules file
- storage.rules: Current Cloud Storage rules file
- docs/backend/02-firebase-admin-guide.md: Admin SDK and custom claims
- docs/testing/03-firebase-emulator-testing.md: How to test rules using emulator
- FIRESTORE_DATA_MODEL.md: Data model and collection structure

TODO / Next work
- Add concrete examples of rule unit tests and expected outcomes.
- Document common rule pitfalls and debugging steps.
- Add process for staged rollouts and monitoring rule changes.