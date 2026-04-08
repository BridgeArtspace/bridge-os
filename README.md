<p align="center">
  <h1 align="center">Bridge OS</h1>
  <p align="center">
    Open-source facility management for mixed-use buildings.
    <br />
    Storage. Studios. Events. Kitchens. Coworking. One system.
  </p>
</p>

<p align="center">
  <a href="#why">Why</a> &middot;
  <a href="#features">Features</a> &middot;
  <a href="#screenshots">Screenshots</a> &middot;
  <a href="#roadmap">Roadmap</a> &middot;
  <a href="#get-involved">Get Involved</a>
</p>

---

## The Problem

If you run a pure self-storage facility, there are dozens of software options. They all assume storage is your only business.

If you run storage alongside art studios, a commercial kitchen, an event venue, coworking, or rehearsal rooms, there is nothing. You end up paying for all of this:

| What you need | What you're paying for | Cost |
|---------------|----------------------|------|
| Storage management | Storage SaaS platform | $80-400/mo |
| Resource booking | Booking platform | $50-100/mo |
| Event calendaring | Calendar widget | $8-20/mo |
| Employee time tracking | Time tracking SaaS | $40-100/mo |
| Task management | Project management tool | $10-50/mo |
| CRM | CRM platform | $25-100/mo |
| Contract e-signatures | E-signature service | $25-50/mo |
| SEO & social media | Various tools | $50-200/mo |
| Adwords & on-page SEO | Bundled with storage vendor (marked up) | $$$$ |
| **Total** | **8-10 subscriptions & services** | **$500-1,500+/mo** |

None of them talk to each other. The same customer exists in 4 different systems. You reconcile in spreadsheets. When someone rents a storage unit AND books the event space AND uses the kitchen, you're updating 3 dashboards manually.

We know because we lived it. Bridge Storage Arts & Events in Richmond, CA ran all of the above before we built Bridge OS to replace them.

**Bridge OS is one system for facilities that do more than storage.**

## Why

Bridge OS is extracted from production software running a real mixed-use facility in Richmond, California: 500 storage units, 30 artist studios, a woodshop, a commercial kitchen, a 1,500 sq ft event space, entrepreneurship coaching, and public art installations throughout the property.

It was built by the facility operator, not a software company. Every feature exists because a real operational problem demanded it.

There is no open-source self-storage management software. Bridge OS is the first.

## Features

### Core Operations
- **Unit & space management** -- storage units, studios, kitchens, event rooms, coworking desks. One inventory across all space types.
- **Contracts & leases** -- create, activate, terminate. Rate changes, billing day management, move-in/move-out workflows.
- **Billing & invoicing** -- automated invoice generation, line items, tax rates, partial payments, payment application.
- **Payment processing** -- Stripe integration, multiple payment methods (card, ACH, cash, check), refunds.
- **Customer management** -- single customer record across all space types. Notes, documents, communication history.

### Compliance & Legal
- **Lien management** -- full California lien process: pre-lien notices, access restriction, sale notices, advertisement, auction. Jurisdiction-configurable timelines.
- **SCRA verification** -- Servicemembers Civil Relief Act compliance checks before access restriction.
- **E-signatures** -- inline contract signing with typed/drawn signatures, PDF generation with audit pages, dual-hash verification, QR code validation.
- **Insurance tracking** -- tenant protection plan management.

### Scheduling & Bookings
- **Resource booking** -- request/approve workflow for event spaces, conference rooms, studios.
- **Public events** -- event creation, RSVP management, signup tracking.
- **Availability management** -- conflict detection, calendar views.

### Customer Self-Service
- **Portal** -- customers can view contracts, invoices, payment history, and documents.
- **Online applications** -- "Grab It" flow: browse available units on the website, apply, complete onboarding, sign contract, move in. No staff intervention required.
- **Magic links** -- passwordless portal access for onboarding.

### AI & Automation
- **Voice AI** -- Retell-powered phone system that actually runs your front desk: answers customer questions, processes payments over the phone, gives lien status and balance-due information, provides gate hours, and walks new tenants through onboarding. Not a phone tree. A real conversation.
- **AI assistant** -- natural language queries against facility data.
- **Automated lien escalation** -- daily job checks overdue invoices, creates compliance tasks with escalating urgency.
- **Recurring tasks** -- template-based task generation (daily, weekly, monthly, quarterly, seasonal).

### Staff Operations
- **Task board** -- Kanban-style task management with assignment, urgency levels, and project grouping.
- **Timekeeping** -- employee clock-in/out PWA with job code tracking, interruption handling, and Gusto payroll integration.
- **Gate access** -- PDK integration for gate events, access control tied to contract and payment status.
- **Activity logging** -- audit trail across all operations.
- **Admin UI** -- full staff interface built with Django, Tailwind CSS, and Flowbite components.

### Communications
- **Notification system** -- email and SMS notifications for contract events, payment reminders, booking confirmations.
- **Template engine** -- configurable message and contract templates with variable substitution.
- **Promotion management** -- promotional pricing with attribution codes and automatic expiration.

### Public Website
- **Marketing site** -- responsive public website with unit browsing, space information, event listings.
- **API-driven** -- website pulls live availability from the backend API.
- **Mobile-first** -- designed for phone browsing (most storage customers search on mobile).

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Python, Django 5.x, Django REST Framework |
| Database | PostgreSQL |
| Frontend (admin) | Django templates, Tailwind CSS, Flowbite |
| Frontend (timeclock) | React 18, TypeScript, Vite |
| Frontend (website) | HTML, Tailwind CSS, vanilla JS |
| Payments | Stripe (pluggable) |
| Voice AI | Pluggable (Retell adapter included) |
| Gate access | Pluggable (PDK adapter included) |
| E-signatures | WeasyPrint + ReportLab + pypdf |
| PDF verification | SHA-256 dual-hash, QR codes |
| Deployment | Docker, Railway (or any container host) |
| CI/CD | GitHub Actions |
| Tests | pytest, Playwright, Vitest |

## Architecture

```
apps/
  backend/          Django API + Admin UI
    core/           Identity, auth, commands, analytics
    domain/         27 bounded contexts (see below)
    ui/             Admin, portal, and public interfaces
  website/          Public marketing site
  timeclock/        Employee time tracking PWA
  e2e/              End-to-end Playwright tests
```

### Domain Modules

| Domain | What it does |
|--------|-------------|
| units | Space inventory across all types |
| customers | Customer records, notes, documents |
| contracts | Lease lifecycle (pending, active, terminated) |
| billing | Invoice generation, line items, tax |
| payments | Payment processing, application, refunds |
| liens | California lien compliance state machine |
| esign | E-signature capture, PDF generation, verification |
| scheduling | Resource booking, availability, public events |
| tasks | Kanban board, recurring tasks, project management |
| timekeeping | Clock in/out, job codes, payroll export |
| voice | AI front desk: answers questions, takes payments, gives lien/balance info, onboards tenants |
| gate_events | PDK gate access control and audit log |
| applications | Online unit applications and onboarding |
| promotions | Promotional pricing and attribution |
| insurance | Tenant protection plan tracking |
| communications | Notifications, templates, messaging |
| bookings | Generic booking management |
| access | Permission and access control |
| documents | Document storage and management |
| moveouts | Move-out workflow and deposit handling |
| reservations | Unit reservation management |
| reviews | Customer feedback |
| notifications | Event-driven notification dispatch |
| activity | Audit trail and activity logging |
| ai_assistant | Natural language facility queries |
| catalog | Service and product catalog |
| signatures | Signature capture and storage |

## What's Different About How This Was Built

Bridge OS isn't just a codebase. It's a system designed to be developed, maintained, and extended by AI-assisted developers.

### AI-Native Development Tooling

**3,700+ lines of Claude Code rules** ship with the repo. These aren't comments or docs — they're structured instructions that give AI coding assistants deep context about every domain: how contracts work, what lien compliance requires, which state transitions are legal, how billing flows connect to payments. An AI assistant working on this codebase understands storage operations, not just Python syntax.

```
.claude/rules/
  00-core.md              # Architecture, workflow, verification gates
  10-python-django.md     # Service layer patterns, cross-domain rules
  20-domains.md           # Entity relationships, state machines
  22-workflows.md         # Staff operational workflows (move-in, move-out, payment)
  25-scheduling.md        # Booking and task state machines
  26-liens.md             # California lien compliance (full state machine + timeline)
  27-contracts-esign.md   # Contract lifecycle, e-sign flow, PDF architecture
  30-testing.md           # TDD requirements, coverage thresholds
  40-ops.md               # CI/CD, migrations, deployment
  50-ui.md                # Flowbite components, bridge-* CSS classes
  60-security.md          # Auth, CSRF, input validation, secrets
  70-cards.md             # Card-code bijection requirements
```

What this means in practice: a developer (or AI agent) can pick up any part of the codebase and understand the domain constraints, not just the code. The rules encode the operational knowledge of running a mixed-use facility.

### Card-Based Domain Documentation

Every model, command, job, and business rule has a corresponding documentation card — an Obsidian-compatible markdown file that stays in sync with the code. Cards use wikilinks for cross-references and code pointers for implementations. When the code changes, the card must change with it (enforced by convention).

This is a **card-code bijection**: every significant code artifact has exactly one card, and every card points to exactly one implementation. No stale docs. No undocumented models.

### Self-Healing CI Pipeline

GitHub Issues labeled `autofix` are automatically picked up by Claude Code, which attempts a fix, runs tests, and opens a PR. If it fails, a retry sweep re-runs it (up to 3 attempts). If that fails, a local agent with unlimited context picks it up. Issues that are too large get automatically decomposed into sub-issues.

```
Issue filed → Claude Code attempts fix (30 turns)
  → Success: PR opened, tests pass
  → Failure: Retry sweep (gh run rerun, up to 3x)
    → Failure: Local agent with unlimited turns
      → Too large: Auto-decompose into sub-issues
```

### Test Coverage

- **3,741 backend tests** (pytest)
- **44 end-to-end specs** (Playwright) covering golden paths: unit rental, self-service onboarding, contract signing, payment processing, space booking
- **OCR-based visual verification** — screenshots are OCR'd to verify rendered text matches expected content (catches CSS overflow, z-index, viewport issues that DOM inspection misses)
- **159 management commands** for operations, data migration, and maintenance

### Domain-Driven Architecture

27 bounded contexts, each with its own models, services, and views. Business logic lives in the service layer, never in views. Domains communicate through service interfaces, never by importing each other's models directly. State machines are explicit (contracts, invoices, payments, liens, bookings, tasks all have documented state diagrams).

## Who Is This For

- **Mixed-use facility operators.** You run storage alongside studios, kitchens, event spaces, coworking, rehearsal rooms, or maker spaces. No existing software handles your operation.
- **Independent storage operators.** You're tired of paying $200-400/month for SaaS software you don't own, can't customize, and can't export your data from.
- **Developers building for the storage industry.** There has never been an open-source foundation to build on. Now there is.

## Who Is This Not For

- Large REIT portfolios with 500+ facilities (enterprise platforms exist for that)
- Operators who want a vendor to handle everything (managed SaaS platforms exist for that)
- People who need it to work perfectly out of the box today (we're still in active development)

## Status

Bridge OS is extracted from production software running a real facility. Core features are battle-tested. The open-source extraction (branding removal, configuration, deployment tooling, documentation) is in progress.

**What works today:** All 27 domain modules are implemented with models, services, and views. The system manages real units, real customers, real money.

**What's in progress:** Deployment tooling for new facilities, configurable branding, demo seed data, multi-jurisdiction lien support.

Star this repo to follow progress. We'll tag releases as extraction milestones complete.

## Roadmap

### Phase 1: Foundation (in progress)
- [x] All domain modules implemented
- [x] Admin UI for staff operations
- [x] Customer self-service portal
- [x] E-signature and PDF generation
- [x] Stripe payment integration
- [x] Lien compliance (California)
- [x] Voice AI integration
- [x] Gate access integration
- [x] Public website with live availability
- [x] E2E test suite
- [ ] Branding extraction (configurable facility name, colors, assets)
- [ ] Docker Compose for local development
- [ ] Demo seed data command
- [ ] Deployment guide (Railway, Fly.io, self-hosted)

### Phase 2: Open Source Release
- [ ] AGPL license
- [ ] Contributing guidelines
- [ ] Feature flags for optional integrations (voice, gate, payments)
- [ ] Configuration documentation
- [ ] API documentation

### Phase 3: Community
- [ ] Multi-jurisdiction lien compliance (Texas, Florida)
- [ ] Additional payment providers
- [ ] Additional gate hardware support
- [ ] Localization / i18n
- [ ] Community forum or Discord

## What It Replaces

Bridge OS replaces the entire stack of tools a mixed-use facility duct-tapes together:

| Function | Before (separate tool) | Bridge OS |
|----------|----------------------|-----------|
| Storage management | Storage SaaS ($80-400/mo) | Built-in |
| Resource & space booking | Booking platform ($50-100/mo) | Built-in |
| Event calendaring | Calendar widget ($8-20/mo) | Built-in |
| Employee time tracking | Time tracking SaaS ($40-100/mo) | Built-in (PWA) |
| Task management | Project management tool ($10-50/mo) | Built-in (Kanban) |
| CRM & customer records | CRM platform ($25-100/mo) | Built-in |
| Contract e-signatures | E-signature service ($25-50/mo) | Built-in |
| Lien compliance | Spreadsheets + calendar reminders | Automated |
| AI phone answering | Answering service ($200-500/mo) | Built-in |
| Gate access management | Separate vendor portal | Built-in |
| Customer self-service portal | Doesn't exist | Built-in |
| Adwords & on-page SEO | Bundled with vendor (marked up) | You control it directly |
| **Total before** | **$750-1,900+/mo across 8-10 tools & services** | |
| **Total with Bridge OS** | | **$0 (self-hosted) or hosting cost** |

**5-year savings per facility: $45,000 - $114,000**

## Compared To Storage Software

| | Bridge OS | Typical storage SaaS |
|---|---|---|
| Open source | Yes | No |
| Self-hosted | Yes | No |
| Mixed-use (storage + events + studios + kitchen) | Native | No |
| Replaces booking/calendar/CRM/tasks | Yes | No |
| AI front desk (answers questions, takes payments, onboards) | Built-in | No |
| E-signatures | Built-in | Add-on or separate vendor |
| Employee timekeeping | Built-in | No |
| Lien compliance automation | Built-in | Manual |
| Price (self-hosted) | Free | $80-400/mo |
| You own the code | Yes | No |
| You own your data | Yes | Vendor controls export |

## Get Involved

Bridge OS is in active development. Here's how to participate:

**Star this repo** to follow progress and signal interest.

**Are you a mixed-use facility operator?** I'd love to hear how you currently manage your operation. What works, what doesn't, what you wish existed. Open an issue or email me.

**Are you a developer?** Contributions welcome once we hit Phase 2. Watch this repo for the contributing guidelines.

**Want a demo?** I can walk you through the production system running my facility. Open an issue or reach out directly.

## About

Built by Jeff Wright, operator of [Bridge Storage Arts & Events](https://bridgestorage.com) in Richmond, California.

I started my career as a math professor and software developer in the dBASE and MS-DOS days, delivering software on stacks of floppy disks to customer sites. Then I left tech, got into the storage business, and built Bridge into a mixed-use facility: 500 storage units, 30 artist studios, a woodshop, a commercial kitchen, a 1,500 sq ft event space, entrepreneurship coaching, and public art everywhere you look.

When I went looking for software to manage all of it, nothing existed. The storage tools didn't understand event bookings. The booking tools didn't understand lien compliance. So I started building again.

The tools have changed since the floppy disk days. The problems haven't. You still need software that understands your actual business, not someone else's idea of it.

I'm open-sourcing Bridge OS because nobody should have to build it again.

## License

AGPL-3.0 -- see [LICENSE](LICENSE) for details.

Free to use, modify, and deploy. If you distribute a modified version, you must open-source your changes. This ensures the community benefits from improvements while preventing proprietary forks.
