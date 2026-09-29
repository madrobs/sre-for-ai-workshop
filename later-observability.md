# Later step — observability via MCP

Do not put logs, metrics, or CloudTrail in the Terraform repo. That reveal comes after someone has the infra map and still cannot tell what production actually did.

## The mismatch to demonstrate

`chore: least-privilege S3 policy for chalkline-storage` merges on the morning of September 19. Prod failures start later, around 13:49 UTC. Terraform Cloud planned that commit and never applied it, so git history is not the incident clock.

What did change production is a manual session from a suspicious IP, using the `ci-deployer` key to assume `chalkline-prod-platform-admin`:

- remove the bucket's public access block
- attach a public `s3:GetObject` bucket policy
- replace the live `chalkline-storage` role policy so it can no longer `s3:PutObject`

The bucket becomes world-readable, and the storage task starts failing writes. Desired state in git and live state in AWS disagree.

## How the room gets there

1. Datadog MCP — when the errors changed. Instrument `chalkline-storage` (or receipts) so successful and failed receipt writes are custom metrics, not only logs. The graph should stay healthy through the Terraform merge and rise when the manual change lands.
2. AWS MCP — CloudTrail for the bucket policy, public access block, and `PutRolePolicy` on `chalkline-prod-chalkline-storage`. This is the evidence that the apply never happened and a credential did.

## Still to build

- [ ] A Datadog account or sandbox with those custom metrics loaded for the September 19 window
- [ ] An AWS account or CloudTrail mock the AWS MCP can query for the same window
- [ ] App instrumentation: count receipt write success and failure, tagged by service and environment
- [ ] Workshop prompt for this round only, after the Terraform round

No metric names, dashboard, or CloudTrail export belong in `chalkline-receipts-terraform`.
