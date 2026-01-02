# Project 01 — Serverless API

## Overview
This project implements a stateless HTTP API using fully managed AWS services.

The intent is to expose a small REST interface without managing servers, capacity planning, or idle compute.

## Architecture
Client → API Gateway → Lambda → DynamoDB

API Gateway is the public entry point. Lambda handles request processing and persists data in DynamoDB.

![Architecture Diagram](../assets/project-01-serverless-api/diagram.png)

## API Surface
Endpoints:

- GET /tasks
- POST /tasks
- GET /tasks/{id}
- PUT /tasks/{id}
- DELETE /tasks/{id}

![API Gateway Routes](../assets/project-01-serverless-api/api-gateway-routes.png)

![POST /tasks Example](../assets/project-01-serverless-api/Post_get.png)

## Lambda Implementation
Lambda uses environment variables and an IAM execution role scoped to only what the function needs.

![Lambda Code](../assets/project-01-serverless-api/lambda_code.png.png)

![Lambda Environment](../assets/project-01-serverless-api/lambda_enviroment.png.png)

## Data Layer
DynamoDB stores tasks by key (taskId) with simple access patterns.

![DynamoDB Table Details](../assets/project-01-serverless-api/tabledetails.png.png)

## Observability
Lambda emits logs and metrics automatically through CloudWatch.

![CloudWatch Logs](../assets/project-01-serverless-api/cloudwatch.png)

## Cost Characteristics
- No always-on compute
- Pay-per-request execution model
- Managed services reduce operational overhead

## Trade-offs
**Pros**
- No server management
- Automatic scaling
- Predictable cost model

**Cons**
- Cold start latency
- Stateless execution model
- Service limits must be designed around

## Status
Deployed and validated end-to-end (API Gateway → Lambda → DynamoDB).


