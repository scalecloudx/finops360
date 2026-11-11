# Rocket.new design brief - ScaleCloud FinOps 360 (paste everything below the line)
---
Build a front-end-only prototype of **ScaleCloud FinOps 360**, a multi-cloud FinOps platform for enterprise customers and the managed-service consultants who serve them (GCC market).

## Hard constraints
- Next.js (App Router) + TypeScript + Tailwind CSS. Export clean, readable source code.
- **No backend, database, or authentication provided by the builder.** No Supabase/Firebase/builder-managed auth. All data comes from typed mock API modules in `/lib/api/` (one function per future endpoint, returning typed objects) so we can later swap mocks for a real REST API.
- Every mock value must be visibly labelled "Sample data" via a global banner.
- Do not use proprietary assets, logos or copy from other FinOps products.
- No claims of compliance certifications or guaranteed savings anywhere in the copy.

## Visual language
White background, royal blue (#1D4ED8) primary, cyan (#06B6D4) accent, slate neutrals. Clean enterprise look, dense but readable tables, 8px grid, Inter font. Responsive collapsible left sidebar. Light mode only. Layout must be RTL-ready (use logical CSS properties).

## Global shell
Top bar: **Customer switcher** (MSP consultants switch between customer organizations; customers see only their own), date-range picker, **currency selector (USD / AED / SAR)**, **cost basis selector (Unblended / Amortized / Net amortized)**, user menu with role badge (Customer Admin, Finance Viewer, MSP Consultant, MSP Admin). Left sidebar for the 8 screens. Reusable components: KPI card, filter bar, data table (sort, pagination, export button), chart wrapper, status badge, empty / loading / error states for every screen.

## Screens
1. **Overview** - KPI cards (month-to-date spend, forecast placeholder, budget status, identified savings), 12-month cost trend, top 5 services, **data freshness indicator** (last successful import, status), anomalies list.
2. **Cloud Connections** - list of providers (AWS active; Azure, GCP, OCI, Alibaba Cloud shown as "Planned"), connection health, "Connect AWS" wizard (steps: create read-only role with external ID, paste Role ARN, validate, choose export location, first sync), sync history table, troubleshooting panel.
3. **Cost Explorer** - filters: date, provider, account, service, region, tag, cost basis; stacked chart with group-by; drilldown table; saved views; export CSV.
4. **Allocation** - cost centers, tag-to-cost-center mapping rules, shared-cost split rules, **explicit "Unallocated" bucket** with percentage.
5. **Budgets & Alerts** - create budget (scope, amount, period, thresholds 50/80/100%), owners, notification channels, alert history.
6. **Recommendations** - table with evidence, estimated savings (range + confidence), risk, status workflow: Identified, Approved, Implemented, Verified. Detail drawer showing source of the recommendation.
7. **Reports** - saved reports, schedule (monthly/weekly), recipients, delivery history, "Executive monthly report" preview.
8. **Managed FinOps (MSP portfolio)** - visible only to MSP roles: customer portfolio table (spend under management, data freshness, open actions, savings register totals), engagement detail (assigned consultants, action register, review meetings, savings register by status).

(Administration - users, roles, audit log - is deferred; add only a placeholder nav item.)

## Deliverables
Source export, a README listing every route and every mock API function with its TypeScript types.
