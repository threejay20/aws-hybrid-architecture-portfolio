# Project 03 — Architecture

## What I built

A static portfolio site delivered globally through CloudFront, with an S3 bucket as the origin.

The S3 bucket is **not public**. CloudFront is the only allowed reader, enforced with **Origin Access Control (OAC)** + a bucket policy that grants access only to the specific distribution.

This keeps the site fast (edge caching) while keeping the origin private (no direct S3 access).

## Core request flow

1. A user requests a page (e.g., `/index.html`) from the CloudFront distribution domain.
2. CloudFront checks the closest edge cache.
3. If the object is cached, CloudFront serves it immediately.
4. If it’s a cache miss, CloudFront fetches it from the S3 origin (using OAC-signed requests).
5. CloudFront returns the object to the user and caches it per the cache policy.

## Design decisions (and why)

### CloudFront in front of S3
I used CloudFront because it provides:
- lower latency via edge caching
- a single public entry point for the site
- origin shielding from direct public access patterns (everything funnels through CloudFront)

### Private S3 origin (no public bucket)
The bucket is locked down so the origin cannot be accessed directly.
That reduces accidental exposure (public ACL/policy mistakes) and forces all traffic through CloudFront where I can control security and caching behavior.

### Origin Access Control (OAC) instead of OAI / public access
OAC is the modern approach for private S3 origins. CloudFront signs requests to S3 and S3 only allows reads that match the distribution access pattern.

This creates a clean separation:
- CloudFront = public delivery layer
- S3 = private origin storage

### Origin path: `/site`
The bucket contains multiple folders for this repo, but the distribution only needs to serve the website files.
Using `/site` as the origin path narrows what CloudFront can request from S3 and keeps the origin mapping aligned with how the repo is structured.

### Default root object: `index.html`
The distribution serves `index.html` as the default root object so the site loads from the base URL without requiring `/index.html` in the browser.

## Security posture

- **S3 Block Public Access: enabled**
- **Bucket policy: allows `s3:GetObject` only from CloudFront** (via OAC)
- Public access paths are intentionally limited to CloudFront, which becomes the enforced front door.

## Reliability + performance characteristics

- CloudFront caches static content at the edge to reduce repeated origin fetches.
- The origin (S3) is extremely durable and doesn’t require maintenance or patching.
- The architecture has no servers, no scaling actions, and minimal moving parts.

## What I validated

- Site loads through the CloudFront distribution domain.
- S3 remains private (no direct public object reads).
- Browser network headers show CloudFront in the response path and confirm the content is served through the distribution.
