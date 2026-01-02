# Project 03 — Secure Static Site Delivery with CloudFront

## Overview

This project delivers a static website globally using Amazon CloudFront in front of a private Amazon S3 origin secured with Origin Access Control (OAC).

The objective is to provide fast, reliable content delivery while ensuring the origin is never publicly accessible and operational overhead remains minimal.

This pattern is commonly used for portfolios, documentation sites, internal dashboards, and public-facing static applications.

---

## Architecture

Client → CloudFront → Private S3 (Origin Access Control)

CloudFront serves as the only public entry point.  
The S3 bucket is fully private and can only be accessed by CloudFront using a service-to-service trust relationship.

---

## Key Design Decisions

### CloudFront as the entry layer
- Terminates HTTPS at the edge
- Caches content globally to reduce latency
- Absorbs traffic spikes without scaling concerns
- Provides a single control plane for delivery and security

### Private S3 origin
- Prevents direct object access
- Eliminates accidental public exposure
- Forces all access through CloudFront

### Origin Access Control (OAC)
- Uses IAM-based authorization
- Replaces legacy Origin Access Identity (OAI)
- Restricts S3 access to a specific CloudFront distribution ARN

---

## Security Configuration

- S3 Block Public Access: Enabled
- Bucket policy allows `s3:GetObject` only from CloudFront
- HTTPS enforced at the CloudFront edge
- No direct S3 website hosting
- No public ACLs or bucket policies

The origin cannot be accessed directly, even if object URLs are known.

---

## Caching Behavior

- Default cache behavior optimized for static assets
- Compression enabled (Brotli and Gzip)
- Objects cached at edge locations to reduce origin fetches
- Cache invalidation supported for controlled updates

---

## Operational Validation

The deployment was validated by:
- Accessing content via the CloudFront domain
- Inspecting response headers confirming edge delivery
- Verifying S3 objects are inaccessible directly
- Confirming bucket access is restricted to CloudFront only

Supporting screenshots are stored under:

assets/project-03-static-cdn/

---

## Cost Characteristics

- CloudFront Free Plan
- Standard S3 storage
- No compute resources
- No always-on infrastructure

Costs scale only with usage.

---

## Trade-offs

Pros:
- Global performance
- Strong origin security
- Minimal operational complexity
- Clear separation of concerns

Cons:
- Cache invalidation introduces propagation delay
- Not suitable for dynamic or user-specific content
- Advanced protections require paid tiers

---

## Use Cases

- Static websites
- Documentation portals
- Public portfolios
- Read-heavy content with minimal updates

---

## Status

Deployed  
CloudFront distribution serving content from a private S3 origin using Origin Access Control.

