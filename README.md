# SafeWork Pro - Implementation Kickoff (Next.js + Firebase)

This repository contains the implementation kickoff artifacts and initial instructions for starting SafeWork Pro (TRA/LMRA B2B SaaS) using the approved stack: Next.js 14 (App Router), TypeScript, Tailwind CSS, Firebase (Auth, Firestore, Storage, Cloud Functions), and Vercel.

Important docs (review before starting):
- Project memory and technical design: [`PROJECT_MEMORY_REVISED.md`](PROJECT_MEMORY_REVISED.md:1)
- Implementation checklist: [`CHECKLIST_REVISED.md`](CHECKLIST_REVISED.md:1)
- Wireframes & UX flows: [`WIREFRAMES_AND_USER_FLOWS.md`](WIREFRAMES_AND_USER_FLOWS.md:1)
- Domain reference: [`info.md`](info.md:1)

Kickoff tasks (first-code sprint)
1. Initialize Next.js app with TypeScript and Tailwind (Task 2.1, 2.2)
   - Command (local): npx create-next-app@latest ./web --typescript --eslint
   - Then: Install Tailwind, setup App Router layout, and add PWA tooling (workbox or next-pwa)
2. Create Firebase project and configure SDK for dev environment (Task 2.3)
   - Create a Firebase project, enable Auth (Email + Google), Firestore, and Storage
   - Create .env.local with firebase config keys
3. Add basic folder structure (see recommended layout in [`WIREFRAMES_AND_USER_FLOWS.md`](WIREFRAMES_AND_USER_FLOWS.md:746))
   - src/app/, src/components/, src/lib/firebase.ts, src/components/tra/TRAWizard.tsx
4. Implement authentication and tenant scaffolding (Tasks 3.1, 3.2, 3.3)
   - Integrate Firebase Auth, implement organization context provider and protected routes
5. Configure GitHub repo and Vercel integration (Task 1.4, 9.2)
   - Push initial code, set up branch protection, and connect Vercel for preview deployments

Developer conventions & tooling
- Language: TypeScript (strict mode)
- Styling: Tailwind CSS with utility-first approach
- Forms & validation: React Hook Form + Zod
- State: local component state + useSWR or React Query for data fetching; Firestore realtime listeners where needed
- Testing: Jest + React Testing Library (unit), Cypress (E2E)
- CI: GitHub Actions (build, lint, test, deploy previews to Vercel)

Important files to add early
- [`src/lib/firebase.ts`](src/lib/firebase.ts:1) - Firebase SDK initialization
- [`src/app/layout.tsx`](src/app/layout.tsx:1) - App Router root layout
- [`src/components/tra/TRAWizard.tsx`](src/components/tra/TRAWizard.tsx:1) - Start of TRA wizard
- [`.github/workflows/ci.yml`](.github/workflows/ci.yml:1) - CI pipeline skeleton
- [`.gitignore`](.gitignore:1) - Node, env, and build ignores

Environment & secrets
- Use GitHub Secrets for:
  - FIREBASE_API_KEY, FIREBASE_AUTH_DOMAIN, FIREBASE_PROJECT_ID, FIREBASE_STORAGE_BUCKET, FIREBASE_MESSAGING_SENDER_ID, FIREBASE_APP_ID
  - VERCEL_TOKEN (for CLI operations if needed)
  - STRIPE_SECRET_KEY (for paid tiers)
- Local: `.env.local` for developer keys (never commit)

Next steps I will implement now (on your approval)
- Initialize the Next.js project skeleton and add TypeScript + Tailwind configuration (Task 2.1, 2.2)
- Create `src/lib/firebase.ts` and a minimal auth/provider example (Task 3.1)
- Add `src/app/layout.tsx` and a placeholder dashboard route (Task 2.1)
- Commit and create initial GitHub repo layout; prepare Vercel preview (Task 1.4, 9.2)

If you'd like me to proceed now, approve "Start scaffolding" and I will create the initial code files and update the checklist entries for the tasks I complete.
