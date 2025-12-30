# Operations

## Monitoring
- CloudWatch metrics for Lambda (errors, duration, throttles)

## Logging
- CloudWatch Logs for request debugging

## Runbook
- If 5xx spikes: check Lambda logs → verify IAM permissions → validate DynamoDB table name/env vars
