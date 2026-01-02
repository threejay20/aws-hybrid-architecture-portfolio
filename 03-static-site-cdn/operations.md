# Project 03 — Operations

## How this system is operated

This architecture intentionally minimizes operational effort.

There are no servers, no runtime environments, and no scaling controls to manage. Once deployed, the system runs passively and only responds to user traffic.

Operational responsibility is limited to:
- content updates
- cache behavior
- access validation

## Content updates

Site updates are handled by uploading new or modified files to the S3 bucket under the `/site` prefix.

Once uploaded:
- CloudFront will serve cached versions until the object expires
- updated content becomes visible automatically after cache expiry or manual invalidation

## Cache management

CloudFront caching is the primary operational lever.

Typical scenarios:
- **Small updates**: wait for cache expiration
- **Urgent updates**: issue a CloudFront invalidation for affected paths

Invalidations are scoped narrowly (e.g., `/index.html`) to avoid unnecessary cache churn.

## Monitoring

Operational visibility is intentionally lightweight.

Validation is done through:
- browser network inspection (confirm CloudFront headers)
- CloudFront metrics (requests, cache hit ratio, error rates)
- S3 access patterns (origin traffic only from CloudFront)

There is no application logging layer because no application code runs in this architecture.

## Failure modes

- **S3 outage**: extremely unlikely; CloudFront will return cached objects if available
- **Cache misconfiguration**: resolved by invalidation or behavior adjustment
- **Permission errors**: manifest as 403 errors from CloudFront and indicate a broken origin policy

Failures are deterministic and configuration-based, not runtime-based.
