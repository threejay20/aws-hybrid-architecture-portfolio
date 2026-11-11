# AWS Hybrid Architecture Portfolio (Solutions Architect + DevOps)

Four AWS builds, each documented the way a team would hand it over: architecture, operations and teardown notes, with decision records for the key trade-offs. Built and tested in a live AWS account, with screenshots as evidence.

Part of my portfolio: [threejay20.github.io](https://threejay20.github.io)

## Highlights

- **No stored AWS credentials.** GitHub Actions deploys through OpenID Connect (OIDC) and a scoped IAM role.
- **Private origin.** S3 stays private with Block Public Access on, and CloudFront reaches it through Origin Access Control.
- **Failure is designed in.** Messages are retried, then moved to a dead-letter queue so bad messages are kept for inspection.
- **Trade-offs written down.** Decision records cover Lambda vs EC2 and DynamoDB vs RDS.
- **No idle compute.** Every build is pay-per-use, and every build has teardown steps.

## Builds

| Build | What it shows | AWS services |
| --- | --- | --- |
| [01 - Serverless API](01-serverless-api) | A REST API for managing tasks (GET, POST, PUT, DELETE) with a least-privilege Lambda execution role | API Gateway, Lambda, DynamoDB, CloudWatch |
| [02 - Event-Driven Architecture](02-event-driven-architecture) | SNS fanout, SQS buffering and a Lambda consumer, with retries and a dead-letter queue | SNS, SQS, Lambda |
| [03 - Static Site + CDN](03-static-site-cdn) | Global delivery of a static site from a private S3 bucket | S3, CloudFront (OAC) |
| [04 - CI/CD with OIDC](04-cicd-oidc-deploy) | Push-to-deploy pipeline with sanity checks, S3 sync and CloudFront invalidation, no long-lived credentials | GitHub Actions, IAM (OIDC), S3, CloudFront |

Each build folder has a README, architecture notes, operations notes and teardown steps.

## Decision Records (ADRs)

- [ADR-001: Lambda vs EC2](01-serverless-api/decision-records/adr-001-lambda-vs-ec2.md)
- [ADR-002: DynamoDB vs RDS](01-serverless-api/decision-records/adr-002-dynamodb-vs-rds.md)

## Notes

- The deployment workflow lives in `.github/workflows/project-04-deploy.yml`.
- Build 04 includes an infrastructure-as-code template in `04-cicd-oidc-deploy/iac/` that shows how the deployment could be provisioned as code. The live resources were created manually, to keep the focus on architecture and security configuration.

## More Work

- [Azure Terraform pipeline with OIDC](https://github.com/threejay20/azure-tf-oidc-lab)
- [Spring Boot service to production (Java, Helm, Kubernetes, Kafka)](https://github.com/threejay20/spring-boot-devops-lab)
- [LLMOps reference platform](https://github.com/threejay20/homelab-ai-stack)
