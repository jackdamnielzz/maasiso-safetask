# Database Management

Purpose
- Short description of what this manual covers.
  Guidance for managing Firestore data, backups, index management, migrations, and maintenance tasks for the project's database.

Audience
- Who should read this.
  Backend engineers, DBAs, and administrators responsible for data integrity, migrations, and backups.

Prerequisites
- What must be available or configured before following this guide.
  - Access to Firebase Console and appropriate IAM permissions.
  - Service account credentials for automated backups.
  - Familiarity with Firestore data model and indexes (see FIRESTORE_DATA_MODEL.md).

Quick start / Steps
1. Step 1 — Review current data model: FIRESTORE_DATA_MODEL.md.
2. Step 2 — Create/modify composite indexes via firestore.indexes.json and deploy.
3. Step 3 — Perform exports for backups using gcloud or Firebase CLI.
4. Step 4 — Plan and apply migrations via Cloud Functions or controlled scripts.
5. Step 5 — Monitor database usage and optimize queries/indexes.

Examples / Commands
- Export Firestore data (gcloud):
  gcloud firestore export gs://your-bucket/exports/`date +%Y%m%d`
- Deploy indexes:
  firebase deploy --only firestore:indexes

Links / Related
- FIRESTORE_DATA_MODEL.md: Data model reference
- firestore.indexes.json: Index definitions
- docs/backend/04-security-rules-guide.md: Security rules and access controls
- docs/admin/03-data-manipulatie.md: Admin data manipulation procedures

TODO / Next work
- Add migration script templates and examples.
- Document retention policy and restore procedures with examples.
- Add step-by-step recovery checklist for disaster scenarios.