
# Project 03 — Teardown

## Teardown order

Resources should be removed in this order to avoid permission conflicts.

### 1. CloudFront distribution

- Disable the distribution
- Wait for deployment to complete
- Delete the distribution

This removes the only public access path to the site.

### 2. S3 bucket policy

Once CloudFront is deleted:
- remove the bucket policy allowing CloudFront access

### 3. S3 bucket contents

- delete all objects under the `/site` prefix

### 4. S3 bucket

- delete the bucket itself

## Post-teardown validation

- CloudFront domain no longer resolves
- S3 bucket cannot be accessed
- No remaining IAM policies reference the deleted distribution

Teardown leaves no exposed resources or dangling permissions.
