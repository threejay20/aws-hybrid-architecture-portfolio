# 01 – Serverless API (API Gateway + Lambda + DynamoDB)

## Overview
This project demonstrates a fully serverless REST API built on AWS,
optimized for zero idle cost and automatic scaling.

## Architecture
Client → API Gateway → Lambda → DynamoDB

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
