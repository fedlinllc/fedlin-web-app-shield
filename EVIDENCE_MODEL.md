# Evidence Model (Public-Safe)

| Area | Evidence Source | Lives in | Notes |
|------|-----------------|----------|-------|
| DNS & DNSSEC | Cloudflare DNS console | Customer Cloudflare | Proves DNS security and DNSSEC enabled |
| TLS & Headers | Security scan reports (Mozilla Observatory, SSL Labs, SecurityHeaders) | Customer S3/R2 | Proves TLS 1.3, HSTS, CSP, and security headers |
| WAF Rules | Cloudflare WAF console exports | Customer S3/R2 | Proves WAF rules configured and active |
| Rate Limits | Cloudflare rate limiting console | Customer Cloudflare | Proves rate limiting policies applied |
| Tunnel Config | Cloudflare Tunnel configuration | Customer GitHub | Proves origin lockdown via Tunnel |
| Logpush | Logpush sample files | Customer S3/R2 | Proves logging configured and flowing |
| Terraform State | Terraform plan/apply outputs | Customer GitHub | Proves infrastructure as code deployment |
| CI Baseline | GitHub Actions run logs | Customer GitHub | Proves OIDC-only delivery |

> FEDLIN does **not** store customer Cloudflare exports or sensitive configuration in this public repo.

