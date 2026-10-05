# 45-minute spine

Same question every round: why did front-desk receipts start failing at 13:04 UTC on September 19, and what would you change?

1. Hook (4) — The failure was not in the app logs. SRE made systems legible. That is what AI needs.
2. Three headlines (4) — Declare the system. Encode the standards. Encode the response.
3. Round 1 (7) — `chalkline-receipts` only. Let the guess stay in the app.
4. Round 2 (7) — Add `chalkline-storage`. The write path becomes visible. The permission change does not.
5. Round 3 (8) — Add `chalkline-receipts-terraform`. Desired state and git history. The least-privilege commit is a decoy until someone proves it was applied.
6. Round 4 (7) — Observability. Datadog for when the errors changed. AWS CloudTrail for what production actually did. If the sandbox is not ready, ask the question and show the note. Do not invent the graphs.
7. Checklist and their org (6) — Which artifact was missing the last time an agent, or a new teammate, got stuck?
8. Close (2) — Each round removed one "who do I ask?" AI does not replace SRE. Undocumented systems starve both humans and agents.

Stage path is the workshop. Laptops follow along if wifi holds. Do not open round 2's repo during round 1.
