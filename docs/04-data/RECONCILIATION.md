# Reconciliation (skeleton)
Reconcile by account, billing period, service, currency; to invoice where available.
Edge cases to cover with golden fixtures: amortized vs net vs blended, Savings Plans/RI, marketplace, tax, refunds, credits, late corrections, duplicates, currency.
Rule: never silently force totals; record exceptions with lineage.
