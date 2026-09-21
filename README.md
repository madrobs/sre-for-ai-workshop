# SRE for AI — facilitator repo

Private notes for the Women Who Code October leadership session **How SRE Accidentally Prepared Us for AI**.

Attendee clone: **[chalkline-receipts](https://github.com/madrobs/chalkline-receipts)** (Chalkline Athletics). Keep this guide private until after round 1 or they will skip the hunt.

Do not mention PushPress on slides or in the public repo.

## Repos

| Repo | Role |
|---|---|
| `chalkline-receipts` | Scene: app + Terraform + logs. `main` is already broken. |
| `sre-for-ai-workshop` | You: prompts, solution, checklist, talk spine. |

## Scene git history (smoking gun)

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
