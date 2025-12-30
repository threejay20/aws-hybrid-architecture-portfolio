# Architecture

## Problem statement
Build a simple serverless REST API that supports CRUD for a single resource (e.g., notes/tasks),
optimized for $0 idle cost and automatic scaling.

## Architecture overview
Client → API Gateway → Lambda → DynamoDB

## Why this design
- Serverless removes server management and scales automatically.
- DynamoDB provides low-latency key-value storage without capacity planning.
- Pay-per-use model keeps cost near $0 for low traffic.

## Alternatives considered
- EC2 + ALB + RDS: more control, more ops overhead, not $0 idle.
- Lambda + RDS: relational benefits, but higher operational/cost risk.

## Failure scenarios
- Lambda errors → API returns 5xx; use logs to debug.
- Throttling → use API Gateway throttles and backoff.
- DynamoDB hot partition → improve key design.
