# Project 03 — Cost Characteristics

## Cost model

This architecture has a predictable, usage-based cost profile.

There are no fixed monthly infrastructure charges.

## Cost drivers

- CloudFront data transfer out
- CloudFront request count
- S3 storage (static files only)
- S3 origin fetches (minimal due to caching)

## Idle cost

There is effectively no idle cost.

If no one visits the site:
- CloudFront serves nothing
- S3 is not accessed
- no compute resources are running

## Cost control mechanisms

- Aggressive caching reduces origin fetches
- Small static assets minimize transfer costs
- No runtime services eliminate surprise billing scenarios

The architecture scales traffic without scaling cost complexity.
