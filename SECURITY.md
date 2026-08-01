# Security and confidentiality

This repository is a public-safe architecture case study. It excludes real data, financial values, tenant and workspace identifiers, organization branding, production PBIX/PBIR files, credentials, and proprietary calculations.

## Production control model

The following controls are design requirements, not claims that this public repository deploys or verifies them:

- Entra ID groups provide role-based workspace and app access; named-user grants are exceptions with expiry.
- Workspace authorization and semantic-model data authorization are reviewed separately.
- Build permission is restricted because it enables downstream analysis beyond the published report experience.
- RLS and OLS use deny-by-default test personas, including negative and export scenarios.
- Service identities use least privilege, managed secrets, and auditable ownership.
- Sensitivity labels, export/download restrictions, external sharing, and app audiences follow data classification.
- Audit logs feed periodic access reviews and incident investigation.
- AI-insight and custom visuals require privacy, tenant-policy, data-egress, reconciliation, and fallback review.

## Public-release checklist

Before publication, scan changed files and Git history for credentials, tokens, email addresses, organization names, GUIDs, Fabric endpoints, report links, real screenshots, real values, and downloadable BI artifacts. Use synthetic names and values only.

## Reporting

Please report suspected sensitive content privately to the repository owner. Do not open a public issue containing the suspected material.
