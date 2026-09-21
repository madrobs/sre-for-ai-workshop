# Solution — do not share in round 1

**Cause:** Terraform IAM for `chalkline-receipts-api` was tightened to `s3:GetObject` only. The task role can no longer `PutObject` on `chalkline-athletics-receipts-prod`. The app still tries to write `drop-ins/{id}.json`. S3 returns `AccessDenied`; the API wraps that as a 500.

**Why it looked like an app bug:** logs live at the HTTP layer. The well-intentioned commit message sounds like good SRE. The previous commit added S3 retries, which is a magnet for the wrong fix.

**Fix (after the session, if they want to tinker):** restore `s3:PutObject` on `${aws_s3_bucket.receipts.arn}/*`. Do not `terraform apply` in the workshop; this is a reading repo.

**The point:** desired state and the story of the change were in git the whole time. Without that in context, humans and agents stay in `storeReceipt.js`.
