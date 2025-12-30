# ADR-002: DynamoDB vs RDS for persistence

## Status
Accepted

## Context
The data model is simple (tasks). The priority is predictable performance, minimal administration, and avoiding idle database cost.

## Decision
Use DynamoDB (on-demand) instead of RDS.

## Rationale
- No server management, backups handled by service defaults
- High performance at scale with simple key access patterns
- On-demand capacity avoids capacity planning and idle cost
- Fits the access pattern: taskId → item

## Consequences
- Requires careful key design to avoid hot partitions
- Limited relational querying compared to SQL
