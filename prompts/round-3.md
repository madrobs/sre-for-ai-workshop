# Round 3 — Terraform (~8 min)

Add `chalkline-receipts-terraform`. This is desired state for dev, stg, and prod.

## Prompt

> Same incident. You now also have the platform Terraform. receipts-api calls chalkline-storage. chalkline-storage is the only task that can use the receipts bucket. What does this repo say changed, and did that change cause the 13:04 failures?

## What good looks like

- `services.tf` sets `STORAGE_URL` to `http://chalkline-storage.<env>.chalkline.internal:4000` and `OBJECTS_BUCKET` to `chalkline-athletics-receipts-<env>`
- Network rule: receipts-api may call storage on port 4000. The receipts-api task role has no S3 policy
- `iam.tf` on main allows the storage role `s3:GetObject` only. The comment says the printer already has the PDF
- `git log -S PutObject -- iam.tf` shows `f14c3df` at 09:12 UTC: `chore: least-privilege S3 policy for chalkline-storage`
- Failures in the receipts log start at 13:04 UTC. This repo does not show an apply

## Say this

Git records what we intended and when we merged it. It does not record what production was running at 13:04. If the room stops on this commit, ask: what would you look at to see whether this apply happened, and when the errors actually started?
