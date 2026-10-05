# Round 4 — observability (~7 min)

No new git repo. This round is Datadog and AWS, queried through their MCPs.

The sandbox is not built yet. See [later-observability.md](../later-observability.md). Until it exists, ask the question on stage and do not fake a graph.

## Prompt, once the sandbox exists

> The least-privilege Terraform commit merged at 09:12 UTC and the receipts log breaks at 13:04 UTC. Use Datadog for when write failures actually started. Use AWS CloudTrail for what changed on the receipts bucket and the chalkline-storage task role. Did the Terraform apply cause this?

## What good looks like

- Custom metrics for storage write success and failure stay healthy through 09:12 and break at 13:04
- CloudTrail shows no Terraform apply of `76376a8`
- CloudTrail shows a manual session, just before 13:04, from a suspicious IP using the `ci-deployer` key to assume `chalkline-prod-platform-admin`
- That session removes the public access block, adds a public `s3:GetObject` bucket policy, and replaces the live storage role policy so it can no longer `s3:PutObject`
- Desired state in git and live state in AWS disagree. The bucket is world-readable and the storage task cannot write

## Say this

IaC told the agent what we meant. Observability told it what happened. Both had to be in a form a tool could query. A wiki page and a memory of "someone was in the console" are not that form.
