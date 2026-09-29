# SRE for AI — facilitator repo

Private notes for the Women Who Code October leadership session **How SRE Accidentally Prepared Us for AI**.

Attendee clone: **[chalkline-receipts](https://github.com/madrobs/chalkline-receipts)** (Chalkline Athletics). Keep this guide private until after round 1 or they will skip the hunt.

Do not mention PushPress on slides or in the public repo.

## Repos

| Repo | Role |
|---|---|
| `chalkline-receipts` | Round 1. Receipt API only. It calls `chalkline-storage` and never mentions AWS. |
| `chalkline-storage` | Internal object API. This is the service that writes to S3 with its task role. |
| `chalkline-receipts-terraform` | Platform for dev, stg, and prod. Desired IAM for `chalkline-storage` only. No logs, metrics, or CloudTrail. |
| `sre-for-ai-workshop` | Facilitator notes. |

The least-privilege commit in Terraform is a decoy: it merges before the outage and is never applied. The live change is a later observability round. See [later-observability.md](later-observability.md).

## Old scene notes (stale)

Newest first:

1. `chore: snapshot Saturday front-desk receipt errors` — logs only; decoy if people `git blame` the log file
2. **`chore: least-privilege S3 policy for receipts-api`** — removes `s3:PutObject`
3. `fix: retry transient S3 errors when storing drop-in receipts` — app red herring
4. `feat: drop-in receipts API and AWS baseline for Chalkline Athletics` — healthy IAM (`GetObject` + `PutObject`)

On stage:

    git show c0d18ef -- terraform/iam.tf

(Refresh the hash after any history rewrite: `git log --oneline -- terraform/iam.tf`)

## Wifi / theater

Stage path is the real workshop. Laptops are bonus: clone `chalkline-receipts`, paste the round 2 prompt into whatever AI they have. If wifi dies, walk `terraform/iam.tf` and `git log` on the projector.
