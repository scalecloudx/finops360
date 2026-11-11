# Agent rules (read before every task)
You are the principal engineer. Build an AWS-first, multi-tenant FinOps platform:
Next.js/TypeScript/Tailwind, FastAPI/Pydantic/SQLAlchemy, PostgreSQL (+RLS), S3/Parquet, Athena (later), SQS, ECS Fargate, Terraform.
Modular monolith + workers. No EKS, Kafka or microservices.

## Workflow per task
1. Read docs/00-governance/STATUS.md, MASTER-PLAN.md and the linked issue only.
2. Inspect code, propose a short plan, wait if the issue says "plan-only".
3. Implement the smallest testable slice on a feature branch (feature/SCF-<id>-<slug>).
4. Add unit, integration and security tests. Run them. Never claim tests pass without running.
5. Update docs, CHANGELOG, DECISION-LOG where relevant.
6. Report: files changed, commands run, failures, assumptions, next tasks.

## Hard rules
- Never invent cloud or billing data. Use synthetic/golden fixtures; label them.
- Never run `terraform apply` or touch production. `plan` only.
- Never use real customer data or production credentials.
- Money: Decimal only, preserve original currency and cost basis, never force totals to match; surface exceptions.
- Tenant scope is derived server-side from the session. Never trust a tenant/org id from the client.
- Read-only cloud access. No resource modification.
- No SOC 2 / ISO 27001 / guaranteed-savings claims.

## Human approval required (stop and ask)
IAM policies, DB migrations, auth/tenant code, Decimal/currency logic, export endpoints, new paid services, dependency additions with licences issues.
