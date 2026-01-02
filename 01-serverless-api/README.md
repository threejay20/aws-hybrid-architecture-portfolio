# Project 01 — Serverless API

## Overview

This project implements a stateless HTTP API using fully managed AWS services.

The service exposes a small REST interface while avoiding server management,
capacity planning, and idle infrastructure.

---

## Architecture

Client → API Gateway → Lambda → DynamoDB

API Gateway is the public ingress.
Lambda handles request processing.
DynamoDB provides persistence.

![Architecture Diagram](../assets/project-01-serverless-api/diagram.png)

---

## API Surface

The API exposes a minimal REST interface for task resources.

Endpoints:
- GET /tasks
- POST /tasks
- GET /tasks/{id}
- PUT /tasks/{id}
- DELETE /tasks/{id}

![API Gateway Routes](../assets/project-01-serverless-api/api-gateway-routes.png)

---

## Security Configuration

- IAM execution role scoped to required DynamoDB actions only
- No public access to DynamoDB
- API Gateway is the only ingress point

![DynamoDB Table](../assets/project-01-serverless-api/tabledetails.png.png)

---

## Observability

Lambda emits logs and metrics automatically.

- Invocation logs available in CloudWatch Logs
- Error rates and latency visible via Lambda metrics

![CloudWatch Logs](../assets/project-01-serverless-api/cloudwatch.png)

---

## Cost Characteristics

- No idle compute
- Pay-per-request execution
- Managed services reduce operational overhead

---

## Trade-offs

Pros:
- No server management
- Automatic scaling
- Predictable cost model

Cons:
- Cold start latency
- Stateless execution model
- Service limits must be managed

---

## Status

Deployed and validated.

Requests flow end-to-end through API Gateway,
Lambda executes correctly,
and DynamoDB persists data as expected.

