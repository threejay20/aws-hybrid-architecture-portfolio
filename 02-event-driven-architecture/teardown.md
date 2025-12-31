# Teardown Procedure

All resources were deleted after validation to avoid unnecessary cost.

## Resources Removed
- AWS Lambda function (`orders-processor`)
- Event source mapping (SQS → Lambda)
- Amazon SNS topic (`orders-topic`)
- Amazon SQS queue (`orders-queue`)
- Amazon SQS Dead Letter Queue (`orders-dlq`)
- IAM execution role (if created exclusively for this project)

## Verification
- No remaining Lambda functions
- No active SQS queues
- No SNS topics
- AWS billing dashboard checked for unexpected charges

## Why teardown matters
- Prevents unintended cost
- Demonstrates operational discipline
- Reinforces infrastructure lifecycle awareness

## Exam relevance (AWS SAA)
- AWS resources incur cost when left running
- Serverless does not mean “free forever”
