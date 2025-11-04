Cloudflare Security Baseline — FEDLIN

Edge WAF & Zero Trust for any web app stack.
Harden the boundary with Cloudflare: managed WAF, DDoS mitigation, bot/rate controls, secure DNS/TLS/headers, origin lockdown via Tunnel/mTLS, and audit-ready evidence—delivered as Terraform + OIDC with change control baked in.

> Replaces our former “WordPress Site Security Hardening.” WordPress hardening is now an optional add-on under this baseline.

---

What this is
An opinionated, repeatable edge security baseline for websites and APIs on Cloudflare (WordPress, Next.js/Vercel, Shopify, custom apps, etc.). We implement protective controls at the edge, lock down the origin, and wire telemetry to your lake/SIEM—all as code, with a signed evidence pack at handoff.

Who it’s for
- Seed–Series B SaaS and SMBs that need SOC 2 / ISO 27001 / HIPAA-aligned guardrails fast.
- Teams that want edge security and Zero Trust without re-architecting the app.
- Agencies/MSPs needing a white-label, evidence-first baseline.

---

What you get (Baseline)
- DNS & TLS: Cloudflare DNS with DNSSEC, TLS 1.3, HSTS, modern security headers (CSP, Referrer-Policy, etc.).
- WAF & Abuse Controls: Managed WAF rules + targeted custom rules, rate limiting, bot mitigation.
- Origin Lockdown: Cloudflare Tunnel + mTLS and/or IP allowlists so the origin is not publicly reachable.
- Access Policies: Country/ASN allow/deny lists and per-path rules for sensitive routes.
- Logging: Logpush → S3/R2 (feeds VistaSec/SIEM).
- IaC Delivery: Terraform modules, GitHub Actions OIDC (no static secrets), change-controlled PRs.
- Evidence Bundle: MANIFEST, before/after scans, console screenshots, plan/apply artifacts.

> Results vary by application, but benchmarks (Mozilla Observatory, SSL Labs, SecurityHeaders) typically improve substantially after baseline.

Plus (optional add-ons)
- Zero Trust Access (per-path RBAC for admin panels/SSH/RDP via your IdP: Entra/Google).
- API Shield (mTLS and optional schema protections for APIs).
- Monthly WAF tuning and change-control PRs.
- VistaSec dashboard panels for Cloudflare telemetry.

Premium (optional add-ons)
- Cloudflare One integrations (SWG/CASB/DLP where appropriate).
- SIEM content handoffs, SLA response windows, quarterly attack-surface reviews, tabletop exercises.

---

How we deliver (Terraform + OIDC)
- Code-first: Terraform modules with sensible defaults; environment-scoped tfvars.
- Pipelines: GitHub Actions with OIDC to Cloudflare/S3—no long-lived secrets.
- Change control: Every change via PR; reviewers see plan/apply output and diff.
- Rollback: Documented, tested rollback steps per environment.
- Evidence: Signed MANIFEST with hashes, screenshots, scans, config exports.

/terraform/
  main.tf                # modules wired for the baseline
  variables.tf
  versions.tf
/modules/
  edge_waf/
  dns_tls_headers/
  tunnel_origin_lockdown/
  rate_bot_controls/
  zero_trust/            # optional
/envs/
  dev/terraform.tfvars
  prod/terraform.tfvars
/.github/workflows/
  apply.yml              # OIDC-only, no static secrets
/docs/
  service-brief.md
  runbooks/
    change-control.md
    dns-cutover.md
    incident-playbook.md
  evidence/
    MANIFEST.md
    README.md
    checks/
    screenshots/

---

Typical outcomes
- Security headers and TLS posture baselined (CSP/HSTS/Referrer-Policy, TLS1.3).
- Origin closed to the public internet (Tunnel/mTLS/allowlists).
- WAF/bot/rate policies active and tuned for critical paths.
- Telemetry flowing to S3/R2 (and optionally VistaSec/SIEM).
- PR-driven changes with audit trail and rollback plan.

---

Acceptance criteria (handoff checklist)
- [ ] Domain hosted in Cloudflare with DNSSEC enabled and verified.
- [ ] HSTS + modern TLS enabled; headers scan shows CSP and core headers present.
- [ ] Managed WAF on; targeted rules for admin/API routes; rate limits applied.
- [ ] Origin restricted via Tunnel/mTLS and/or IP allowlists; direct ingress blocked.
- [ ] Logpush to S3/R2 configured; sample files validated; retention documented.
- [ ] Terraform + OIDC pipeline in place; latest plan/apply artifacts stored.
- [ ] Evidence pack delivered (MANIFEST, scans, screenshots, diffs, runbooks).

---

Evidence bundle (audit-ready)
- MANIFEST.md with file hashes and sources.
- Terraform plan/apply outputs (sanitized).
- Exports/screenshots of WAF, rate limits, headers/TLS settings.
- Before/after headers/TLS scan reports; WAF hit samples.
- Logpush samples + retention notes.
- Runbooks: change control, DNS cutover, incident playbook.

---

Quick start (clients)

Prerequisites
- Cloudflare account (Pro/Business/Enterprise as required by scope).
- Registrar access to change nameservers (or confirm already pointing to Cloudflare).
- Origin details (IPs/hostnames/ports), admin paths, API endpoints.
- S3/R2 bucket for Logpush (we can provision).
- IdP groups (Entra/Google) if enabling Zero Trust Access.

Engagement flow
1. Discovery & scope (domains/subdomains, app traits, admin/API paths, traffic profile).
2. Prepare repos & OIDC (we create deployment repo and pipeline).
3. Implement baseline (Terraform apply in staging → validate → prod).
4. DNS cutover (change window; monitor; rollback plan documented).
5. Tuning + evidence (WAF/rate adjustments; deliver evidence pack).

---

FAQs

Will this break my site?
We roll out in monitor → block mode with a rollback plan and change window. Most breakage risks come from aggressive WAF rules or strict CSP; we tune with you.

Do I need to move my domain registrar?
No. You can keep GoDaddy/other; we just point nameservers to Cloudflare.

Is WordPress covered?
Yes. Platform-agnostic baseline. Optional WordPress Hardening Add-On includes plugin policy, updates cadence, and file permission checks.

HIPAA / BAA?
We scope Cloudflare services to those appropriate for regulated workloads and document logging/retention paths. For Enterprise/BAA, we align features accordingly.

---

Compliance alignment (examples)
- SOC 2: CC6/7 boundary protection, CC8 monitoring, CC5 change control.
- ISO 27001: A.8 (asset), A.12 (ops), A.13 (communications), A.14 (system acquisition), A.16 (incidents).
- HIPAA: 164.312 (technical safeguards), 164.308/310 (admin/physical in practice via process & evidence).

(We provide control mapping in the evidence pack; this repo avoids exhaustive mappings by design.)

---

Limitations / notes
- We avoid hard guarantees like “A+ in hours.” We set targets, verify with scans, and document residual risks.
- CSP reduces inline-script XSS significantly when using nonces/hashes, but residual risks can remain depending on app code and 3rd-party scripts.
- Some features (e.g., advanced Zero Trust, API Shield options) may require Business/Enterprise plans.

---

Related FEDLIN services
- VistaSec (AWS Continuous Monitoring Center)
- AWS / Microsoft 365 / Google Workspace Baselines
- DMARC / SPF / DKIM Baseline
- Linux Device Reimaging Baseline

---

Contact / Request a demo
Want the baseline applied to your environment (with evidence pack)? Request a demo and we’ll scope your domains, set targets, and schedule a safe cutover.
