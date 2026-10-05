# SRE for AI — facilitator repo

Private notes for the Women Who Code October leadership session **How SRE Accidentally Prepared Us for AI**.

Keep this repo private through the session. Do not mention PushPress on slides or in the public repos.

## Rounds

Same incident every time. Add one artifact per round.

| Round | Add | What becomes legible |
|---|---|---|
| 1 | [chalkline-receipts](https://github.com/madrobs/chalkline-receipts) | A vague 500 at 13:04 UTC. The handler hides the upstream error. |
| 2 | [chalkline-storage](https://github.com/madrobs/chalkline-storage) | This service writes the object. S3 is the mechanism. The permission change is not here. |
| 3 | [chalkline-receipts-terraform](https://github.com/madrobs/chalkline-receipts-terraform) | Desired state. `f14c3df` drops `s3:PutObject` at 09:12 UTC and was not applied. |
| 4 | Datadog MCP and AWS MCP | When the errors started, and the manual change that production actually ran. Sandbox not built. |

Script: [talk-spine.md](talk-spine.md). Prompts are in `prompts/`. Full cause: [SOLUTION.md](SOLUTION.md). Round 4 build list: [later-observability.md](later-observability.md).

## Wifi / theater

You run each round on stage. Attendees clone along if the network holds. Round 4 needs the MCPs on your machine. If they are not ready, ask what they would query and stop there.
