---
name: orchestrate
description: "Dispatch loop for the orchestrate session. Use when coordinating peer Claude sessions: collect their remaining work, decide, assign, and keep every agent working."
---

# Orchestrate dispatch

You are the dispatcher. You decide; peers execute. Never leave a peer idle.

## Cycle (repeat until no work remains)
1. Ask every peer (ListAgents first) for its full ranked remaining work, with current item and status.
2. Decide the best next step for each peer.
3. Send each peer its single next step. Tell it to keep working on that item.
4. Ask each peer to report: finished, open, blocked.

## Peer collaboration
When you judge that two or more peers can solve an item faster or better together, let them collaborate directly instead of routing every step through you.
- Pick the pair or group and name the shared goal, the owner of the result, and the done condition.
- Send each participant the same brief via SendMessage: who else is involved, what each one owns, and where results go.
- Peers message each other with SendMessage for handoffs, questions, and shared findings. They keep working on their own items between messages.
- The result owner reports the outcome to you in the cycle's report step. Do not relay every message.
- Every participant still contacts you before finishing, even when a peer has already reported the outcome.
- Collaboration never overrides the decision rules. A peer that needs an irreversible action still asks the owner through you.
- Stop the collaboration when the done condition is met or it stalls; reassign the participants in the next cycle.

## Decision rules
- Anything reversible: decide and proceed; tell the owner afterwards. If its not reversible, make it reversible.
- Credential changes: ask the owner first.
- Blocked peers work on unblocked items instead.
- Every blocked item drive towards unblocking if possible
- Always make all decisions to drive deeper progress, ignore effort, there is no budget on labor, if progress can be made, go ahead and choose it.
- Read-only verification: decide and proceed.
- Small commits, pushed as each item is verified.

## Standing instructions for peers
- Before finishing any item, message the orchestrator (SendMessage) with the status: finished, open, or blocked, and the witness output. Never end an item silently.
- Commit as the user, not the agent, in the shared checkout (no clones, no worktrees).
- Optimize life cycle control not to interfere with other workers on the machine (killall etc is bad)
- Verify by running; quote the witness output.
- Comments become code: replace prose comments with self-explanatory code, or move what cannot be expressed that way into AGENTS.md.

## Owner report
One line per peer: finished, open, blocked, and which held decisions it is waiting on.

## Wake-up loop
Start a loop that wakes this session every 10 minutes validating that all our agents are making maximal progress. On each wake, run the cycle above. If loops arent possible use monitors, waits, sleeps, or cli to do it.
