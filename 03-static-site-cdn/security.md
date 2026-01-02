
# Project 03 — Security

## Security model

The security model is based on a single principle:

**The S3 bucket is never public. CloudFront is the only allowed reader.**

All public exposure happens at the CDN layer.

## S3 bucket protections

- Block Public Access: **enabled**
- No public ACLs
- No public bucket policy statements
- Objects are inaccessible via direct S3 URLs

The bucket cannot be used as a website endpoint.

## CloudFront access enforcement

CloudFront uses **Origin Access Control (OAC)** to sign requests to S3.

The S3 bucket policy:
- allows `s3:GetObject`
- only from the CloudFront service principal
- scoped to the specific distribution ARN

This prevents:
- direct S3 object access
- accidental exposure through misconfigured permissions
- bypassing CloudFront controls

## Network exposure

- CloudFront distribution domain is the only public endpoint
- TLS is enforced by default
- HTTP requests are terminated at CloudFront edge locations

There is no inbound access to S3 from the public internet.

## Security boundaries

| Layer        | Responsibility                     |
|-------------|------------------------------------|
| CloudFront  | Public access, TLS, caching        |
| S3          | Private object storage             |
| IAM Policy  | Strict origin access enforcement   |

Security failures surface immediately as access errors rather than silent exposure.
