# Delivery Model — Web App Shield

1. **Access prep** — customer creates Cloudflare API token with appropriate scopes and configures GitHub OIDC for Cloudflare/S3.
2. **Service deployment** — FEDLIN runs/guides Web App Shield deployment to enable WAF, DNS/TLS hardening, Tunnel, and security headers.
3. **Evidence capture** — evidence is stored in the **customer** S3/R2 bucket and GitHub repository.
4. **Handoff** — customer/MSP receives scope + evidence model + runbooks.
5. **(Optional)** customer schedules periodic GitHub Action re-runs for ongoing change control.

**Why OIDC?**
- No long-lived Cloudflare API tokens in CI
- Easy to rotate/revoke from Cloudflare side
- Cleaner story for auditors
- S3/R2 access via OIDC eliminates static credentials

