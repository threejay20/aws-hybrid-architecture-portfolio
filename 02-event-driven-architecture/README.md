# 02 - Event-Driven Architecture (SNS + SQS + Lambda)

## Dead Letter Queue (DLQ) Validation

To validate failure handling, the Lambda consumer was intentionally forced
to throw an exception.

After 3 failed receive attempts, the message was automatically moved
to the Dead Letter Queue (DLQ), preventing message loss and blocking.

![DLQ Message](dlq-message.png)
