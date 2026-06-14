# Qualys GraphQL Schema

## Overview

This conceptual GraphQL schema models the Qualys cloud security platform, covering its major product areas: Vulnerability Management Detection and Response (VMDR), Policy Compliance, Web Application Scanning (WAS), Container Security, Certificate View, Cloud Agent, and Cloud Security Posture Management (CSPM).

The schema is derived from the Qualys REST/XML API surface documented in the Qualys API VMPC User Guide and related product API references. Qualys does not currently publish a native GraphQL endpoint; this schema represents a normalized, unified view of the platform data model that could be exposed via a GraphQL layer over the existing REST APIs.

## Source APIs

- **VMDR API** — `https://qualysapi.qualys.com/api/2.0/` — asset inventory, scans, vulnerabilities, reports
- **Authentication API** — `https://gateway.qg1.apps.qualys.com/auth` — JWT tokens for newer APIs
- **Policy Compliance API** — controls, frameworks, compliance scans, reports
- **Web Application Scanning API** — web apps, WAS scans, web vulnerability findings
- **Container Security API** — container images, registries, container vulnerabilities
- **Certificate View API** — certificates, internal/external CAs
- **Cloud Agent API** — agent inventory, agent details, agent configuration
- **CSPM / TotalCloud API** — cloud accounts, cloud resource posture

## Authentication Model

The Qualys platform supports two authentication schemes:

1. **HTTP Basic Auth** — username and password sent with every request; used by VMDR, Policy Compliance, WAS, and legacy APIs.
2. **JWT Bearer Token** — obtained from the Authentication API (`POST /auth`) and passed as `Authorization: Bearer <token>`; used by VMDR OT, CSAM, and TotalCloud APIs.

In the GraphQL schema, authentication context is represented via the `APIUser`, `APIKey`, and `Token` types.

## Schema Highlights

### Asset Management
- `Asset`, `AssetDetails`, `AssetTag`, `AssetGroup` — inventory objects representing hosts and their groupings
- `IPAddress`, `IPRange` — network address primitives
- `HostDetails`, `NetworkInterface`, `OperatingSystem`, `Software`, `Port`, `Service` — host profile sub-objects

### Scanning
- `Scanner`, `ScannerType` — physical and virtual scanner appliances
- `ScanTarget`, `Scan`, `ScanDetails`, `ScanStatus`, `ScanResults`, `ScanSchedule` — full scan lifecycle

### Vulnerability Knowledge Base
- `Vulnerability`, `VulnDetails`, `CVE`, `CVSS`, `KnowledgeBase`, `QID` — Qualys-native vulnerability records
- `Risk`, `Severity`, `Threat`, `Exploit`, `Remediation` — prioritization and response context

### Policy Compliance
- `Compliance`, `Control`, `Framework`, `ComplianceReport`, `ComplianceScan` — CIS, DISA STIG, PCI-DSS, and custom frameworks
- `Policy`, `PolicyRule`, `PolicyCompliance` — policy definition and host-level compliance state

### Web Application Scanning
- `WAS`, `WebApp`, `WebAppScan`, `WebAppVuln`, `WASFindings` — web app inventory and scan results

### Container Security
- `ContainerSecurity`, `Container`, `ContainerImage`, `ContainerRegistry` — container and image vulnerability management

### Certificate View
- `CertificateView`, `Certificate`, `InternalCA`, `ExternalCA` — SSL/TLS certificate inventory

### Cloud Agent
- `CloudAgent`, `AgentDetails`, `Platform` — installed agent inventory and platform metadata

### CSPM
- `CSPM`, `CloudAccount` — cloud account posture and misconfiguration findings

### Access Control
- `APIUser`, `APIKey`, `Token`, `Webhook` — platform users, credentials, and event notifications

## GraphQL File

See `qualys-schema.graphql` for the full type definitions.

## References

- Qualys API Documentation: https://docs.qualys.com
- VMDR API User Guide: https://cdn2.qualys.com/docs/qualys-api-vmpc-user-guide.pdf
- API Quick Reference: https://cdn2.qualys.com/docs/qualys-api-quick-reference.pdf
- Platform Pod URLs: https://www.qualys.com/platform-identification/
- Qualys API Framework: https://docs.qualys.com/en/vmdr-mobile/api/get_started/qualys_api_framework.htm
