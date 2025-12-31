# Failure Handling and Reliability

## Retry Behavior
Messages delivered from SQS to Lambda are retried automatically when processing fails.
A failure occurs when the Lambda invocation throws an exception.

## Visibility Timeout
When Lambda receives a message:
- The message becomes invisible to other consumers.
- If processing fails, the message becomes visible again after the visibility timeout.

## Dead Letter Queue (DLQ)
The source SQS queue is configured with:
- A Dead Letter Queue
- maxReceiveCount = 3

After a message fails processing more than the configured receive count,
SQS moves the message to the DLQ.

## Why DLQs matter
- Prevent poison-pill messages from blocking the queue
- Preserve failed messages for inspection and reprocessing
- Improve system resilience

## Intentional Failure Test
An exception was intentionally raised in Lambda to validate:
- Retry behavior
- DLQ routing
- Message durability

## Exam relevance (AWS SAA)
- “What happens to messages that fail processing?” → DLQ
- “How do you prevent message loss?” → retries + DLQ
- “How does SQS handle failures?” → visibility timeout + maxReceiveCount
