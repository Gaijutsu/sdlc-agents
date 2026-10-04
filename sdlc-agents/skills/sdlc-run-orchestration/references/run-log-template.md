# Run log: <slug>

| Field | Value |
|-------|-------|
| Ticket | <id / link> |
| Started | <date time> |
| Orchestrator session id | <paste of /session-id> |
| Process version | <git -C ~/.kiro/sdlc log -1 --format=%h> |
| Branch | <type/slug> |
| Repo | <path> |

## Ticket
<verbatim or summary with link>

## Decisions
| When | Checkpoint | Decision | Reason code | Note |
|------|-----------|----------|-------------|------|
| | G1 | approve / send back | | |

## Stages
| # | Agent | Task | Signal | Rounds | Output |
|---|-------|------|--------|--------|--------|
| 1 | sdlc/analyst | | | | requirements.md |

## Stage notes
<!-- Each sub-agent appends a section:
### <agent> <task> (round n)
- Inputs read:
- Outputs written:
- Decisions (cite principle / context ids):
- Deviations from design, with reasons:
- Follow-ups:
#### Context findings
- [fact | rule | gotcha | stale <id> | helpful <id>] statement — evidence (path:line or command) — suggested home
-->

## Team review
<notable PR review comments, pasted by the human>

## Run summary
Outcome · rounds per stage · checkpoints used · what felt slow or awkward
