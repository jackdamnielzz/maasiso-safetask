# Supervisor handleiding

Purpose
- Short description of what this manual covers.
  Guide for supervisors on coordinating field teams, approving work, assigning TRAs, and reviewing LMRA sessions on a day-to-day basis.

Audience
- Who should read this.
  Supervisors and team leads responsible for day-to-day task assignments and immediate safety oversight.

Prerequisites
- What must be available or configured before following this guide.
  - Supervisor role assigned.
  - Teams and field workers created in the organization.
  - Access to TRA templates and assigned projects.

Quick start / Steps
1. Step 1 — Sign in as a Supervisor.
2. Step 2 — View assigned projects and team members.
3. Step 3 — Assign TRAs or LMRA tasks to field workers.
4. Step 4 — Review completed LMRA sessions and provide feedback.
5. Step 5 — Escalate unsafe conditions to Safety Manager or Admin.

Examples / Commands
- Web UI actions: Dashboard → Teams → Assign task → Monitor.
- API example (pseudo):
  POST /api/projects/{projectId}/assign { workerId, traId }

Links / Related
- docs/gebruikers/04-field-worker-handleiding.md: Field worker guide
- docs/gebruikers/02-safety-manager-handleiding.md: Safety manager responsibilities
- docs/admin/02-gebruiker-beheer.md: User/role management

TODO / Next work
- Add screenshots for assignment flows.
- Document escalation procedures and templates.
- Include examples of daily checklists and common actions.