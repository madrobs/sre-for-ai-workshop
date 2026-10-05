# Round 4 sandbox — still to build

Round 4 is observability. It is not a git repo, and it does not belong in `chalkline-receipts-terraform`.

Prompt: [prompts/round-4.md](prompts/round-4.md).

## The mismatch

`f14c3df` merges at 09:12 UTC on September 19 and is never applied. `chalkline-receipts` logs break at 13:04 UTC. Git is not the incident clock.

What changes production, just before 13:04, is a manual session from a suspicious IP. It uses the `ci-deployer` key to assume `chalkline-prod-platform-admin`, then:

- removes the bucket public access block
- attaches a public `s3:GetObject` bucket policy on `chalkline-athletics-receipts-prod`
- replaces the live `chalkline-prod-chalkline-storage` role policy so it can no longer `s3:PutObject`

The bucket becomes world-readable. The storage task starts failing writes.

## How the room gets there

1. Datadog MCP — when the errors changed. Instrument `chalkline-storage` so successful and failed object writes are custom metrics. The series stays healthy through 09:12 and breaks at 13:04.
2. AWS MCP — CloudTrail for the bucket policy, the public access block, and `PutRolePolicy` on `chalkline-prod-chalkline-storage`. This shows the apply never happened.

## Still to build

- [ ] A Datadog account or sandbox with those custom metrics for the September 19 window
- [ ] An AWS account or CloudTrail mock the AWS MCP can query for the same window
- [ ] App instrumentation in `chalkline-storage`: count write success and failure, tagged by service and environment
- [ ] Rehearse round 4 against those MCPs before the summit

Until those exist, round 4 on stage is the question only.
