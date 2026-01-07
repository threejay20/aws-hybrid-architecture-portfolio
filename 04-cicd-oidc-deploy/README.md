# Project 04 — CI/CD with GitHub Actions (OIDC to AWS)

## Overview

This project implements a secure, credential-less CI/CD pipeline using GitHub Actions and AWS OIDC to deploy a static site to a private S3 bucket behind CloudFront.

The goal is to demonstrate a modern deployment model that avoids long-lived credentials, enforces least-privilege access, and supports automated, repeatable deployments triggered directly from version control.

---

## Architecture Summary

GitHub Actions → AWS IAM (OIDC) → S3 (private) → CloudFront

- GitHub Actions authenticates to AWS using OpenID Connect (OIDC)
- No static AWS credentials are stored in GitHub
- IAM role trust policy restricts who can assume the role
- Deployment syncs site assets to a private S3 bucket
- CloudFront serves content and handles cache invalidation

---

## Authentication Model (OIDC)

Authentication is handled using GitHub’s OIDC provider (`token.actions.githubusercontent.com`).

Key characteristics:

- No access keys or secrets stored in GitHub
- Short-lived credentials issued by AWS STS
- Role assumption restricted to:
  - This repository
  - The `main` branch
- Blast radius limited by IAM policy scope

This removes the risk associated with leaked or over-privileged CI/CD credentials.

---

## Deployment Flow

1. Code is pushed to the `main` branch
2. GitHub Actions workflow starts automatically
3. Workflow requests a short-lived AWS session via OIDC
4. Sanity checks validate deployment artifacts
5. Static site contents are synced to a private S3 bucket
6. CloudFront cache is invalidated (if configured)
7. Deployment completes with no manual intervention

All steps are idempotent and safe to re-run.

---

## Security Posture

- S3 bucket:
  - Block Public Access enabled
  - Access allowed only via CloudFront Origin Access Control (OAC)
- IAM role:
  - Assumable only via GitHub OIDC
  - Scoped to required S3 and CloudFront actions
- GitHub:
  - No stored AWS secrets
  - Trust restricted to repository and branch

The deployment pipeline itself forms part of the security boundary.

---

## Operational Characteristics

- Fully automated deployments
- No manual credential rotation
- Fast rollback via Git history
- Deterministic behavior across runs
- Minimal ongoing maintenance

Failures surface immediately in GitHub Actions logs and do not impact previously deployed content.

---

## Failure Modes and Handling

- **Sanity check failure**  
  Deployment stops before any AWS changes occur.

- **S3 sync failure**  
  No partial state is committed; previously deployed content remains live.

- **CloudFront invalidation failure**  
  Content still deploys; cache naturally expires.

Each failure mode is isolated and observable.

---

## Cost Profile

- GitHub Actions: free tier sufficient
- IAM / OIDC: no cost
- S3 static hosting: negligible
- CloudFront: free tier or minimal cost for low traffic

This architecture is safe to leave running continuously.

---

## Repository Structure

04-cicd-oidc-deploy/
├── README.md
├── project-04-deploy.yml
├── architecture.md
├── operations.md
├── security.md
├── teardown.md
├── iac/
└── assets/project-04-cicd-oidc/


---

## Status

Deployed and validated.

- OIDC authentication confirmed
- GitHub Actions deployment succeeds
- Private S3 + CloudFront serving content
- No static credentials in use

---

## Future Improvements

- Add environment separation (dev / prod)
- Introduce policy linting or IAM analysis
- Add build artifact integrity checks
- Expand to multi-account deployments
- Integrate monitoring for deployment frequency and failure rate

