# Round 1 — app + logs only (~8 min)

Do **not** send people to Terraform yet. Paste logs (and optionally `app/src/storeReceipt.js`) on the projector.

## What they see

From `chalkline-receipts` (or a slide copy of `logs/prod-latest.log`):

- `failed to store receipt: Access Denied`
- `code: AccessDenied`
- `awsAction: PutObject`
- `status: 500`
- front desk reprint queue backing up

App tests still pass. There is retry logic for `SlowDown` / `InternalError` / `NetworkingError`.

## Prompt (laptops, if wifi)

> Chalkline Athletics. Drop-in day passes at the front desk started failing Saturday around 13:00 UTC. Here are the logs and the receipts service code. Why are sales returning 500? What would you change?

Attach or paste: `logs/prod-latest.log`, `app/src/storeReceipt.js`, `app/src/server.js`.

## Let it fail

Typical wrong turns: more retries, AWS SDK bug, “S3 is down,” blame the Saturday-rush commit, add client-side PDF generation. AccessDenied on PutObject is a permission problem; the app cannot fix it.

Say out loud: **the failure is not in the handler. The map of the system is missing.**
