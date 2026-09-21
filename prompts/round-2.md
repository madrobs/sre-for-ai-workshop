# Round 2 — full clone (~10 min)

Same question, now with **Chalkline Athletics in the workspace**: app, `terraform/`, git history, logs.

## Prompt

> Same incident. You now have the chalkline-receipts repo cloned (app, terraform, logs, git history). Why is the front desk getting AccessDenied on PutObject? What changed?

## What good looks like

- `terraform/iam.tf` — `s3:PutObject` gone; comment claims the printer already has the PDF
- `git show` on `chore: least-privilege S3 policy for receipts-api`
- Security group still allows 443 egress (same pattern, not this outage)
- App retries never fire: `AccessDenied` is not retryable

## If nobody has wifi

On the projector:

    git log --oneline -- terraform/iam.tf
    git show <least-privilege-hash> -- terraform/iam.tf

Then: an agent (or a new engineer) can only do this if the map is in the repo.
