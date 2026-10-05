# Round 2 — storage service (~7 min)

Add `chalkline-storage` to the workspace. Leave Terraform closed.

## Prompt

> Same incident. receipts-api calls the chalkline-storage service. You now have that repo too. Why is the write failing? What would you change in this service?

## What good looks like

- `POST /objects` is the write path receipts-api uses
- `OBJECTS_BUCKET` selects S3. The task role is the credential. There is no access key in the repo
- A rejected write is logged here as `object write failed` with `errorName` and `errorCode`, then returned to receipts-api as `failed to write object`
- The receipts-api 500 is that generic response. The storage service is where an AccessDenied would be visible
- Tests still pass. Nothing in this repo shows a permission change

## Say this

The mechanism is legible now. Desired state and live state are still missing. An agent that says "check the bucket policy" is guessing. Round 3 is where that guess can be checked against what we meant to deploy.
