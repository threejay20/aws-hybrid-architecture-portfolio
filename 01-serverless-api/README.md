# 01 – Serverless API (API Gateway + Lambda + DynamoDB)



## Overview
This project demonstrates a fully serverless REST API built on AWS,
optimized for zero idle cost and automatic scaling.

## Architecture
Client → API Gateway → Lambda → DynamoDB

## Architecture Diagram
<img width="1536" height="1024" alt="diagram" src="https://github.com/user-attachments/assets/0a2625e9-7cd2-4ff6-947f-7925f73e5907" />

## Why this design
- Serverless eliminates server management and scales automatically.
- DynamoDB avoids capacity planning and idle database costs.
- HTTP API keeps the solution simple and cost-efficient.

## Security considerations
- Lambda execution role uses least-privilege IAM policies.
- No hardcoded credentials.
- TLS enforced by API Gateway.

## Cost considerations
- Designed to remain within AWS Free Tier.
- No long-running compute resources.
- Resources are torn down after validation.

## Operations
- CloudWatch used for logs and basic metrics.
- Errors and latency observable via Lambda metrics.

## Teardown
All resources are deleted after validation to ensure $0 spend.

## Key Decisions
- [ADR-001: Lambda vs EC2](../decision-records/adr-001-lambda-vs-ec2.md)
- [ADR-002: DynamoDB vs RDS](../decision-records/adr-002-dynamodb-vs-rds.md)
