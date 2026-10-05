# Round 1 — receipts API only (~7 min)

Repo: `chalkline-receipts`. Do not mention storage, Terraform, or AWS.

## What they see

`logs/prod-latest.log`

- Receipts succeed until 12:52 UTC
- At 13:04 UTC, `receipt request failed` with status 500
- No error code, no upstream body, no bucket

`app/src/storeReceipt.js` retries `Throttled`, `Timeout`, and `Unavailable`, then throws `failed to save receipt`. The handler returns "Something went wrong."

## Prompt

> Chalkline Athletics. Drop-in receipts at the front desk started failing on September 19 around 13:04 UTC. You have the receipts-api repo: app code and logs/prod-latest.log. Why are sales returning 500? What would you change?

## Let it fail

Typical wrong turns: more retries, a bug in the handler, "the storage service is down," blame the health check or the id check. The app only knows that a POST to the storage service failed.

Say: the caller is doing its job. The next thing an agent needs is the service it calls, not a better prompt.
