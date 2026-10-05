# Solution — facilitator only

Do not show this during rounds 1–3.

**What production did:** Just before 13:04 UTC on September 19, a manual session assumed `chalkline-prod-platform-admin` with the `ci-deployer` key. It made `chalkline-athletics-receipts-prod` world-readable and replaced the live `chalkline-storage` role policy with `s3:GetObject` only. Writes from the storage task then fail. receipts-api only sees a generic 500.

**The decoy:** `f14c3df` (`chore: least-privilege S3 policy for chalkline-storage`) merged at 09:12 UTC the same morning and was not applied. It describes the same missing `PutObject`, so git looks guilty until CloudTrail shows no apply.

**What each round can know**

1. receipts-api failed at 13:04. The handler hid the upstream error.
2. chalkline-storage is the writer. S3 is the object store. The permission is not in this repo.
3. Desired state gives the storage role `GetObject` only, as of a commit four hours earlier. Apply status is absent.
4. Metrics time the break to 13:04. CloudTrail names the manual session.

**Fix after the session, if anyone tinkers:** restore `s3:PutObject` on the live storage role, remove the public bucket policy, restore the public access block, and rotate the `ci-deployer` key. Do not `terraform apply` during the workshop.
