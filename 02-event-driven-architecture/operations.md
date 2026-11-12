# Operations and Monitoring

## Observability
- Lambda execution logs are written to CloudWatch Logs.
- Each message processing attempt generates log entries.

## Monitoring Strategy
Key signals:
- Lambda errors
- SQS queue depth
- DLQ message count

## Troubleshooting Workflow
1. Check CloudWatch Logs for Lambda errors.
2. Inspect DLQ messages to identify poison-pill data.
3. Fix the processing logic or data.
4. Optionally redrive messages from the DLQ.

## Why this approach works
- No servers to monitor
- Managed retry behavior
- Clear separation between healthy and failed messages
