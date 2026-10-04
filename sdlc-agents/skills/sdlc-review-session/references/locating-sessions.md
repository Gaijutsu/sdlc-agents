# Locating Kiro sessions

Kiro CLI saves every session turn locally under `~/.kiro/sessions/` (owner-only access). Sub-agents get their own
session records, linked to the parent. Layouts differ by engine and version, so confirm which you have.

## 1. Find the parent (orchestrator) session
- Best: run-log.md records the orchestrator session id (`/session-id`). Search for it:
  `find ~/.kiro/sessions -maxdepth 3 -name "*<id>*"` and `grep -rl "<id>" ~/.kiro/sessions --include=*.json | head`
- Otherwise: find sessions for this workspace in the run's time window:
  `grep -l "\"<workspace-path>\"" ~/.kiro/sessions/*/*.json ~/.kiro/sessions/*/*/session.json 2>/dev/null`
  then pick by modified time (`ls -lt`) against the run-log start date.

## 2. Known layouts
- **Directory format** (V3 engine): `~/.kiro/sessions/<…>/<session>/session.json` (metadata),
  `messages.jsonl` (the conversation and tool events), `sub-executions/` (one entry per sub-agent run).
- **Three-file format**: `~/.kiro/sessions/cli/<id>.json` (metadata: cwd, title), `<id>.jsonl` (event log),
  `<id>.lock`. Sub-agent sessions appear as additional `<id>.json/.jsonl` pairs with the same cwd, created during
  the parent's run; the parent's event log contains the sub-agent dispatch events with their ids.

## 3. Find the sub-agent sessions
- Directory format: list `sub-executions/` in the parent.
- Three-file format: `grep -n -i "subagent\|sub_agent" <parent>.jsonl | head` to find dispatch events, then
  match the child ids; or list same-cwd sessions created between the parent's start and end times.
- Match each child to its agent name (e.g. `sdlc/implementer`) and task from the dispatch event or the child's first message.

## 4. Reading the event log
Each line is one JSON event. Useful patterns:
- tool calls and their status: `grep -n '"tool_call' file.jsonl | head -50`
- failures and refusals: `grep -n -i '"failed"\|rejected\|denied\|forbidden' file.jsonl`
- the brief (first user message): `head -c 6000 file.jsonl`
- the final message and exit signal: `tail -c 4000 file.jsonl`
- with jq available: `jq -c 'select(.type? // "" | test("tool"))' file.jsonl | head`

## 5. If you can't find a session
Write what you searched in the review under "Locating notes" and review from the run-log and output files alone,
marking findings with lower confidence. The human can export a session manually with `/transcript save <file> --json`
from within it, or resume it with `kiro-cli chat --resume-id <id>`.
