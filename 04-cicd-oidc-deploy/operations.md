# Operations

This project is designed for low operational overhead with clear visibility into deployment activity.

---

## Deployment Triggers

- Automatic on push to `main`
- No manual approval steps required
- Idempotent execution

---

## Observability

- GitHub Actions logs provide full deployment traceability
- Each workflow run shows:
  - Authentication
  - Validation
  - Sync status
  - Cache invalidation (if enabled)

AWS-side observability is minimal by design due to static content and managed services.

---

## Failure Handling

- Validation failures stop deployments early
- Failed syncs do not impact existing content
- CloudFront invalidation failures do not block deploys

Previously deployed content remains available unless explicitly replaced.

---

## Rollback Strategy

- Rollback is performed via Git history
- Reverting a commit triggers a redeploy
- No infrastructure changes required for rollback

---

## Maintenance

- No credential rotation
- No servers to patch
- Minimal AWS configuration drift

This project is safe to leave running with near-zero ongoing maintenance.

