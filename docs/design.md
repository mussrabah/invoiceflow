# User Journeys, Screens & Architecture

**Goal:** Know exactly what the app does screen by screen, and how the pieces fit together, before writing code.

## 1. Core Journeys

| # | Journey | Steps |
|---|---|---|
| J1 | Onboard | Sign up → Add business details (name, tax ID, address, bank account) → Land on empty dashboard |
| J2 | Add client | Clients → New → Enter name, tax ID, address, default payment terms → Save |
| J3 | Create and issue invoice | New invoice → Pick client → Select currency → Add line items with VAT → Review totals → Issue (number assigned) → Share PDF |
| J4 | Record payment | Open issued invoice → Mark as paid → Choose payment date → Status becomes paid |
| J5 | Check cash flow | Open dashboard → See outstanding, overdue, and upcoming invoices for the next 30 days → Tap into a list |

## 2. Screen List

The application consists of **10 screens**.

| # | Screen | Description |
|---|---|---|
| 1 | Sign in | Authenticate an existing user |
| 2 | Sign up | Create a new account |
| 3 | Business profile | Onboarding and business profile editing |
| 4 | Dashboard | Financial overview and cash-flow summary |
| 5 | Invoice list | Browse invoices with filters: draft, issued, overdue, paid |
| 6 | Invoice editor | Select client and currency, manage line items, calculate live totals |
| 7 | Invoice detail | View invoice status and perform actions: issue, share PDF, mark paid |
| 8 | Client list | Browse and manage clients |
| 9 | Client editor | Create or edit client information |
| 10 | Settings | Access business profile and sign out |

### Navigation

The application uses a bottom navigation bar with four destinations:

- **Dashboard**
- **Invoices**
- **Clients**
- **Settings**

Invoice editors, client editors, and invoice detail screens open on top of the main navigation structure.

## 3. Architecture Decisions

The following are the recommended architectural and technology choices.

| Decision | Choice | Rationale |
|---|---|---|
| Backend shape | One Spring Boot application, packages organized by feature (`auth`, `clients`, `invoices`, `dashboard`) | A modular monolith is appropriate for a solo project and easy to explain. |
| Database | PostgreSQL with Flyway migrations | Versioned schema management and production-standard tooling. |
| API | REST and JSON, documented with OpenAPI | Easy to test, integrate, and demonstrate. |
| Authentication | Short-lived JWT access token plus rotating refresh token | A recognizable and defensible authentication pattern. |
| Money | Integer minor units plus a currency code | Avoids floating-point precision errors entirely. |
| PDF | **Generated on the server and downloaded by the mobile app** | Avoids implementing PDF generation separately for Android and iOS, saving significant iOS development time. |
| Mobile | Compose Multiplatform, Ktor Client, Koin, ViewModels with `StateFlow` | Maximizes shared business logic and minimizes platform-specific code. |
| Platform code | Only two `expect/actual` implementations: secure token storage and the native share sheet | Keeps platform-specific implementation and Mac development sessions short. |
| Local development | Docker Compose with PostgreSQL | One command to start the local development environment. |
| Hosting | To be decided in Phase 7 | No need to commit to an infrastructure provider yet. |

## 4. Guiding Principles

1. **Journey-driven development:** Implement features around complete user journeys rather than isolated screens.
2. **Shared mobile logic:** Keep business logic, networking, validation, and presentation state in common Kotlin code.
3. **Backend ownership:** The backend owns invoice numbering, financial calculations, persistence, and PDF generation.
4. **Financial precision:** Never use floating-point arithmetic for monetary calculations.
5. **Incremental architecture:** Start with a modular monolith; introduce additional infrastructure only when justified.

---

**Document status:** Initial architecture proposal.

**Scope:** Product definition and architectural planning, before implementation begins.
