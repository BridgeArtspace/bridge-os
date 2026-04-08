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

If you run a pure self-storage facility, there are dozens of software options: SiteLink, StorEDGE, Easy Storage Solutions, Storeganise.

If you run storage alongside art studios, a commercial kitchen, an event venue, coworking, or rehearsal rooms, there is nothing. You end up paying for all of this:

| What you need | Tool you're paying for | Cost |
|---------------|----------------------|------|
| Storage management | Easy Storage Solutions | $80-200/mo |
| Resource booking | Skedda | $50-100/mo |
| Event calendaring | Tockify | $8-20/mo |
| Employee time tracking | TSheets/QuickBooks Time | $40-100/mo |
| Task management | Trello / Asana | $10-50/mo |
| CRM | Brevo / HubSpot | $25-100/mo |
| SEO & social media | Various tools | $50-200/mo |
| Adwords & on-page SEO | ESS (bundled markup) | $$$$ |
| **Total** | **8+ subscriptions & services** | **$500-1,500+/mo** |

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
- **Voice AI** -- Retell-powered phone system: answers calls, handles inquiries, routes to staff when needed.
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
| Payments | Stripe |
| Voice AI | Retell |
| Gate access | PDK |
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
| voice | Retell AI phone system integration |
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

## Who Is This For

- **Mixed-use facility operators.** You run storage alongside studios, kitchens, event spaces, coworking, rehearsal rooms, or maker spaces. No existing software handles your operation.
- **Independent storage operators.** You're tired of paying $200-400/month for SaaS software you don't own, can't customize, and can't export your data from.
- **Developers building for the storage industry.** There has never been an open-source foundation to build on. Now there is.

## Who Is This Not For

- Large REIT portfolios with 500+ facilities (use Storable/Monument)
- Operators who want a vendor to handle everything (use Storeganise or ESS)
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
- [x] Voice AI integration (Retell)
- [x] Gate access integration (PDK)
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
| Storage management | ESS / SiteLink ($80-400/mo) | Built-in |
| Resource & space booking | Skedda ($50-100/mo) | Built-in |
| Event calendaring | Tockify ($8-20/mo) | Built-in |
| Employee time tracking | TSheets ($40-100/mo) | Built-in (PWA) |
| Task management | Trello ($10-50/mo) | Built-in (Kanban) |
| CRM & customer records | Brevo ($25-100/mo) | Built-in |
| Contract e-signatures | DocuSign ($25-50/mo) | Built-in |
| Lien compliance | Spreadsheets + calendar reminders | Automated |
| AI phone answering | Answering service ($200-500/mo) | Built-in (Retell) |
| Gate access management | Separate vendor portal | Built-in (PDK) |
| Customer self-service portal | Doesn't exist | Built-in |
| Adwords & on-page SEO | ESS / agency (marked up) | You control it directly |
| **Total before** | **$750-1,900+/mo across 8-10 tools & services** | |
| **Total with Bridge OS** | | **$0 (self-hosted) or hosting cost** |

**5-year savings per facility: $45,000 - $114,000**

## Compared To Storage Software

| | Bridge OS | SiteLink | ESS | Storeganise |
|---|---|---|---|---|
| Open source | Yes | No | No | No |
| Self-hosted | Yes | No | No | No |
| Mixed-use (storage + events + studios + kitchen) | Native | No | No | No |
| Replaces booking/calendar/CRM/tasks | Yes | No | No | No |
| AI voice | Built-in | No | No | No |
| E-signatures | Built-in | Add-on | Add-on | Add-on |
| Employee timekeeping | Built-in | No | No | No |
| Lien compliance automation | Built-in | Manual | Manual | No |
| Price (self-hosted) | Free | $200-400/mo | $80-200/mo | $50-150/mo |
| You own the code | Yes | No | No | No |
| You own your data | Yes | Vendor controls | Vendor controls | Vendor controls |

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
