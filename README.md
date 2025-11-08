# FEDLIN – Web App Shield

[![Terraform](https://img.shields.io/badge/IaC-Terraform_5.0+-623CE4?logo=terraform)](https://www.terraform.io/)
[![Cloudflare](https://img.shields.io/badge/Cloud-Cloudflare-F38020?logo=cloudflare)](https://www.cloudflare.com/)
[![ISO 27001](https://img.shields.io/badge/ISO%2027001-Mapped-1f77b4)](#compliance-coverage)
[![SOC 2](https://img.shields.io/badge/SOC%202-Mapped-d62728)](#compliance-coverage)
[![HIPAA](https://img.shields.io/badge/HIPAA-Mapped-9467bd)](#compliance-coverage)
[![Maintained](https://img.shields.io/badge/Maintained-Yes-green)](#)

**Edge WAF & Zero Trust for any web app stack**

Harden the boundary with Cloudflare: managed WAF, DDoS mitigation, bot/rate controls, secure DNS/TLS/headers, origin lockdown via Tunnel/mTLS, and audit-ready evidence—delivered as Terraform + OIDC with change control baked in.

> Replaces our former "WordPress Site Security Hardening." WordPress hardening is now an optional add-on under Web App Shield.

[📧 Contact](mailto:info@fedlin.com) · [📞 Book Consultation](https://calendar.app.google/7z8eAZPvrW82jtxk6) · [🌐 fedlin.com](https://www.fedlin.com)

---

## 🎯 What This Delivers

An opinionated, repeatable edge security baseline for websites and APIs on Cloudflare (WordPress, Next.js/Vercel, Shopify, custom apps, etc.). We implement protective controls at the edge, lock down the origin, and wire telemetry to your lake/SIEM—all as code, with a signed evidence pack at handoff.

**Designed for:**
- **Seed–Series B SaaS and SMBs** that need SOC 2 / ISO 27001 / HIPAA-aligned guardrails fast
- **Teams** that want edge security and Zero Trust without re-architecting the app
- **Agencies/MSPs** needing a white-label, evidence-first baseline

**Key capabilities:**
- DNS & TLS hardening with DNSSEC, TLS 1.3, HSTS, modern security headers
- WAF & abuse controls (managed rules + custom rules, rate limiting, bot mitigation)
- Origin lockdown via Cloudflare Tunnel + mTLS/IP allowlists
- Access policies (country/ASN filtering, per-path rules)
- Logging integration (Logpush → S3/R2 → VistaSec/SIEM)
- Terraform + OIDC deployment (zero long-lived credentials)
- Audit-ready evidence bundle

---

## 🏗️ Security Services Configured

### Cloudflare Edge Security

| Service | Purpose | Evidence Output |
|---------|---------|-----------------|
| **DNS & DNSSEC** | Domain security and DNS integrity | DNSSEC verification, DNS records |
| **TLS & Security Headers** | TLS 1.3, HSTS, CSP, Referrer-Policy, etc. | Before/after scan reports, header analysis |
| **Managed WAF** | Web application firewall rules | WAF rule configurations, hit samples |
| **Custom WAF Rules** | Targeted protection for admin/API routes | Rule definitions, evaluation logs |
| **Rate Limiting** | Abuse prevention and DDoS mitigation | Rate limit policies, violation logs |
| **Bot Management** | Automated bot detection and mitigation | Bot scores, challenge logs |
| **Cloudflare Tunnel** | Origin lockdown (no public ingress) | Tunnel configurations, connection logs |
| **mTLS** | Mutual TLS authentication | Certificate policies, connection logs |
| **Zero Trust Access** | Per-path RBAC via IdP (optional) | Access policies, session logs |
| **Logpush** | Centralized logging (S3/R2) | Log samples, retention policies |

### Modular Terraform Architecture

```
terraform/
├── modules/
│   ├── edge_waf/              # WAF rules and custom policies
│   ├── dns_tls_headers/       # DNS, TLS, security headers
│   ├── tunnel_origin_lockdown/ # Tunnel + mTLS configuration
│   ├── rate_bot_controls/      # Rate limiting and bot management
│   └── zero_trust/            # Zero Trust Access (optional)
├── main.tf                     # Orchestration
├── variables.tf
└── versions.tf
envs/
├── dev/terraform.tfvars
└── prod/terraform.tfvars
.github/workflows/
└── apply.yml                   # OIDC-only, no static secrets
docs/
├── service-brief.md
├── runbooks/
│   ├── change-control.md
│   ├── dns-cutover.md
│   └── incident-playbook.md
└── evidence/
    ├── MANIFEST.md
    ├── README.md
    ├── checks/
    └── screenshots/
```

**Configuration-driven deployment:**
- Terraform modules with sensible defaults
- Environment-scoped tfvars
- GitHub Actions with OIDC (no long-lived secrets)
- Change-controlled PRs with plan/apply artifacts

---

## 📊 Compliance Framework Coverage

### Security Controls Mapping

**SOC 2 Trust Services:**
- CC6.1/CC6.7: Boundary protection (WAF, Tunnel, mTLS)
- CC7.2: System monitoring and logging (Logpush, telemetry)
- CC7.4: Security incident detection (WAF alerts, bot detection)
- CC5.2: Change control (PR-driven, Terraform plan/apply)

**ISO 27001 Controls:**
- A.8 (Asset Management): DNS/TLS configuration tracking
- A.12 (Operations Security): Logging, monitoring, change control
- A.13 (Communications Security): TLS 1.3, security headers, Tunnel
- A.14 (System Acquisition): Secure deployment practices
- A.16 (Incident Management): WAF/rate limit alerts, incident playbooks

**HIPAA Security Rule:**
- §164.312(a)(2)(i): Access controls (Zero Trust, mTLS)
- §164.312(b): Audit controls (Logpush, Cloudflare logs)
- §164.312(e)(1): Transmission security (TLS 1.3, mTLS)

> Results vary by application, but benchmarks (Mozilla Observatory, SSL Labs, SecurityHeaders) typically improve substantially after baseline.

(We provide detailed control mapping in the evidence pack; this repo avoids exhaustive mappings by design.)

---

## 🔒 What You Get

### Baseline (Core Service)

**DNS & TLS:**
- Cloudflare DNS with DNSSEC enabled and verified
- TLS 1.3 with modern cipher suites
- HSTS with appropriate max-age
- Security headers (CSP, Referrer-Policy, X-Frame-Options, etc.)

**WAF & Abuse Controls:**
- Managed WAF rules enabled
- Targeted custom rules for admin/API routes
- Rate limiting configured
- Bot mitigation active

**Origin Lockdown:**
- Cloudflare Tunnel configured (origin not publicly reachable)
- mTLS and/or IP allowlists enforced
- Direct ingress blocked

**Logging & Telemetry:**
- Logpush → S3/R2 configured
- Sample files validated
- Retention documented
- Integration with VistaSec/SIEM (optional)

**Infrastructure as Code:**
- Terraform modules with sensible defaults
- GitHub Actions with OIDC (no static secrets)
- Change-controlled PRs with plan/apply output
- Documented rollback procedures

**Evidence Bundle:**
- MANIFEST.md with file hashes and sources
- Terraform plan/apply outputs (sanitized)
- Exports/screenshots of WAF, rate limits, headers/TLS settings
- Before/after headers/TLS scan reports
- WAF hit samples
- Logpush samples + retention notes
- Runbooks (change control, DNS cutover, incident playbook)

### Plus (Optional Add-Ons)

- **Zero Trust Access:** Per-path RBAC for admin panels/SSH/RDP via your IdP (Entra/Google)
- **API Shield:** mTLS and optional schema protections for APIs
- **Monthly WAF Tuning:** Ongoing tuning and change-control PRs
- **VistaSec Dashboard:** Custom panels for Cloudflare telemetry

### Premium (Optional Add-Ons)

- **Cloudflare One:** SWG/CASB/DLP integrations where appropriate
- **SIEM Content:** Handoff packages for your SIEM
- **SLA Response Windows:** Defined response times for incidents
- **Quarterly Reviews:** Attack-surface reviews and tabletop exercises

---

## 🎯 Typical Outcomes

**Security Posture:**
- Security headers and TLS posture baselined (CSP/HSTS/Referrer-Policy, TLS 1.3)
- Origin closed to the public internet (Tunnel/mTLS/allowlists)
- WAF/bot/rate policies active and tuned for critical paths
- Telemetry flowing to S3/R2 (and optionally VistaSec/SIEM)

**Operational Excellence:**
- PR-driven changes with audit trail and rollback plan
- Terraform + OIDC pipeline in place
- Latest plan/apply artifacts stored
- Evidence pack delivered and validated

---

## 📋 Acceptance Criteria (Handoff Checklist)

- [ ] Domain hosted in Cloudflare with DNSSEC enabled and verified
- [ ] HSTS + modern TLS enabled; headers scan shows CSP and core headers present
- [ ] Managed WAF on; targeted rules for admin/API routes; rate limits applied
- [ ] Origin restricted via Tunnel/mTLS and/or IP allowlists; direct ingress blocked
- [ ] Logpush to S3/R2 configured; sample files validated; retention documented
- [ ] Terraform + OIDC pipeline in place; latest plan/apply artifacts stored
- [ ] Evidence pack delivered (MANIFEST, scans, screenshots, diffs, runbooks)

---

## 💻 Infrastructure Efficiency

**Typical Cloudflare costs:**
- Pro plan: $20/month per domain (covers baseline features)
- Business plan: $200/month per domain (advanced WAF, Zero Trust)
- Enterprise: Custom pricing (BAA, advanced features)

**Deployment metrics:**
- Terraform resources: 40-80 (depends on modules enabled)
- Deployment time: 3-5 business days post-access
- Evidence retention: 7 years (configurable)
- Multi-domain: Supported via Terraform modules

---

## 🤝 Engagement Models

**Direct Deployment**  
Complete Web App Shield setup for your domains with documentation and training.

**MSP Partnership**  
Standardized Web App Shield deployment across your managed client accounts.

**Consulting Business Services**  
FEDLIN operates as an independent consulting firm, open to contract and C2C engagements for Cloudflare security architecture and compliance automation projects.

---

## 🚀 Quick Start (Clients)

### Prerequisites

- Cloudflare account (Pro/Business/Enterprise as required by scope)
- Registrar access to change nameservers (or confirm already pointing to Cloudflare)
- Origin details (IPs/hostnames/ports), admin paths, API endpoints
- S3/R2 bucket for Logpush (we can provision)
- IdP groups (Entra/Google) if enabling Zero Trust Access

### Engagement Flow

1. **Discovery & Scope:** Domains/subdomains, app traits, admin/API paths, traffic profile
2. **Prepare Repos & OIDC:** We create deployment repo and pipeline
3. **Implement Web App Shield:** Terraform apply in staging → validate → prod
4. **DNS Cutover:** Change window; monitor; rollback plan documented
5. **Tuning + Evidence:** WAF/rate adjustments; deliver evidence pack

---

## ❓ FAQs

**Will this break my site?**  
We roll out in monitor → block mode with a rollback plan and change window. Most breakage risks come from aggressive WAF rules or strict CSP; we tune with you.

**Do I need to move my domain registrar?**  
No. You can keep GoDaddy/other; we just point nameservers to Cloudflare.

**Is WordPress covered?**  
Yes. Platform-agnostic service. Optional WordPress Hardening Add-On includes plugin policy, updates cadence, and file permission checks.

**HIPAA / BAA?**  
We scope Cloudflare services to those appropriate for regulated workloads and document logging/retention paths. For Enterprise/BAA, we align features accordingly.

---

## ⚠️ Limitations / Notes

- We avoid hard guarantees like "A+ in hours." We set targets, verify with scans, and document residual risks.
- CSP reduces inline-script XSS significantly when using nonces/hashes, but residual risks can remain depending on app code and 3rd-party scripts.
- Some features (e.g., advanced Zero Trust, API Shield options) may require Business/Enterprise plans.

---

## 📞 Get Started

**Primary Contact:** [info@fedlin.com](mailto:info@fedlin.com)  
**Book Consultation:** [Google Calendar](https://calendar.app.google/7z8eAZPvrW82jtxk6) or [Arrangr](https://arrangr.com/fedlin)  
**Demo:** Available upon request

### Related FEDLIN Services

- **[AWS Security Baseline](https://github.com/fedlinllc/fedlin-aws-security-baseline)** - AWS security hardening
- **[AWS VistaSec/CMC](https://github.com/fedlinllc/fedlin-aws-vistasec-cmc)** - Continuous monitoring center
- **[M365 Security Baseline](https://github.com/fedlinllc/fedlin-m365-security-baseline)** - Microsoft 365 hardening
- **[Google Workspace HIPAA](https://github.com/fedlinllc/fedlin-gws-hipaa-baseline)** - GWS compliance
- **[DMARC/SPF/DKIM](https://github.com/fedlinllc/fedlin-dmarc-spf-dkim)** - Email authentication

---

## 📋 Repository Note

This repository describes the Web App Shield service and architecture approach. Deployment assets (Terraform modules, configuration templates, automation workflows) are provided as part of paid engagements.

**FEDLIN LLC**  
Security Solutions Architecture · Vulnerability Management · Compliance Automation  
Independent · Contract/C2C · Customer-tenant-first