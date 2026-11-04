# InvoiceFlow: Product Definition

## One-liner
InvoiceFlow helps Polish B2B freelancers create invoices, track who has paid,
and see how much money is actually coming in over the next 30 days.

## Target user
Ola is a freelance developer or designer on B2B contracts. She invoices 3-8
clients a month in PLN or EUR. She currently uses a spreadsheet and sometimes
forgets to chase late payers.

Her jobs to be done:
1. Create and send a correct invoice in under two minutes.
2. See what is unpaid and what is overdue at a glance.
3. Know her expected income for the next few weeks.

## Key decisions
- Single-owner accounts: each user sees only their own data.
- Base currency PLN; invoices in PLN or EUR (NBP rate stored on issue date).
- VAT rate chosen per line item (23%, 8%, 5%, 0%), rounded per line.
- Gapless invoice numbering per user per year (e.g. FV/2026/001).
- Android and iOS release; Kotlin with Compose Multiplatform shared code.
- InvoiceFlow is a tracker, not certified accounting software.

## Success criteria
Product
- Sign-up to a sent invoice in under 5 minutes.
- Dashboard shows outstanding, overdue and 30-day expected income correctly.

Engineering
- Invoice numbers are gapless under concurrent requests (test proves it).
- Money is never stored as floating point.
- Core flows covered by automated tests; CI is green.

Portfolio
- Live backend, installable Android build (APK), iOS demonstrated on simulator, 2-minute demo video.
- README with architecture diagram and "key decisions" section.

## MVP scope (in)
- Sign-up, login, token refresh
- Clients (create, edit, archive)
- Invoice drafts with line items, VAT and totals
- Gapless numbering on issue
- Status lifecycle: draft -> issued -> paid (overdue computed from due date)
- Record a full payment
- PDF generation and share
- EUR invoices with NBP rate
- Dashboard: outstanding, overdue, 30-day expected income

## Non-goals
- KSeF e-invoicing integration
- Tax filing, JPK, accounting exports
- Teams, roles, multiple companies per user
- Partial payments, credit notes, corrections
- Online payment links
- Web client

## Cut order if time runs short
1. Recurring invoices
2. Overdue push reminders
3. Partial payments
4. PDF polish
5. Forecast refinements
