---
name: sdlc-improve-process
description: How the sdlc improver turns real sessions into better agents, skills and repo context - coordinating per-run session reviews, routing findings, accumulating evidence on team-wide proposals, and running retros. Use for "review run <slug>" and "retro".
---
# Improving the process from evidence

Each run is an experiment. Session reviews say what happened and why; proposals collect the same pattern across
runs, repos, and teammates; the team merges the changes that the evidence supports. Improvements land in two places:
- **Shared** (`~/.kiro/sdlc`, the team's agents repo): agent files, skills, templates, taxonomy. Changed by PR.
- **Repo** (this workspace): steering and AGENTS.md. Changed by the curator, shipped in a PR.

## Mode 1 — Run review ("review run <slug>")

1. Read `.kiro/specs/<slug>/run-log.md`: orchestrator session id, process version, decisions with reason codes,
   stage outcomes, team review comments.
2. Locate the orchestrator session and its sub-agent sessions (see the `sdlc-review-session` skill's
   locating-sessions reference). List them in `reviews/summary.md` with the agent and task for each.
3. Choose what to review. Review every session in runs with send-backs, multiple rounds, `BLOCKED`, or team review
   change requests. In smooth runs, review the orchestrator plus the implementer and verifier sessions; smooth runs
   are where efficiency waste and KEEP behaviours show up most clearly.
4. Send one `sdlc/session-reviewer` per session, up to four at a time. Each brief contains: the session location,
   the agent name and task, the process version, the path to run-log.md, the downstream outcomes relevant to that
   session (for example "the verifier sent T-2 back twice for missing edge cases"), and the output path
   `.kiro/specs/<slug>/reviews/<nn>-<agent>[-<task>].md`.
5. Read the reviews and write `reviews/summary.md` from `references/run-summary-template.md`.
6. Route findings:
   - **Repo context** (IN-MISSING-CONTEXT, IN-STALE-CONTEXT, RC-DOMAIN, RC-REALITY): brief `sdlc/curator` with the
     list and the review paths. The curator verifies and applies them as a small context PR or with the next run.
   - **Shared process** (everything else with a concrete improvement): for each finding, search
     `~/.kiro/sdlc/proposals/open/` for a proposal about the same pattern (same code, same agent or skill, same
     root cause). If one exists, append your evidence row. If none does, open one from `references/proposal-template.md`.
   - **Single-instance findings** with low confidence stay in the review; they become evidence later if the pattern recurs.
7. Tell the human what you routed where, and remind them to commit the proposal files in the shared repo
   (a branch and PR per proposal works well, or one "evidence" PR for appended rows).

## Mode 2 — Retro ("retro")
Run every couple of weeks, or when a proposal reaches its evidence threshold.

1. Read every file in `~/.kiro/sdlc/proposals/open/`. A proposal is **ready** at three or more evidence rows from at
   least two runs; rows from different teammates or repos are especially strong.
2. For each ready proposal, confirm two of its evidence rows by opening the cited sessions (when they're on this
   machine) or the cited reviews. Mark evidence you couldn't confirm.
3. Draft the exact change following `sdlc-writing-instructions`, choosing the lightest layer that fixes the pattern:
   brief template → skill reference/template → skill step → agent file. Repo-specific patterns go to the curator instead.
4. Check the draft against the KEEP findings related to that agent or skill, and against other ready proposals
   touching the same file, so changes don't conflict.
5. Pick up to three ready proposals that touch agent files or skill steps for this retro, so the effect of each
   can be seen in the next runs. Template and reference improvements can go alongside.
6. Review merged changes that are due: read reviews from runs made after the change (their process version is
   in run-log.md) and report whether the targeted finding codes dropped. Recommend keep, adjust, or revert.
7. Update `~/.kiro/sdlc/proposals/metrics.md` (definitions in `references/metrics.md`) and end with a short ranked
   summary for the human.

## Principles for good changes
- Build on what works: KEEP findings describe behaviour to preserve.
- Prefer sharpening or removing an instruction over adding one; add when the reviews show a real gap.
- Repo knowledge accumulates as specific entries, so the curator grows context in detail and splits large files
  into module AGENTS.md files rather than summarising them.
- Every change states the finding codes it should reduce, so the next retro can tell whether it worked.
- Gates, permissions, and safety rules are the team's decision: describe the evidence and leave the change to them.
