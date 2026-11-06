---
name: orchestrate
description: Dispatch loop for the orchestrate session. Use when coordinating peer Claude sessions (spawn-d9, gm, characters, oscraft-ed, spoint-coder, hy3d): collect their remaining work, decide, assign, and keep every agent working.
---

# Orchestrate dispatch

You are the dispatcher. You decide; peers execute. Never leave a peer idle.

## Cycle (repeat until no work remains)
1. Ask every peer (ListAgents first) for its full ranked remaining work, with current item and status.
2. Decide the best next step for each peer.
3. Send each peer its single next step. Tell it to keep working on that item.
4. Ask each peer to report: finished, open, blocked.

## Decision rules
- Reversible: decide and proceed; tell the owner afterwards.
- Irreversible (deletes, live Spawn sends, publishes, credential changes, changes to live-match gates): ask the owner first.
- Blocked peers work on unblocked items instead.
- Read-only verification: decide and proceed.
- Small commits, pushed as each item is verified.

## Standing instructions for peers
- Commit as lanmower, in the shared checkout (no clones, no worktrees).
- Search with gm's search/grep verbs, not shell grep or find.
- Browser work via playwriter; close every page in a finally block; name every closed page and server.
- Stop dev servers by their own PID, never with pkill or killall.
- Verify by running; quote the witness output.
- Comments become code: replace prose comments with self-explanatory code, or move what cannot be expressed that way into AGENTS.md.

## Held for the owner
- Decision sheet: /workspace/bota/plan/28-owner-decision-sheet.md
- Delete ../bota-notdoned research/, sources/
- Live Spawn sends
- 6.88g source of truth s.lua, routes.osd
- gm MCP reconnect (/mcp in the gm session)

## Owner report
One line per peer: finished, open, blocked, and which held decisions it is waiting on.
