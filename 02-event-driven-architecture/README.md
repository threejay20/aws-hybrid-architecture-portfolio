# Project 02 — Event-Driven Architecture

## Overview

This project implements an asynchronous, event-driven workflow using managed messaging services.
The system decouples producers from consumers and treats failure as a first-class concern.

Messages are buffered, retried automatically, and isolated on repeated failure to preserve durability.

---

## Architecture

Producer → SNS → SQS → Lambda (with Dead Letter Queue)

SNS provides event fanout, SQS buffers messages, and Lambda processes events asynchronously.
Messages that repeatedly fail processing are routed to a Dead Letter Queue.

![Architecture Diagram](assets/project-02-event-driven/diagram.png)

---

## Key Design Decisions

### Asynchronous messaging
- Producers are isolated from consumer throughput
- Temporary spikes are absorbed without backpressure
- Failures do not cascade upstream

### SNS for fanout
- Single event published to multiple subscribers
- Enables independent downstream consumers

### SQS for buffering and durability
- At-least-once delivery semantics
- Visibility timeout controls retry behavior
- Message retention protects against data loss

---

## Failure Handling

Messages that fail processing are retried automatically.
After exceeding the configured receive count, messages are moved to a Dead Letter Queue for inspection and remediation.

![SNS to SQS Subscription](assets/project-02-event-driven/sns-to-sqs.png)

![Dead Letter Queue Configuration](assets/project-02-event-driven/sqs-dlq.png)

---

## Processing and Scaling

- Lambda concurrency scales with queue depth
- No polling infrastructure required
- Processing rate adapts to workload automatically

![Lambda SQS Trigger](assets/project-02-event-driven/lambda-trigger.png)

---

## Operational Characteristics

- Failures isolated to individual messages
- Backlogs observable via queue metrics
- Poison-pill messages preserved for analysis

---

## Cost Characteristics

- No idle compute
- Messaging charged per request
- Suitable for bursty or unpredictable workloads

---

## Trade-offs

**Pros**
- Strong decoupling
- High durability
- Automatic retries and failure isolation

**Cons**
- Eventual consistency
- Duplicate message handling required
- Increased architectural complexity

---

## Use Cases

- Event-driven workflows
- Background processing
- Fanout architectures
- Systems requiring resilience to partial failure

---

## Status

Deployed and validated  
Event-driven workflow operating with retries and dead-letter handling.

