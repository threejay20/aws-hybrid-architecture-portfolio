
# Architecture

This project implements a credential-less CI/CD deployment pipeline using GitHub Actions and AWS OIDC to deploy static content to a private S3 bucket served through CloudFront.

The architecture is intentionally minimal while enforcing strong security boundaries and automation guarantees.

---

## High-Level Flow

GitHub Actions → AWS IAM (OIDC) → S3 (private) → CloudFront

A GitHub Actions workflow authenticates to AWS using OpenID Connect and assumes a tightly scoped IAM role. Deployment artifacts are synced to a private S3 bucket. CloudFront serves the content and handles caching.

---

## Components

### GitHub Actions
- Acts as the CI/CD control plane
- Triggers on commits to the `main` branch
- Uses OIDC to request short-lived AWS credentials
- Performs validation, deployment, and cache invalidation

### AWS IAM (OIDC)
- Trusts GitHub’s OIDC provider
- Issues short-lived credentials via STS
- Trust policy restricts access to:
  - Specific repository
  - Specific branch
- Permissions scoped to S3 and CloudFront only

### Amazon S3
- Stores static site content
- Public access fully blocked
- Accessible only through CloudFront using Origin Access Control (OAC)

### Amazon CloudFront
- Serves content globally
- Acts as the sole public entry point
- Optional cache invalidation triggered after deploys

---

## Design Characteristics

- No long-lived credentials
- Immutable deployments
- Least-privilege IAM
- Clear separation between control plane and runtime

This architecture favors security and operational simplicity over flexibility.
