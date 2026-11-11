# Threat model (skeleton)
Assets: customer billing data, cloud role ARNs/external IDs, user sessions, reports/exports.
Threats to test: IDOR across tenants, MSP over-delegation, export leakage, worker without tenant scope, confused-deputy on AWS role (external ID), secret leakage, runaway Athena scans, replayed import files.
Each threat -> control -> test ID (to be filled by Test agent).
