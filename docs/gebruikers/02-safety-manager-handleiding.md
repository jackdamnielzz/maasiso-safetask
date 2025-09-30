# Safety Manager handleiding

Purpose
- Short description of what this manual covers.
  This guide covers the responsibilities and workflows for Safety Managers: reviewing TRAs, approving LMRA sessions, managing hazard controls, and monitoring team compliance.

Audience
- Who should read this.
  Safety managers, quality & safety officers, and supervisors who perform safety reviews and approvals.

Prerequisites
- What must be available or configured before following this guide.
  - Safety Manager role assigned to the user.
  - Access to organization TRAs and LMRA sessions.
  - Basic knowledge of TRA/LMRA terminology and risk scoring.

Quick start / Steps
1. Step 1 — Sign in as a Safety Manager.
2. Step 2 — Open the organization's TRA templates and pending TRAs.
3. Step 3 — Review hazards and control measures; request edits or approve.
4. Step 4 — Monitor LMRA sessions and provide feedback or approvals.
5. Step 5 — Generate compliance reports and export findings.

Examples / Commands
- Web UI actions: Navigation → TRAs → Review → Approve.
- API example (pseudo):
  POST /api/tras/{traId}/approve { approverId, comment }

Links / Related
- docs/gebruikers/03-supervisor-handleiding.md: Supervisor responsibilities
- docs/backend/01-api-endpoints-guide.md: Backend endpoints for approvals
- docs/testing/04-authentication-testing.md: Test accounts and roles

TODO / Next work
- Add screenshots of TRA review workflow.
- Document risk scoring interpretation and examples.
- Add step-by-step export/report generation instructions.