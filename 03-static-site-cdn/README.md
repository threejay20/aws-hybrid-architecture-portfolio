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

![CloudFront Distribution Overview](assets/project-03-static-cdn/01-cloudfront-distribution.png)

---

## Origin Protection

The S3 bucket is not publicly accessible.  
Access is granted exclusively to the CloudFront distribution via Origin Access Control.

![CloudFront Origin with OAC](assets/project-03-static-cdn/02-cloudfront-origins-oac.png)

![S3 Bucket Permissions (Private)](assets/project-03-static-cdn/03-s3-bucket-private.png)

This configuration ensures all requests must pass through CloudFront and prevents direct object access.

---

## Caching and Delivery

CloudFront caches static assets at edge locations to reduce latency and minimize origin load.  
Compression is enabled to reduce transfer size and improve performance.

---

## Operational Validation

Live traffic was validated using browser developer tools:

- Requests are served from a `cloudfront.net` domain
- Response headers confirm edge delivery
- Origin server is reported as Amazon S3
- Direct S3 access is denied

![CloudFront Live Request Headers](assets/project-03-static-cdn/04-cloudfront-live-request.png)

---

## Cost Characteristics

- CloudFront Free Plan
- Standard S3 storage
- No compute resources
- No always-on infrastructure

Costs scale only with usage.

---

## Trade-offs

**Pros**
- Global performance
- Strong origin security
- Minimal operational complexity
- Clear separation of concerns

**Cons**
- Cache invalidation introduces propagation delay
- Not suitable for dynamic or personalized content
- Advanced protections require paid tiers

---

## Use Cases

- Static websites
- Documentation portals
- Public portfolios
- Read-heavy content with minimal updates

---

## Future Improvements

Several enhancements were intentionally left out to keep the architecture simple, cost-efficient, and focused. These would be appropriate additions as requirements evolve:

- **Custom domain and TLS certificate**  
  Attach an ACM certificate and Route 53 record to serve the site under a custom domain while maintaining HTTPS enforcement at the edge.

- **Access logging and request analytics**  
  Enable CloudFront access logs or integrate with centralized logging to analyze traffic patterns and cache efficiency.

- **Web Application Firewall (WAF)**  
  Add AWS WAF for request inspection, rate limiting, or geo-based controls if the site begins accepting user input or higher traffic volumes.

- **Cache strategy refinement**  
  Introduce versioned static assets or fine-grained cache behaviors to reduce invalidation frequency during updates.

- **Multi-environment separation**  
  Split content into separate buckets and distributions (e.g., staging and production) for safer iteration and controlled releases.

These enhancements build naturally on the existing design without changing the core delivery or security model.

--

## Status

Deployed  
CloudFront distribution serving content from a private S3 origin using Origin Access Control.

