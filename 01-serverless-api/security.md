# Security

## IAM roles & policies
- Lambda execution role with least privilege to the DynamoDB table.
- No hardcoded credentials.

## Trust boundaries
- Public internet ends at API Gateway.
- Lambda runs with IAM role permissions.
- DynamoDB access only via IAM policy.

## Data protection
- TLS in transit via API Gateway.
- DynamoDB encryption at rest (AWS-managed).
