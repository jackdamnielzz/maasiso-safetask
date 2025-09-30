# Data Manipulatie

Purpose
- Short description of what this manual covers.
  Instructions for administrators on how to safely inspect, modify, and correct organization data using admin tools, APIs, and recommended procedures.

Audience
- Who should read this.
  System administrators and operators responsible for data corrections, user imports, and emergency fixes.

Prerequisites
- What must be available or configured before following this guide.
  - Admin access with appropriate permissions.
  - Backups available before performing destructive changes.
  - Familiarity with Firestore data model: FIRESTORE_DATA_MODEL.md.
  - Access to `web/src/lib/firebase-admin.ts` helper for server-side operations.

Quick start / Steps
1. Step 1 — Export current data or verify latest backup.
2. Step 2 — Use admin UI or API to locate target documents.
3. Step 3 — Apply non-destructive updates where possible (patch).
4. Step 4 — Verify changes in a staging environment or emulator before production.
5. Step 5 — Record changes in audit logs and notify stakeholders.

Examples / Commands
- Safe update (pseudo):
  PATCH /api/organizations/{orgId}/users/{userId} { displayName, role }
- Firestore export (gcloud):
  gcloud firestore export gs://your-bucket/exports/`date +%Y%m%d`

Links / Related
- FIRESTORE_DATA_MODEL.md: Data model reference
- docs/backend/02-firebase-admin-guide.md: Firebase Admin SDK usage
- docs/admin/04-backup-restore-guide.md: Backup & restore procedures
- docs/admin/01-organisatie-beheer.md: Organization management guide

TODO / Next work
- Add concrete step-by-step examples for common tasks (change user role, merge organizations).
- Add CLI scripts and automation examples for bulk changes.
- Document audit log format and retention policy.