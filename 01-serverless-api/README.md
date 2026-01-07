# Project 01 — Serverless API

## Overview

This project implements a stateless HTTP API using fully managed AWS services.

The intent is to expose a small REST interface without managing servers,
capacity planning, or idle compute.

---

## Architecture

Client → API Gateway → Lambda → DynamoDB

API Gateway acts as the public entry point.  
Lambda handles request processing and persists data in DynamoDB.

![Architecture Diagram](../assets/project-01-serverless-api/diagram.png)

---

## API Surface

The API exposes a minimal REST interface for managing task resources.

Endpoints:

- GET /tasks  
- POST /tasks  
- GET /tasks/{id}  
- PUT /tasks/{id}  
- DELETE /tasks/{id}  

![API Gateway Routes](../assets/project-01-serverless-api/api-gateway-routes.png)

![POST /tasks Example](../assets/project-01-serverless-api/Post_get.png)

---

## Lambda Implementation

Lambda uses environment variables and an IAM execution role scoped only to
the DynamoDB actions it requires.

![Lambda Code](../assets/project-01-serverless-api/lambda_code.png)

![Lambda Environment Variables](../assets/project-01-serverless-api/lambda_environment.png)

---

## Data Layer

DynamoDB is used as a fully managed NoSQL data store.

- No public access
- Access restricted to the Lambda execution role

![DynamoDB Table Details](../assets/project-01-serverless-api/tabledetails.png)

---

## Observability

- Lambda automatically emits logs to CloudWatch
- Invocation metrics provide visibility into errors and latency

![CloudWatch Logs](../assets/project-01-serverless-api/cloudwatch.png)

---

## Cost Characteristics

- No idle compute
- Pay-per-request execution
- Fully managed services reduce operational overhead

---

## Status

Deployed and validated.  
API responds correctly through API Gateway with DynamoDB persistence.

