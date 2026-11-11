# ADR-001: Tenancy and MSP delegation model
**Status:** PROPOSED - requires owner approval (auth/tenancy is a human-approval area)
**Date:** 2026-11-11

## Context
Customers must see only their own data. MSP consultants (ScaleCloudX) must work across many customers, only where explicitly authorized. Retrofitting this later is where leaks happen.

## Proposed model
- `organizations` (type: customer | msp). A customer org owns cloud connections, cost data, budgets, reports.
- `msp_relationships` (msp_org_id, customer_org_id, status, start/end) - customer-granted trust, revocable.
- `engagements` (msp_relationship_id, scope, services) and `engagement_assignments` (user_id, role, expires_at) - consultant access is derived from assignments.
- `memberships` (user_id, org_id, role) for direct members.
- **Tenant scope is computed server-side per request**: set of customer_org_ids = direct memberships + active assignments. Never accepted from the client.
- Every tenant-owned table has `customer_org_id`. Postgres Row-Level Security uses a per-request setting (`app.allowed_org_ids`) as a second layer beneath application checks.
- Background workers receive a single customer_org_id per job and set it before any query.
- Exports and reports re-check scope at generation and at download.
- All cross-org access writes an `audit_events` row (actor, customer, action, time).

## Required tests (G1)
IDOR on every endpoint; consultant with expired/revoked assignment; consultant of customer A reading customer B; worker job with wrong org; export link reuse by another user; RLS bypass attempt with app check disabled.

## Alternatives considered
Schema-per-tenant (heavier ops for solo founder); DB-per-tenant (cost). Revisit if a regulated customer requires physical isolation.

## Open questions
Do any prospects require data segregation per country? Does MSP need customer-visible audit of consultant activity (recommended: yes)?
