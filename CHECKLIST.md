# SafeWork Pro - Development Checklist (Strategic Review Implementation)

**Project**: SafeWork Pro - Next.js + Firebase + Vercel Stack  
**Developer**: Solo Full-Stack Developer  
**Timeline**: 6-8 months (with parallel work streams)  
**Stack**: Next.js 14, Firebase, Vercel, TypeScript  
**Budget**: ~€275/month operating costs (infrastructure + tools)  
**Version**: 2.0 (Strategic Review Implementation)  
**Last Updated**: September 29, 2025 22:17 UTC

**KEY CHANGES FROM ORIGINAL:**
- Added 29 new strategic tasks identified in strategic review
- Reorganized tasks by priority and parallel work streams
- Moved testing infrastructure to Month 2 (from Month 4)
- Added market validation phase (highest priority)
- New categories: Market Validation, API Architecture, Demo Environment, Search, Analytics
- Total tasks: 83 (54 original + 29 new)

---

## PHASE 0: Market Validation (Weeks 1-3) - CRITICAL PRIORITY

**STATUS: ⏸️ PAUSED - Business Activities**
These tasks require human interaction (interviews, partner recruitment, market research) and will be completed by the user separately from development work. Development continues with technical tasks.

**Timeline**: Weeks 1-3 (BEFORE continuing development)
**Rationale**: Prevent building wrong features, validate product-market fit

### Market Research & Customer Validation
- [⏸] **Task 1.4A**: Conduct 15+ customer interviews with safety managers
  - **Completion Criteria**: Interviewed 15+ prospects from construction/industrial sectors, documented insights
  - **Dependencies**: None - START IMMEDIATELY
  - **Time Estimate**: 2 weeks
  - **Phase**: Market Validation (Weeks 1-2)
  - **Questions to Ask**:
    - Current TRA/LMRA workflow and pain points
    - Willingness to pay for digital solution
    - Must-have vs nice-to-have features
    - Mobile requirements for field workers
    - Integration needs with existing systems
  - **Success Criteria**: Clear understanding of customer needs, pricing validation, feature priorities

- [⏸] **Task 1.4B**: Validate pricing strategy with target customers
  - **Completion Criteria**: Tested €50/€150 pricing with 10+ prospects, confirmed willingness-to-pay
  - **Dependencies**: Task 1.4A (interview insights)
  - **Time Estimate**: 3 days
  - **Phase**: Market Validation (Week 2)
  - **Validation Methods**:
    - Van Westendorp Price Sensitivity Meter
    - Competitive pricing comparison
    - Value-based pricing discussions
  - **Success Criteria**: Confirmed pricing tiers are acceptable, identified optimal price points

- [⏸] **Task 1.4C**: Perform MoSCoW analysis and prioritize MVP features
  - **Completion Criteria**: Complete MVP_SCOPE.md with Must/Should/Could/Won't categorization
  - **Dependencies**: Task 1.4A, Task 1.4B
  - **Time Estimate**: 2 days
  - **Phase**: Market Validation (Week 2)
  - **Deliverable**: MVP_SCOPE.md document
  - **Success Criteria**: Clear MVP scope, deferred nice-to-have features

- [⏸] **Task 1.4D**: Identify and onboard 3-5 design partners for early access
  - **Completion Criteria**: Signed agreements with 3-5 companies for beta testing
  - **Dependencies**: Task 1.4C (MVP scope defined)
  - **Time Estimate**: 1 week
  - **Phase**: Market Validation (Week 3)
  - **Partner Criteria**:
    - Active TRA/LMRA users
    - Willing to provide weekly feedback
    - Representative of target market
  - **Success Criteria**: Committed design partners, feedback schedule established

- [⏸] **Task 1.4E**: Document market research findings in MARKET_RESEARCH.md
  - **Completion Criteria**: Complete documentation of all interviews, insights, and validated assumptions
  - **Dependencies**: Task 1.4A, Task 1.4B, Task 1.4C
  - **Time Estimate**: 2 days
  - **Phase**: Market Validation (Week 3)
  - **Deliverable**: MARKET_RESEARCH.md document
  - **Success Criteria**: Comprehensive market research documentation for future reference

---

## 1. Foundation & Planning (8 tasks) - Months 1-2

### Business & Legal Foundation
- [⏸] **Task 1.1**: Register domain and set up basic business structure
  - **Completion Criteria**: Domain purchased, basic legal entity established, payment processing ready
  - **Dependencies**: None
  - **Time Estimate**: 1 week
  - **Phase**: Foundation (Month 1)

- [⏸] **Task 1.2**: Research and validate target market with potential customers
  - **Completion Criteria**: 10+ customer interviews, pricing validation, feature priority feedback
  - **Dependencies**: Task 1.1
  - **Time Estimate**: 2 weeks
  - **Phase**: Foundation (Month 1)
  - **NOTE**: This task is MERGED with Tasks 1.4A-1.4E above for comprehensive market validation

- [x] **Task 1.3**: Create detailed feature requirements based on TRA/LMRA domain knowledge
  - **Completion Criteria**: Feature specification document, user stories, acceptance criteria
  - **Dependencies**: Task 1.2, info.md analysis
  - **Time Estimate**: 1 week
  - **Phase**: Foundation (Month 1)
  - **Completed**: 2025-09-29
  - **Deliverable**: FEATURE_REQUIREMENTS.md (2245 lines, 13 major feature epics, 80+ user stories)

### Technical Planning
- [x] **Task 1.4**: Set up development accounts and services
  - **Completion Criteria**: Firebase project, Vercel account, GitHub repository, Stripe account
  - **Dependencies**: Task 1.1
  - **Time Estimate**: 2 days
  - **Phase**: Foundation (Month 1)
  - **Completed**: 2025-09-29
  - **Notes**:
    - GitHub repo: git@github.com:jackdamnielzz/maasiso-safetask.git
    - Firebase: Already configured (hale-ripsaw-403915)
    - Vercel: Connected via GitHub, auto-deploys enabled
    - Stripe: Test keys ready for integration (Task 7.1)
    - Created SETUP_ACCOUNTS.md with detailed instructions

- [ ] **Task 1.5**: Design Firestore data model for multi-tenant TRA/LMRA system
  - **Completion Criteria**: Complete Firestore schema, security rules drafted, relationship diagram
  - **Dependencies**: Task 1.3
  - **Time Estimate**: 4 days
  - **Phase**: Foundation (Month 1)

- [ ] **Task 1.6**: Plan component architecture and folder structure
  - **Completion Criteria**: Component hierarchy designed, reusable component list, file structure planned
  - **Dependencies**: Task 1.3
  - **Time Estimate**: 2 days
  - **Phase**: Foundation (Month 1)

### Design & UX Planning  
- [ ] **Task 1.7**: Create design system and UI component specifications
  - **Completion Criteria**: Color palette, typography, component designs, responsive breakpoints
  - **Dependencies**: Task 1.3
  - **Time Estimate**: 1 week
  - **Phase**: Foundation (Month 1)

- [ ] **Task 1.8**: Plan mobile PWA requirements and offline strategy
  - **Completion Criteria**: PWA manifest, service worker strategy, offline data sync plan
  - **Dependencies**: Task 1.5
  - **Time Estimate**: 3 days
  - **Phase**: Foundation (Month 1)

---

## 2. Development Environment & Infrastructure (10 tasks) - Month 1-2

### Next.js Application Setup
- [x] **Task 2.1**: Initialize Next.js 14 project with TypeScript and essential dependencies
  - **Completion Criteria**: Next.js app created, TypeScript configured, essential packages installed
  - **Dependencies**: Task 1.4
  - **Time Estimate**: 1 day
  - **Phase**: Foundation (Month 1)
  - **Completed**: 2025-01-29
  - **Notes**: Next.js 15.5.4, TypeScript 5, React 19, essential dependencies installed

- [x] **Task 2.2**: Configure Tailwind CSS and component library setup
  - **Completion Criteria**: Tailwind configured, base components created, responsive design system
  - **Dependencies**: Task 2.1, Task 1.7
  - **Time Estimate**: 2 days
  - **Phase**: Foundation (Month 1)
  - **Completed**: 2025-01-29
  - **Notes**: Tailwind CSS 4.1.13 configured with PostCSS, responsive design system in place

### Firebase Integration
- [x] **Task 2.3**: Set up Firebase project with Authentication, Firestore, and Storage
  - **Completion Criteria**: Firebase project configured, SDK integrated, environment variables set
  - **Dependencies**: Task 2.1, Task 1.4
  - **Time Estimate**: 2 days
  - **Phase**: Foundation (Month 1)
  - **Completed**: 2025-09-29
  - **Notes**: Reusing existing Firebase project (hale-ripsaw-403915). Created .env.local with credentials

- [x] **Task 2.4**: Implement Firebase Security Rules for multi-tenant isolation
  - **Completion Criteria**: Firestore rules implemented, tested, organization-level isolation working
  - **Dependencies**: Task 2.3, Task 1.5
  - **Time Estimate**: 3 days
  - **Phase**: Foundation (Month 1)
  - **Completed**: 2025-09-29
  - **Notes**: Firestore and Storage security rules successfully deployed. Multi-tenant isolation with RBAC implemented.

### Development Tools & Pre-commit Hooks
- [x] **Task 2.5**: Configure development tools and testing framework
  - **Completion Criteria**: ESLint, Prettier, Jest, Cypress configured, GitHub Actions setup
  - **Dependencies**: Task 2.1
  - **Time Estimate**: 2 days
  - **Phase**: Foundation (Month 1)
  - **Completed**: 2025-01-29
  - **Notes**: ESLint + Prettier configured, React Hook Form + Zod for validation

- [ ] **Task 2.5A**: Configure Husky pre-commit hooks (NEW)
  - **Completion Criteria**: Automated linting, formatting, type-check on commit
  - **Dependencies**: Task 2.5
  - **Time Estimate**: 2 hours
  - **Phase**: Foundation (Month 2)
  - **Hooks to Add**:
    - Lint staged files
    - Format with Prettier
    - TypeScript type-check
    - Run relevant tests

- [ ] **Task 2.5B**: Set up Dependabot for dependency updates (NEW)
  - **Completion Criteria**: Automated weekly dependency PRs configured
  - **Dependencies**: Task 2.1
  - **Time Estimate**: 1 hour
  - **Phase**: Foundation (Month 2)
  - **Configuration**: .github/dependabot.yml for npm, GitHub Actions

- [ ] **Task 2.5C**: Create GitHub issue templates (NEW)
  - **Completion Criteria**: Bug report, feature request, question templates
  - **Dependencies**: None
  - **Time Estimate**: 1 hour
  - **Phase**: Foundation (Month 2)
  - **Templates**: Bug, Feature, Documentation, Question

- [ ] **Task 2.5D**: Configure security headers in Next.js (NEW)
  - **Completion Criteria**: CSP, X-Frame-Options, HSTS headers configured
  - **Dependencies**: Task 2.1
  - **Time Estimate**: 2 hours
  - **Phase**: Foundation (Month 2)
  - **Headers**: Content-Security-Policy, X-Frame-Options, Strict-Transport-Security

### Testing Infrastructure (MOVED UP FROM MONTH 4)
- [ ] **Task 2.6A**: Set up Jest unit testing framework (NEW)
  - **Completion Criteria**: Jest configured, sample tests passing, coverage reporting
  - **Dependencies**: Task 2.5
  - **Time Estimate**: 1 day
  - **Phase**: Foundation (Month 2) - MOVED UP
  - **Configuration**: jest.config.js, test utils, coverage thresholds

- [ ] **Task 2.6B**: Configure Cypress E2E testing (NEW)
  - **Completion Criteria**: Cypress installed, sample E2E test passing
  - **Dependencies**: Task 2.5
  - **Time Estimate**: 1 day
  - **Phase**: Foundation (Month 2) - MOVED UP
  - **Configuration**: cypress.config.ts, custom commands, fixtures

- [ ] **Task 2.6C**: Integrate Firebase emulator suite (NEW)
  - **Completion Criteria**: Local Firestore, Auth, Functions emulators running
  - **Dependencies**: Task 2.3
  - **Time Estimate**: 1 day
  - **Phase**: Foundation (Month 2) - MOVED UP
  - **Emulators**: Firestore, Authentication, Functions, Storage

- [ ] **Task 2.6D**: Add test coverage reporting to CI/CD (NEW)
  - **Completion Criteria**: GitHub Actions run tests, report coverage
  - **Dependencies**: Task 2.6A, Task 2.6B
  - **Time Estimate**: 4 hours
  - **Phase**: Foundation (Month 2) - MOVED UP
  - **Target**: >80% coverage for critical paths

- [ ] **Task 2.6E**: Create TESTING_STRATEGY.md (NEW)
  - **Completion Criteria**: Complete testing strategy documentation
  - **Dependencies**: Task 2.6A, Task 2.6B, Task 2.6C
  - **Time Estimate**: 4 hours
  - **Phase**: Foundation (Month 2) - MOVED UP
  - **Content**: Testing pyramid, coverage goals, test patterns

### Performance Monitoring (MOVED UP FROM MONTH 8)
- [ ] **Task 2.7A**: Configure Sentry error tracking (NEW)
  - **Completion Criteria**: Sentry integrated, errors tracked, sourcemaps uploaded
  - **Dependencies**: Task 2.1
  - **Time Estimate**: 3 hours
  - **Phase**: Foundation (Month 2) - MOVED UP
  - **Configuration**: @sentry/nextjs, error boundaries

- [ ] **Task 2.7B**: Set up Vercel Analytics (NEW)
  - **Completion Criteria**: Analytics enabled, performance metrics tracked
  - **Dependencies**: Task 2.1
  - **Time Estimate**: 1 hour
  - **Phase**: Foundation (Month 2) - MOVED UP
  - **Metrics**: Page views, Web Vitals, custom events

- [ ] **Task 2.7C**: Define performance budgets (NEW)
  - **Completion Criteria**: Performance budgets documented, alerts configured
  - **Dependencies**: Task 2.7B
  - **Time Estimate**: 2 hours
  - **Phase**: Foundation (Month 2) - MOVED UP
  - **Budgets**: Page load <2s, API <500ms, FCP <1.8s, LCP <2.5s

- [ ] **Task 2.7D**: Set up uptime monitoring (NEW)
  - **Completion Criteria**: UptimeRobot or similar configured, alerts active
  - **Dependencies**: None (can use free tier)
  - **Time Estimate**: 1 hour
  - **Phase**: Foundation (Month 2) - MOVED UP
  - **Monitors**: Homepage, API health check, auth endpoints

### UI Component Library
- [x] **Task 2.6**: Build Core UI Component Library
  - **Completion Criteria**: Reusable UI components for dashboards and user interactions
  - **Dependencies**: Task 2.2
  - **Time Estimate**: 3 days
  - **Phase**: Foundation (Month 1)
  - **Completed**: 2025-01-29
  - **Components**: Card, Modal, Alert, LoadingSpinner, Badge

- [x] **Task 2.7**: Create Layout Components
  - **Completion Criteria**: Reusable layout components for application structure
  - **Dependencies**: Task 2.6
  - **Time Estimate**: 2 days
  - **Phase**: Foundation (Month 1)
  - **Completed**: 2025-01-29
  - **Components**: DashboardLayout, FormContainer, PageHeader, Breadcrumb

- [x] **Task 2.8**: Build Authentication UI Pages (Preparation)
  - **Completion Criteria**: Complete authentication flow UI without Firebase backend integration
  - **Dependencies**: Task 2.7
  - **Time Estimate**: 2 days
  - **Phase**: Foundation (Month 1)
  - **Completed**: 2025-01-29
  - **Pages**: Login, Register, Forgot Password, Verify Email

---

## 3. Core Authentication & Organization System (10 tasks) - Month 2

### API Architecture Documentation (NEW)
- [x] **Task 3.1A**: Create API_ARCHITECTURE.md with patterns (NEW)
   - **Completion Criteria**: Complete API design patterns documented
   - **Dependencies**: Task 2.1
   - **Time Estimate**: 1 day
   - **Phase**: Foundation (Month 2)
   - **Completed**: 2025-09-29
   - **Notes**: API_ARCHITECTURE.md already exists with complete documentation (2182 lines)
   - **Content**:
     - RESTful conventions
     - Error handling patterns
     - Request/response formats
     - Validation with Zod
     - Rate limiting strategy

- [x] **Task 3.1B**: Define error handling and validation strategy (NEW)
   - **Completion Criteria**: Standardized error codes, Zod schemas for all endpoints
   - **Dependencies**: Task 3.1A
   - **Time Estimate**: 1 day
   - **Phase**: Foundation (Month 2)
   - **Completed**: 2025-09-29
   - **Notes**: Created lib/api/errors.ts with standardized error utilities and complete error catalog
   - **Deliverables**:
     - Error code catalog (AUTH_*, VALIDATION_*, RESOURCE_*, BUSINESS_*, RATE_*, SERVER_*)
     - Standard error response format
     - Helper functions for all common errors

- [x] **Task 3.1C**: Implement rate limiting middleware (NEW)
   - **Completion Criteria**: Rate limiting active on all API routes
   - **Dependencies**: Task 3.1B
   - **Time Estimate**: 1 day
   - **Phase**: Foundation (Month 2)
   - **Completed**: 2025-09-29
   - **Notes**: Created lib/api/rate-limit.ts with Upstash Redis implementation
   - **Limits**: 100 req/min per user, 1000 req/hour per org

- [x] **Task 3.1D**: Document API response formats (NEW)
   - **Completion Criteria**: Standard response format for success/error
   - **Dependencies**: Task 3.1A
   - **Time Estimate**: 4 hours
   - **Phase**: Foundation (Month 2)
   - **Completed**: 2025-09-29
   - **Notes**: Documented in API_ARCHITECTURE.md and implemented in lib/api/errors.ts
   - **Formats**: Success, Error, Pagination, Validation errors

### User Authentication System
- [ ] **Task 3.1**: Implement Firebase Authentication with email/password and Google SSO
  - **Completion Criteria**: Login/logout working, user registration, password reset functionality
  - **Dependencies**: Task 2.3, Task 3.1A
  - **Time Estimate**: 3 days
  - **Phase**: Foundation (Month 2)

- [ ] **Task 3.2**: Build user profile management and role-based access control
  - **Completion Criteria**: User profiles, role assignment, custom Firebase Auth claims
  - **Dependencies**: Task 3.1
  - **Time Estimate**: 4 days
  - **Phase**: Foundation (Month 2)

### Multi-tenant Organization System
- [ ] **Task 3.3**: Implement organization creation and management
  - **Completion Criteria**: Organization CRUD, user-organization relationships, tenant isolation
  - **Dependencies**: Task 3.2, Task 2.4
  - **Time Estimate**: 1 week
  - **Phase**: Foundation (Month 2)

- [ ] **Task 3.4**: Build user invitation and team management system
  - **Completion Criteria**: User invitations, role assignment, team management interface
  - **Dependencies**: Task 3.3
  - **Time Estimate**: 4 days
  - **Phase**: Foundation (Month 2)

### Project Management Foundation
- [ ] **Task 3.5**: Create project management system for organizing TRAs
  - **Completion Criteria**: Project CRUD, project-user relationships, project-based access control
  - **Dependencies**: Task 3.3
  - **Time Estimate**: 3 days
  - **Phase**: Foundation (Month 2)

- [ ] **Task 3.6**: Implement file upload system with Firebase Storage
  - **Completion Criteria**: File upload, image optimization, secure access, metadata management
  - **Dependencies**: Task 2.3
  - **Time Estimate**: 3 days
  - **Phase**: Foundation (Month 2)

---

## 4. TRA Creation System (16 tasks) - Months 3-4

### TRA Data Model & Templates
- [ ] **Task 4.1**: Implement TRA data model in Firestore
  - **Completion Criteria**: TRA document structure, task steps, validation rules, relationships
  - **Dependencies**: Task 3.5, Task 1.5
  - **Time Estimate**: 4 days
  - **Phase**: TRA Core (Month 3)

- [ ] **Task 4.2**: Build TRA template system with industry-specific templates
  - **Completion Criteria**: Template CRUD, 5+ VCA-compliant templates, template versioning
  - **Dependencies**: Task 4.1
  - **Time Estimate**: 1.5 weeks
  - **Phase**: TRA Core (Month 3)

- [ ] **Task 4.3**: Create hazard identification library and database
  - **Completion Criteria**: 100+ common hazards categorized by industry, search functionality
  - **Dependencies**: Task 4.1
  - **Time Estimate**: 1 week
  - **Phase**: TRA Core (Month 3)

### Risk Assessment Engine
- [ ] **Task 4.4**: Implement Kinney & Wiruth risk calculation engine
  - **Completion Criteria**: Risk calculator, score validation, risk level determination, edge cases handled
  - **Dependencies**: Task 4.1
  - **Time Estimate**: 1 week
  - **Phase**: TRA Core (Month 3)

- [ ] **Task 4.5**: Build control measures recommendation system
  - **Completion Criteria**: Hierarchical control suggestions, customization, effectiveness scoring
  - **Dependencies**: Task 4.4, Task 4.3
  - **Time Estimate**: 1.5 weeks
  - **Phase**: TRA Core (Month 3)

### TRA Creation Interface
- [ ] **Task 4.6**: Create TRA creation wizard with step-by-step guidance
  - **Completion Criteria**: Multi-step form, progress tracking, auto-save, validation, template integration
  - **Dependencies**: Task 4.2, Task 4.4
  - **Time Estimate**: 2 weeks
  - **Phase**: TRA Core (Month 3)

### Demo Environment (NEW)
- [ ] **Task 4.6A**: Design and create seed data structure (NEW)
  - **Completion Criteria**: Realistic TRA/LMRA demo data schema designed
  - **Dependencies**: Task 4.1
  - **Time Estimate**: 2 days
  - **Phase**: TRA Core (Month 4)
  - **Data**: Sample organizations, users, projects, TRAs, LMRAs

- [ ] **Task 4.6B**: Build data generation scripts (NEW)
  - **Completion Criteria**: Automated script to populate demo environment
  - **Dependencies**: Task 4.6A
  - **Time Estimate**: 3 days
  - **Phase**: TRA Core (Month 4)
  - **Script**: Node.js script using Firebase Admin SDK

- [ ] **Task 4.6C**: Set up demo organization and users (NEW)
  - **Completion Criteria**: Demo org with realistic data for testing/demos
  - **Dependencies**: Task 4.6B
  - **Time Estimate**: 1 day
  - **Phase**: TRA Core (Month 4)
  - **Users**: Admin, safety manager, supervisor, field workers

- [ ] **Task 4.6D**: Document demo scenarios and walkthrough (NEW)
  - **Completion Criteria**: Demo script with scenarios for sales/investor demos
  - **Dependencies**: Task 4.6C
  - **Time Estimate**: 1 day
  - **Phase**: TRA Core (Month 4)
  - **Scenarios**: TRA creation, LMRA execution, reporting

### Collaboration Features
- [ ] **Task 4.7**: Implement real-time collaborative editing with Firebase
  - **Completion Criteria**: Multiple users can edit TRA simultaneously, conflict resolution, presence indicators
  - **Dependencies**: Task 4.6, Task 3.2
  - **Time Estimate**: 1.5 weeks
  - **Phase**: TRA Core (Month 3-4)

- [ ] **Task 4.8**: Build comment and annotation system for TRA review
  - **Completion Criteria**: Comments on TRA sections, annotations, notification system
  - **Dependencies**: Task 4.7
  - **Time Estimate**: 1 week
  - **Phase**: TRA Core (Month 4)

### Approval Workflow
- [ ] **Task 4.9**: Create approval workflow system with role-based permissions
  - **Completion Criteria**: Configurable approval steps, role-based routing, status tracking
  - **Dependencies**: Task 4.8, Task 3.2
  - **Time Estimate**: 1.5 weeks
  - **Phase**: TRA Core (Month 4)

- [ ] **Task 4.10**: Implement digital signature capture for approvals
  - **Completion Criteria**: Electronic signatures, legal compliance, audit trail integration
  - **Dependencies**: Task 4.9
  - **Time Estimate**: 1 week
  - **Phase**: TRA Core (Month 4)

### TRA Management & Search
- [ ] **Task 4.11**: Build TRA library with search and filtering capabilities
  - **Completion Criteria**: Full-text search, faceted filtering, sorting, pagination, bulk operations
  - **Dependencies**: Task 4.6
  - **Time Estimate**: 1.5 weeks
  - **Phase**: TRA Core (Month 4)

### Search Integration (NEW - DEFERRED TO PHASE 2)
- [ ] **Task 4.11A**: Evaluate and select search solution (Algolia) (NEW)
  - **Completion Criteria**: Algolia account created, evaluated vs alternatives
  - **Dependencies**: Task 4.11
  - **Time Estimate**: 1 day
  - **Phase**: Phase 2 - DEFERRED FROM MVP
  - **Alternatives**: Algolia, Typesense, ElasticSearch
  - **Decision**: Deferred - use Firestore queries for MVP, add based on customer demand

- [ ] **Task 4.11B**: Design search index schema (NEW)
  - **Completion Criteria**: Algolia index structure designed for TRAs, templates, hazards
  - **Dependencies**: Task 4.11A
  - **Time Estimate**: 1 day
  - **Phase**: Phase 2 - DEFERRED FROM MVP
  - **Indexes**: TRAs, Templates, Hazards, Projects

- [ ] **Task 4.11C**: Implement incremental indexing (NEW)
  - **Completion Criteria**: Cloud Function syncs Firestore changes to Algolia
  - **Dependencies**: Task 4.11B
  - **Time Estimate**: 2 days
  - **Phase**: Phase 2 - DEFERRED FROM MVP
  - **Trigger**: Firestore onCreate, onUpdate, onDelete

- [ ] **Task 4.11D**: Build search UI with filters (NEW)
  - **Completion Criteria**: Search interface with faceted filtering
  - **Dependencies**: Task 4.11C
  - **Time Estimate**: 3 days
  - **Phase**: Phase 2 - DEFERRED FROM MVP
  - **Filters**: Risk level, status, project, date range, hazard type

### Customer Onboarding (MOVED UP FROM MONTH 8)
- [ ] **Task 4.12A**: Design interactive product tour (NEW)
  - **Completion Criteria**: 3-5 step product tour on first login
  - **Dependencies**: Task 4.6
  - **Time Estimate**: 2 days
  - **Phase**: TRA Core (Month 4) - MOVED UP
  - **Tool**: React Joyride or custom solution
  - **Steps**: Create TRA, Execute LMRA, View Reports

- [ ] **Task 4.12B**: Create pre-loaded sample TRA templates (NEW)
  - **Completion Criteria**: New orgs get 5+ sample templates
  - **Dependencies**: Task 4.2
  - **Time Estimate**: 1 day
  - **Phase**: TRA Core (Month 4) - MOVED UP
  - **Templates**: Electrical work, Confined space, Working at height

- [ ] **Task 4.12C**: Build quick start wizard (NEW)
  - **Completion Criteria**: Step-by-step wizard for org setup
  - **Dependencies**: Task 3.3
  - **Time Estimate**: 3 days
  - **Phase**: TRA Core (Month 4) - MOVED UP
  - **Steps**: Org details, Add team, Create project, First TRA

- [ ] **Task 4.12D**: Implement contextual help system (NEW)
  - **Completion Criteria**: ? icons with tooltips throughout app
  - **Dependencies**: Task 4.12A
  - **Time Estimate**: 2 days
  - **Phase**: TRA Core (Month 4) - MOVED UP
  - **Help**: Tooltips, help modals, link to documentation

### Analytics Dashboard
- [ ] **Task 4.12**: Create TRA analytics dashboard with key safety metrics
  - **Completion Criteria**: Risk distribution charts, compliance tracking, trend analysis
  - **Dependencies**: Task 4.11
  - **Time Estimate**: 1.5 weeks
  - **Phase**: TRA Core (Month 4)

---

## 5. Mobile LMRA System (14 tasks) - Months 5-6

### PWA Foundation
- [ ] **Task 5.1**: Convert Next.js app to Progressive Web App with offline capabilities
  - **Completion Criteria**: Service worker, app manifest, offline functionality, installable
  - **Dependencies**: Task 4.6
  - **Time Estimate**: 1 week
  - **Phase**: Mobile LMRA (Month 5)

### File Optimization (NEW)
- [ ] **Task 5.1A**: Implement client-side image compression (NEW)
  - **Completion Criteria**: Images compressed before upload
  - **Dependencies**: Task 3.6
  - **Time Estimate**: 2 days
  - **Phase**: Mobile LMRA (Month 5)
  - **Library**: browser-image-compression or similar
  - **Target**: Reduce image sizes by 40-60%

- [ ] **Task 5.1B**: Add Cloud Function for thumbnail generation (NEW)
  - **Completion Criteria**: Automatic thumbnails on image upload
  - **Dependencies**: Task 5.1A
  - **Time Estimate**: 2 days
  - **Phase**: Mobile LMRA (Month 5)
  - **Sizes**: 150x150, 300x300, 600x600

- [ ] **Task 5.1C**: Implement progressive upload strategy (NEW)
  - **Completion Criteria**: Large files upload in chunks with progress
  - **Dependencies**: Task 3.6
  - **Time Estimate**: 2 days
  - **Phase**: Mobile LMRA (Month 5)
  - **Benefits**: Better mobile experience, resume capability

- [ ] **Task 5.1D**: Add lazy loading for images (NEW)
  - **Completion Criteria**: Images load on scroll, not page load
  - **Dependencies**: Task 5.1B
  - **Time Estimate**: 1 day
  - **Phase**: Mobile LMRA (Month 5)
  - **Implementation**: Next.js Image component, IntersectionObserver

### Mobile Interface
- [ ] **Task 5.2**: Optimize mobile interface with touch-friendly design
  - **Completion Criteria**: Mobile-first responsive design, touch targets >44px, gesture support
  - **Dependencies**: Task 5.1
  - **Time Estimate**: 1 week
  - **Phase**: Mobile LMRA (Month 5)

- [ ] **Task 5.3**: Implement camera integration for safety photo documentation
  - **Completion Criteria**: Photo capture, image compression, local storage, Firebase upload
  - **Dependencies**: Task 5.1, Task 3.6
  - **Time Estimate**: 4 days
  - **Phase**: Mobile LMRA (Month 5)

- [ ] **Task 5.4**: Add GPS integration for location verification
  - **Completion Criteria**: Location capture, accuracy validation, privacy controls, offline caching
  - **Dependencies**: Task 5.1
  - **Time Estimate**: 3 days
  - **Phase**: Mobile LMRA (Month 5)

### LMRA Execution Engine
- [ ] **Task 5.5**: Build LMRA execution workflow based on TRA data
  - **Completion Criteria**: Dynamic checklists from TRA, step-by-step execution, progress tracking
  - **Dependencies**: Task 5.2, Task 4.1
  - **Time Estimate**: 2 weeks
  - **Phase**: Mobile LMRA (Month 5-6)

- [ ] **Task 5.6**: Implement environmental condition assessment and logging
  - **Completion Criteria**: Weather API integration, condition logging, risk factor validation
  - **Dependencies**: Task 5.5
  - **Time Estimate**: 1 week
  - **Phase**: Mobile LMRA (Month 6)

- [ ] **Task 5.7**: Create personnel competency verification system
  - **Completion Criteria**: Team member check-in, certification validation, competency tracking
  - **Dependencies**: Task 5.5, Task 3.2
  - **Time Estimate**: 1 week
  - **Phase**: Mobile LMRA (Month 6)

- [ ] **Task 5.8**: Build equipment verification with QR code scanning
  - **Completion Criteria**: QR code reader, equipment database, inspection status tracking
  - **Dependencies**: Task 5.7
  - **Time Estimate**: 4 days
  - **Phase**: Mobile LMRA (Month 6)

### Offline Sync & Real-time Features
- [ ] **Task 5.9**: Implement offline data synchronization with conflict resolution
  - **Completion Criteria**: Offline data storage, background sync, conflict resolution, queue management
  - **Dependencies**: Task 5.5
  - **Time Estimate**: 2 weeks
  - **Phase**: Mobile LMRA (Month 6)

- [ ] **Task 5.10**: Create real-time dashboard updates and push notifications
  - **Completion Criteria**: Firebase listeners, real-time UI updates, push notifications for alerts
  - **Dependencies**: Task 5.9, Task 4.12
  - **Time Estimate**: 1 week
  - **Phase**: Mobile LMRA (Month 6)

---

## 6. Reporting & Analytics System (12 tasks) - Month 7

### Analytics & Metrics (NEW)
- [ ] **Task 6.1A**: Define core product metrics (KPIs) (NEW)
  - **Completion Criteria**: KPI catalog documented with calculation methods
  - **Dependencies**: Task 4.12
  - **Time Estimate**: 1 day
  - **Phase**: Reporting (Month 7)
  - **Metrics**:
    - TRAs created per month
    - LMRAs executed per month
    - Average risk score
    - Compliance rate
    - Time to approval
    - User activation rate

- [ ] **Task 6.1B**: Implement event tracking in Firebase Analytics (NEW)
  - **Completion Criteria**: Custom events tracked for all key actions
  - **Dependencies**: Task 6.1A
  - **Time Estimate**: 2 days
  - **Phase**: Reporting (Month 7)
  - **Events**: TRA created, LMRA executed, Approval, Export, etc.

- [ ] **Task 6.1C**: Create metrics dashboard (NEW)
  - **Completion Criteria**: Admin dashboard showing all KPIs
  - **Dependencies**: Task 6.1B
  - **Time Estimate**: 3 days
  - **Phase**: Reporting (Month 7)
  - **Charts**: Line, bar, donut charts with Recharts

- [ ] **Task 6.1D**: Set up cohort analysis (NEW)
  - **Completion Criteria**: User cohort retention analysis
  - **Dependencies**: Task 6.1B
  - **Time Estimate**: 2 days
  - **Phase**: Reporting (Month 7)
  - **Analysis**: Day 1, Day 7, Day 30 retention

### Dashboard & Metrics
- [ ] **Task 6.1**: Build executive dashboard with real-time safety KPIs
  - **Completion Criteria**: Executive dashboard, key metrics, real-time updates, role-based views
  - **Dependencies**: Task 4.12, Task 5.10
  - **Time Estimate**: 1.5 weeks
  - **Phase**: Reporting (Month 7)

- [ ] **Task 6.2**: Create detailed risk analysis and trend reporting
  - **Completion Criteria**: Risk trend charts, project comparisons, drill-down capabilities
  - **Dependencies**: Task 6.1
  - **Time Estimate**: 1 week
  - **Phase**: Reporting (Month 7)

- [ ] **Task 6.3**: Implement LMRA execution analytics and performance metrics
  - **Completion Criteria**: LMRA completion rates, timing analysis, efficiency metrics
  - **Dependencies**: Task 6.1, Task 5.10
  - **Time Estimate**: 1 week
  - **Phase**: Reporting (Month 7)

### Professional Reporting
- [ ] **Task 6.4**: Build custom report builder with drag-and-drop interface
  - **Completion Criteria**: Report designer, section templates, preview functionality, save/load templates
  - **Dependencies**: Task 6.2
  - **Time Estimate**: 2 weeks
  - **Phase**: Reporting (Month 7)

- [ ] **Task 6.5**: Implement PDF report generation with custom branding
  - **Completion Criteria**: PDF export, custom branding, charts included, professional formatting
  - **Dependencies**: Task 6.4
  - **Time Estimate**: 1 week
  - **Phase**: Reporting (Month 7-8)

- [ ] **Task 6.6**: Create Excel export functionality for compliance reporting
  - **Completion Criteria**: Excel export, multiple sheets, formulas, compliance-ready format
  - **Dependencies**: Task 6.4
  - **Time Estimate**: 4 days
  - **Phase**: Reporting (Month 8)

### Compliance Features
- [ ] **Task 6.7**: Implement VCA compliance checking and templates
  - **Completion Criteria**: VCA-compliant templates, automated compliance scoring, audit readiness
  - **Dependencies**: Task 4.2, Task 6.4
  - **Time Estimate**: 1.5 weeks
  - **Phase**: Reporting (Month 8)

- [ ] **Task 6.8**: Build comprehensive audit trail system
  - **Completion Criteria**: Immutable audit logs, user action tracking, compliance reporting
  - **Dependencies**: Task 6.7
  - **Time Estimate**: 1 week
  - **Phase**: Reporting (Month 8)

---

## 7. Advanced Features & Integrations (7 tasks) - Month 8

### Payment & Subscription System
- [ ] **Task 7.1**: Integrate Stripe for subscription management
  - **Completion Criteria**: Stripe integration, subscription tiers, payment processing, billing dashboard
  - **Dependencies**: Task 3.3
  - **Time Estimate**: 1 week
  - **Phase**: Advanced (Month 8)

- [ ] **Task 7.2**: Implement usage tracking and tier-based feature limitations
  - **Completion Criteria**: Feature gates, usage monitoring, upgrade prompts, tier management
  - **Dependencies**: Task 7.1
  - **Time Estimate**: 4 days
  - **Phase**: Advanced (Month 8)

### Communication & Notifications
- [ ] **Task 7.3**: Set up email notification system with SendGrid
  - **Completion Criteria**: Transactional emails, templates, delivery tracking, unsubscribe handling
  - **Dependencies**: Task 4.9
  - **Time Estimate**: 3 days
  - **Phase**: Advanced (Month 8)

- [ ] **Task 7.4**: Implement push notifications for critical safety alerts
  - **Completion Criteria**: Web push notifications, priority-based alerts, notification preferences
  - **Dependencies**: Task 5.10, Task 7.3
  - **Time Estimate**: 3 days
  - **Phase**: Advanced (Month 8)

### Third-party Integrations
- [ ] **Task 7.5**: Create webhook system for external integrations
  - **Completion Criteria**: Webhook endpoints, retry logic, authentication, event routing
  - **Dependencies**: Task 7.1
  - **Time Estimate**: 4 days
  - **Phase**: Advanced (Month 8)

- [ ] **Task 7.6**: Build basic ERP integration framework (future expansion)
  - **Completion Criteria**: Integration architecture, sample connector, documentation for future development
  - **Dependencies**: Task 7.5
  - **Time Estimate**: 1 week
  - **Phase**: Phase 2 (DEFERRED FROM MVP)

### AI/ML Features (Optional Enhancement)
- [ ] **Task 7.7**: Implement basic AI features for hazard identification assistance
  - **Completion Criteria**: Hazard suggestion engine, photo analysis (basic), template recommendations
  - **Dependencies**: Task 4.3, Task 5.3
  - **Time Estimate**: 2 weeks
  - **Phase**: Phase 2 (DEFERRED FROM MVP)

---

## 8. Testing & Quality Assurance (8 tasks) - Months 2-8 (Continuous)

### Automated Testing
- [ ] **Task 8.1**: Implement comprehensive unit testing for all components
  - **Completion Criteria**: >90% code coverage, all business logic tested, automated test execution
  - **Dependencies**: Task 2.6A, ongoing with each feature
  - **Time Estimate**: Ongoing (30 min per feature)
  - **Phase**: Continuous (Month 2-8)

- [ ] **Task 8.2**: Create integration tests for Firebase interactions
  - **Completion Criteria**: Firestore operations tested, Authentication flow tested, Storage operations tested
  - **Dependencies**: Task 2.3, Task 8.1
  - **Time Estimate**: 1 week
  - **Phase**: TRA Core (Month 4)

- [ ] **Task 8.3**: Build end-to-end tests for critical user journeys
  - **Completion Criteria**: TRA creation flow, LMRA execution flow, user management flow tested
  - **Dependencies**: Task 5.5, Task 4.6
  - **Time Estimate**: 1.5 weeks
  - **Phase**: Mobile LMRA (Month 6)

### Mobile & PWA Testing
- [ ] **Task 8.4**: Test PWA functionality across different devices and browsers
  - **Completion Criteria**: iOS Safari, Android Chrome, offline functionality, installation tested
  - **Dependencies**: Task 5.1
  - **Time Estimate**: 1 week
  - **Phase**: Mobile LMRA (Month 6)

- [ ] **Task 8.5**: Conduct mobile usability testing with target users
  - **Completion Criteria**: 10+ field worker interviews, usability improvements implemented
  - **Dependencies**: Task 8.4
  - **Time Estimate**: 2 weeks
  - **Phase**: Advanced (Month 8)

### Performance & Security Testing
- [ ] **Task 8.6**: Perform load testing and performance optimization
  - **Completion Criteria**: Page load <2s, API response <500ms, Firebase optimization
  - **Dependencies**: Task 6.1
  - **Time Estimate**: 1 week
  - **Phase**: Advanced (Month 8)

- [ ] **Task 8.7**: Conduct security audit and penetration testing
  - **Completion Criteria**: Security scan clean, Firebase rules tested, data isolation verified
  - **Dependencies**: Task 2.4, Task 8.6
  - **Time Estimate**: 1 week
  - **Phase**: Advanced (Month 8)

- [ ] **Task 8.8**: GDPR compliance validation and privacy controls testing
  - **Completion Criteria**: Data export/deletion tested, consent management, privacy controls working
  - **Dependencies**: Task 8.7
  - **Time Estimate**: 4 days
  - **Phase**: Advanced (Month 8)

---

## 9. Marketing & Launch Preparation (4 NEW TASKS) - Months 6-8

### Marketing Materials
- [ ] **Task 8.9A**: Create landing page with product tour (NEW)
  - **Completion Criteria**: Marketing website with product screenshots/videos
  - **Dependencies**: Task 4.6
  - **Time Estimate**: 1 week
  - **Phase**: Advanced (Month 6-7)
  - **Sections**: Hero, Features, Pricing, Testimonials, CTA

- [ ] **Task 8.9B**: Build pricing page with feature comparison (NEW)
  - **Completion Criteria**: Interactive pricing tiers with feature matrix
  - **Dependencies**: Task 7.1
  - **Time Estimate**: 3 days
  - **Phase**: Advanced (Month 7)
  - **Tiers**: Starter, Professional, Enterprise

- [ ] **Task 8.9C**: Set up lead capture and CRM integration (NEW)
  - **Completion Criteria**: Email signup, lead tracking, CRM sync
  - **Dependencies**: Task 8.9A
  - **Time Estimate**: 2 days
  - **Phase**: Advanced (Month 7)
  - **Tools**: ConvertKit/Mailchimp, HubSpot/Pipedrive

- [ ] **Task 8.9D**: Create demo video and sales materials (NEW)
  - **Completion Criteria**: 3-5 min product demo video, sales one-pager
  - **Dependencies**: Task 4.6D
  - **Time Estimate**: 1 week
  - **Phase**: Advanced (Month 7-8)
  - **Assets**: Demo video, PDF one-pager, ROI calculator

---

## 10. Deployment & Launch Preparation (6 tasks) - Month 8

### Production Deployment
- [ ] **Task 9.1**: Set up production Firebase project with proper configuration
  - **Completion Criteria**: Production Firebase project, security rules deployed, monitoring configured
  - **Dependencies**: Task 2.3
  - **Time Estimate**: 2 days
  - **Phase**: Advanced (Month 8)

- [ ] **Task 9.2**: Configure Vercel production deployment with custom domain
  - **Completion Criteria**: Custom domain, SSL certificate, environment variables, monitoring
  - **Dependencies**: Task 9.1, Task 1.1
  - **Time Estimate**: 1 day
  - **Phase**: Advanced (Month 8)

- [ ] **Task 9.3**: Implement comprehensive monitoring and error tracking
  - **Completion Criteria**: Vercel Analytics, Sentry error tracking, Firebase monitoring, custom alerts
  - **Dependencies**: Task 9.2
  - **Time Estimate**: 2 days
  - **Phase**: Advanced (Month 8)

### Data Migration & Backup
- [ ] **Task 9.4**: Set up automated backup system for Firestore data
  - **Completion Criteria**: Automated daily backups, backup testing, restoration procedures
  - **Dependencies**: Task 9.1
  - **Time Estimate**: 2 days
  - **Phase**: Advanced (Month 8)

- [ ] **Task 9.5**: Create data import/export tools for customer onboarding
  - **Completion Criteria**: CSV/Excel import, data validation, bulk operations, export functionality
  - **Dependencies**: Task 9.4
  - **Time Estimate**: 1 week
  - **Phase**: Advanced (Month 8)

### Launch Preparation
- [ ] **Task 9.6**: Conduct final pre-launch testing and optimization
  - **Completion Criteria**: All features tested, performance optimized, security validated, documentation complete
  - **Dependencies**: Task 8.8, Task 9.3
  - **Time Estimate**: 1 week
  - **Phase**: Launch (Month 8)

---

## 11. Documentation & Knowledge Management (4 tasks) - Month 8

### Technical Documentation
- [ ] **Task 10.1**: Create comprehensive API documentation
  - **Completion Criteria**: All API routes documented, code examples, integration guides
  - **Dependencies**: Task 7.5
  - **Time Estimate**: 1 week
  - **Phase**: Advanced (Month 8)

- [ ] **Task 10.2**: Document Firebase schema and security rules
  - **Completion Criteria**: Data model documentation, security rule explanations, best practices
  - **Dependencies**: Task 2.4, Task 10.1
  - **Time Estimate**: 3 days
  - **Phase**: Advanced (Month 8)

### User Documentation
- [ ] **Task 10.3**: Create user guides and training materials
  - **Completion Criteria**: User manual, video tutorials, onboarding guide, FAQ
  - **Dependencies**: Task 8.5
  - **Time Estimate**: 2 weeks
  - **Phase**: Launch (Month 8)

- [ ] **Task 10.4**: Build in-app help system and onboarding flow
  - **Completion Criteria**: Contextual help, interactive tutorial, progress tracking, tips system
  - **Dependencies**: Task 10.3
  - **Time Estimate**: 1 week
  - **Phase**: MOVED TO Task 4.12A-4.12D (Month 4)
  - **NOTE**: This task has been split and moved earlier in the timeline

---

## Summary Statistics - REVISED V2

**Total Tasks**: 83 (54 original + 29 new strategic tasks)
**Status**: 9 completed, 5 paused (business activities), 69 pending (development tasks)
**Estimated Duration**: 6-8 months
**Team Size**: 1 solo developer
**Infrastructure Budget**: €275/month (€200 base + €75 tools)
**Monthly Operating Cost**: €275 (vs €120-220 in V1)

**Task Status Breakdown:**
- ✅ **Completed**: 9 tasks (Foundation setup, UI components, Auth pages, Firebase Security)
- ⏸️ **Paused**: 5 tasks (Market validation - skipped, user validated via website traffic)
- 🔄 **In Progress**: 0 tasks
- 📋 **Pending**: 69 tasks (Development work)

**Phase Distribution - OPTIMIZED FOR PARALLEL WORK:**
- Market Validation & Planning: 5 tasks (Weeks 1-3) - NEW
- Foundation & Setup: 24 tasks (Months 1-2) - up from 19
- TRA Core Features: 16 tasks (Months 3-4) - up from 12
- Mobile LMRA System: 14 tasks (Months 5-6) - up from 10
- Reporting & Analytics: 12 tasks (Month 7) - up from 8
- Advanced Features: 7 tasks (Month 8)
- Testing & QA: 8 tasks (Continuous, Months 2-8)
- Marketing & Launch: 4 tasks (Months 6-8) - NEW
- Deployment: 6 tasks (Month 8)
- Documentation: 4 tasks (Month 8)

**Key Strategic Improvements:**
- ✅ Market validation BEFORE continuing development (highest priority)
- ✅ Testing infrastructure moved to Month 2 (from Month 4)
- ✅ Performance monitoring from Month 2 (from Month 8)
- ✅ Customer onboarding moved to Month 4 (from Month 8)
- ✅ Added search functionality planning (deferred to Phase 2 based on demand)
- ✅ Added demo environment for sales/testing
- ✅ Added comprehensive analytics and metrics
- ✅ Added marketing preparation tasks
- ✅ Parallel work streams enabled for faster delivery

**New Tool Budget Items:**
- GitHub Copilot: €10/month (AI code assistance)
- SendGrid/Email: €15/month (email notifications)
- Algolia: €50/month (DEFERRED to Phase 2 - search functionality)
- **Total New Tools**: +€75/month (Algolia deferred)

**Maintained Enterprise Features:**
- All comprehensive MVP features preserved
- Professional B2B SaaS capabilities
- Multi-tenant architecture with complete isolation
- VCA compliance and regulatory features
- Mobile PWA with offline capabilities
- Real-time collaboration and approval workflows

**Risk Mitigation Addressed:**
- Market validation prevents building wrong features
- Early testing prevents technical debt accumulation
- Search improves UX for large TRA libraries (Phase 2)
- Demo environment enables early sales
- Analytics provide product-market fit insights
- Marketing prep ensures better launch

**Parallel Work Opportunities:**
- Month 2: Testing + API Architecture + Auth (can work in parallel)
- Month 3-4: TRA Core + Demo Environment (sequential but with overlap)
- Month 5-6: Mobile LMRA + Reporting Foundation (can overlap)
- Month 7: Reporting + Marketing Materials (can overlap)
- Month 8: Polish + Launch Prep (sequential)

This revised checklist implements all strategic review recommendations while maintaining the solo developer approach and 6-8 month timeline through parallel work streams and better prioritization.