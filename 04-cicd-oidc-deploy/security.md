# Security

Security is enforced at every layer of the deployment pipeline, with a strong emphasis on credential elimination and access minimization.

---

## Authentication

- GitHub Actions authenticates using OpenID Connect (OIDC)
- AWS issues short-lived credentials via STS
- No AWS access keys are stored in GitHub

The IAM role trust policy restricts assumption to:
- This repository
- The `main` branch only

---

## Authorization

The IAM role permissions are scoped to:
- Sync objects to a specific S3 bucket path
- Optionally invalidate a specific CloudFront distribution

No wildcard permissions are granted beyond what is operationally required.

---

## S3 Security

- Block Public Access enabled
- Bucket policy allows access only from CloudFront
- No direct public object access

S3 is treated as a private origin, not a hosting endpoint.

---

## CloudFront Security

- Acts as the public boundary
- Uses Origin Access Control (OAC) to access S3
- Prevents direct bucket access even if object URLs are known

---

## CI/CD Boundary

The deployment pipeline itself is part of the security model:
- Credentials are ephemeral
- Access is time-bound
- Compromise impact is limited by role scope

This reduces both attack surface and credential management overhead.

