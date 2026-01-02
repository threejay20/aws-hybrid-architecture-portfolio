# Project 01 — Serverless API

## Overview

This project implements a stateless HTTP API using fully managed AWS services.
The design avoids server management, capacity planning, and idle infrastructure.

---

## Architecture

Client → API Gateway → Lambda → DynamoDB

API Gateway acts as the public entry point.  
Lambda functions process requests and persist data in DynamoDB.

![Architecture Diagram](../../assets/project-01-serverless-api/diagram.png)

---

## API Surface

The API exposes a minimal REST interface for task management.

- GET /tasks
- POST /tasks
- GET /tasks/{id}
- PUT /tasks/{id}
- DELETE /tasks/{id}

![API Gateway Routes](../../assets/project-01-serverless-api/api-gateway-routes.png)

---

## Security

- IAM execution role scoped to required DynamoDB actions
- No public access to DynamoDB
- API Gateway is the only ingress point

![DynamoDB Table Configuration](../../assets/project-01-serverless-api/tabledetails.png.png)

---

## Observability

Lambda emits logs and metrics automatically.

- Invocation logs in CloudWatch Logs
- Error rates and latency via Lambda metrics

![CloudWatch Logs](../../assets/project-01-serverless-api/cloudwatch.png)

---

## Cost Characteristics

- No idle compute
- Pay-per-request execution
- Fully managed services reduce operational overhead

---

## Status

Deployed and validated.  
Requests flow end-to-end through API Gateway, Lambda, and DynamoDB.

