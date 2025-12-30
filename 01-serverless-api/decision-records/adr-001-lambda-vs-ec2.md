# ADR-001: Lambda vs EC2 for REST API

## Decision
Use AWS Lambda instead of EC2 for the API backend.

## Context
The API is expected to have low and unpredictable traffic.
Operational overhead and idle cost should be minimized.

## Considered options
- EC2 + ALB
- Lambda + API Gateway

## Decision rationale
Lambda provides automatic scaling, no server management,
and zero cost when idle, making it ideal for this workload.

## Consequences
- Cold starts possible (acceptable for this use case)
- Less control over runtime environment
