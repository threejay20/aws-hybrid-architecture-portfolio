# Cost

## Free-tier assumptions
- Low request volume (manual testing only)
- DynamoDB on-demand
- Lambda + API Gateway within free tier usage

## What could accidentally cost money
- Heavy API testing or loops
- Leaving logs extremely noisy (high ingestion)
- Creating extra paid services (avoid NAT Gateway, ALB, etc.)

## How I verified $0 usage
- AWS Billing dashboard / Cost Explorer checked after build + teardown
