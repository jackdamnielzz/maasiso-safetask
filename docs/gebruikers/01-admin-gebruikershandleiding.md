# Admin gebruikershandleiding

Purpose
- Short description of what this manual covers.
  This guide provides administrators with step-by-step instructions to manage organizations, users, roles, and high-level system settings in the application.

Audience
- Who should read this.
  System administrators and owners responsible for onboarding organizations, assigning roles, and performing administrative tasks.

Prerequisites
- What must be available or configured before following this guide.
  - Access to an administrator account with the proper permissions.
  - Organization created in the system (or permission to create one).
  - Basic familiarity with project terminology (organizations, roles, TRAs, LMRA).

Quick start / Steps
1. Step 1 — Sign in with an administrator account.
2. Step 2 — Navigate to Settings → Organizations.
3. Step 3 — Create or select an organization.
4. Step 4 — Add users and assign roles (admin, safety_manager, supervisor, field_worker).
5. Step 5 — Configure organization-level settings and integrations.

Examples / Commands
- Use the web UI: open Settings → Users → Invite user.
- API example (pseudo):
  POST /api/organizations/{orgId}/users { email, role }

Links / Related
- docs/admin/02-gebruiker-beheer.md: User management guide
- docs/backend/01-api-endpoints-guide.md: API reference for admin endpoints
- ../README.md: Documentation index

TODO / Next work
- Fill in screenshots for each step.
- Add exact API request/response examples.
- Document permission matrix per role.
- Provide troubleshooting section for common admin errors.