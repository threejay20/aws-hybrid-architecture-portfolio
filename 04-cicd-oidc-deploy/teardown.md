# Teardown

This project can be removed cleanly without impacting other resources.

---

## Teardown Order

1. Disable or delete the GitHub Actions workflow
2. Delete the CloudFront distribution
3. Empty the S3 bucket
4. Delete the S3 bucket
5. Delete the IAM role and OIDC trust relationship
6. Remove related CloudFormation stacks (if used)

---

## Notes

- Ensure the S3 bucket is empty before deletion
- CloudFront distributions must be disabled before removal
- IAM role deletion is immediate once detached

---

## Cost Considerations

There are no ongoing costs once resources are removed.

While deployed, costs remain minimal and within free-tier or low-usage ranges for typical portfolio traffic.

