# Backup & Restore Guide

Purpose
- Short description of what this manual covers.
  Procedures for creating backups of Firestore and Storage, verifying backups, and restoring data safely in disaster recovery scenarios.

Audience
- Who should read this.
  System administrators, operators, and DevOps engineers responsible for backups and disaster recovery.

Prerequisites
- What must be available or configured before following this guide.
  - Access to Firebase Console and GCP project with storage buckets.
  - Service account with permissions to run exports/imports.
  - gsutil and gcloud CLI configured with appropriate IAM permissions.
  - Backup destination bucket (e.g., gs://your-backup-bucket).

Quick start / Steps
1. Step 1 — Verify backup bucket and IAM permissions are configured.
2. Step 2 — Export Firestore data to Cloud Storage:
   gcloud firestore export gs://your-backup-bucket/exports/`date +%Y%m%d`
3. Step 3 — Export Storage objects (if needed) using gsutil or lifecycle rules.
4. Step 4 — Verify backup integrity by listing export metadata and testing restore in a staging project or emulator.
5. Step 5 — To restore, use gcloud firestore import pointing to the chosen export folder.

Examples / Commands
- Export Firestore:
  gcloud firestore export gs://your-backup-bucket/exports/20250930
- Import Firestore:
  gcloud firestore import gs://your-backup-bucket/exports/20250930
- Copy storage objects:
  gsutil -m rsync -r gs://project-storage-bucket gs://your-backup-bucket/storage-backup

Links / Related
- docs/backend/03-database-management.md: Database management guide
- FIRESTORE_DATA_MODEL.md: Data model for verification after restore
- FIREBASE_EMULATOR_GUIDE.md: Use emulator to validate restores in staging

TODO / Next work
- Add automated backup cron/CI examples and retention policy.
- Document step-by-step restore checklist for production incidents.
- Include sample IAM role definitions and least-privilege recommendations.