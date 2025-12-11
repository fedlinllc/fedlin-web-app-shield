# Service Scope — Web App Shield

## In scope
- **DNS & TLS:** Cloudflare DNS with DNSSEC, TLS 1.3, HSTS, modern security headers (CSP, Referrer-Policy, etc.)
- **WAF & Abuse Controls:** Managed WAF rules + targeted custom rules, rate limiting, bot mitigation
- **Origin Lockdown:** Cloudflare Tunnel + mTLS and/or IP allowlists so the origin is not publicly reachable
- **Access Policies:** Country/ASN allow/deny lists and per-path rules for sensitive routes
- **Logging:** Logpush → S3/R2 (feeds VistaSec/SIEM)
- **IaC Delivery:** Terraform modules, GitHub Actions OIDC (no static secrets), change-controlled PRs
- **Evidence Bundle:** MANIFEST, before/after scans, console screenshots, plan/apply artifacts
- **Operational Guides:** Change control, DNS cutover, incident playbook

## Out of scope
- **Zero Trust Access:** Optional add-on (per-path RBAC for admin panels/SSH/RDP via IdP)
- **API Shield:** Optional add-on (mTLS and schema protections for APIs)
- **Cloudflare One:** Optional premium add-on (SWG/CASB/DLP)
- **24/7 monitoring / MDR:** Covered by VistaSec/CMC
- **Application-level security:** Code security, dependency scanning, SAST/DAST
- **Non-OIDC CI/CD patterns:** We standardize on GitHub Actions with OIDC
- **Multi-tenant MSP automation:** Standard baseline; MSP-specific automation is custom

