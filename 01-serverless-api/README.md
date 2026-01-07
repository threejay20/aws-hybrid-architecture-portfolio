# Project 01 — Serverless API

## Overview
This project implements a stateless HTTP API using fully managed AWS services.

The goal is to expose a small REST interface while avoiding server management, capacity planning, and idle infrastructure costs.

---

## Architecture
Client → API Gateway → Lambda → DynamoDB

API Gateway is the public entry point.  
Lambda handles request processing and persists data in DynamoDB.

![Architecture Diagram](../assets/project-01-serverless-api/diagram.png)

---

## API Surface
The API exposes a minimal REST interface for managing task resources.

**Endpoints**
- GET `/tasks`
- POST `/tasks`
- GET `/tasks/{id}`
- PUT `/tasks/{id}`
- DELETE `/tasks/{id}`

![API Gateway Routes](../assets/project-01-serverless-api/api-gateway-routes.png)

---

## Request Example
![POST /tasks Example](../assets/project-01-serverless-api/Post_get.png)

---

## Lambda Implementation
Lambda uses environment variables and an IAM execution role scoped to only what the function needs.

![Lambda Code](../assets/project-01-serverless-api/lamba_code.png.png)
![Lambda Environment Variables](../assets/project-01-serverless-api/lambda_enviroment.png.png)

---

## Data Layer
DynamoDB stores tasks with simple key-based access patterns.

![DynamoDB Table Details](../assets/project-01-serverless-api/tabledetails.png.png)

---

## Observability
Lambda emits logs and metrics automatically.

- Invocation logs available in CloudWatch Logs
- Error rates and latency visible via Lambda metrics

![CloudWatch Logs](../assets/project-01-serverless-api/cloudwatch.png)

---

## Cost Characteristics
- No idle compute resources
- Pay-per-request execution model
- Fully managed services reduce operational overhead

---

## Trade-offs

**Pros**
- No server management
- Automatic scaling
- Predictable cost model

**Cons**
- Cold start latency
- Stateless execution model
- Service limits must be considered

---

## Status
Deployed and validated.  
API responds correctly through API Gateway with DynamoDB persistence.

