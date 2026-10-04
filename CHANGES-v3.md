# v3: what changed and why

## Two homes for two kinds of knowledge
| Lives in | What | How it's shared |
|----------|------|-----------------|
| `sdlc-agents/` (its own team repo, cloned to `~/.kiro/sdlc`, agents linked as `~/.kiro/agents/sdlc`) | agents, skills (SOPs + templates), taxonomy, reason codes, proposals | PRs to the team repo |
| each product repo | AGENTS.md, CLAUDE.md, `.kiro/steering/*` (what is where, build commands, odd dependencies, domain rules), module AGENTS.md, `docs/adr`, `.kiro/specs/<slug>/` run artifacts | normal PRs; the curator's updates ship with the code |

## Fully native Kiro
- **Removed:** the runner, the transcript parser, the agent-config generator, `roles.json`, the context-guard
  script, and the interactive-capture hook.
- **Agents** are Kiro Markdown custom agents (frontmatter config, body prompt) with a team namespace (`sdlc/…`).
- **SOPs are Agent Skills.** They load progressively, are reusable as slash commands, and are portable to Claude Code.
- **Orchestration uses Kiro's own sub-agents and review loops.** Each sub-agent runs with its own permissions and
  context, and is recorded by Kiro as its own session.
- **Session review reads Kiro's native session storage** (orchestrator plus sub-executions) with ordinary read
  tools. The orchestrator records `/session-id` and the process version in run-log.md so the threads can be found.

## Orchestrator-led, human-in-the-loop
- You start `sdlc/orchestrator` with a ticket and plan together: the analyst researches, you answer open questions,
  the architect and critic iterate, and you approve the requirements, the design, and a `plan.md`.
- `plan.md` includes where you want checkpoints (per task, after all tasks, or before PR only). Stages are tailored
  to the work: a bug fix skips what a feature needs.
- During execution you can talk to the orchestrator at any time. It stops at your checkpoints and whenever an agent
  needs a human.

## Improvement loop
- `sdlc/improver` runs after a run. It locates the orchestrator and sub-agent sessions and fans out
  `sdlc/session-reviewer` sub-agents (up to four in parallel), one per session. The orchestrator's own thread is
  reviewed too, because its briefs shape every stage.
- Findings are routed to the right place. Repo context gaps go to the curator, then into the repo. Agent and skill
  improvements become evidence rows on proposals in the team repo, where evidence from teammates and other repos
  accumulates on the same proposal. Retros act on proposals with three or more instances across two or more runs.

## Positive, specific instructions
- A new skill, `sdlc-writing-instructions`, is used by the improver, the curator, the session-reviewer, and human
  contributors. It covers: say what to do, be specific, give the reason, calibrate emphasis, place instructions
  where the decision happens, use examples deliberately, keep one home per behaviour, prefer sharpening over
  adding, and keep hard limits in permissions. It includes before/after rewrites and a self-check.
- A new finding code, IN-NEGATIVE ("said what to avoid without saying what to do"), makes this measurable.
- Every agent and skill was rewritten in that style. Hard limits (push, merge, rm -rf, write scopes) live in each
  agent's permission rules; the prompts describe the positive workflow around them.

## Kept from v2
Finding taxonomy, reason codes (plus RC-BRIEF and RC-CONTEXT), itemized context entries with ids and delta edits,
KEEP findings, evidence thresholds, limited prompt changes per retro, and "check the effect after N runs".
