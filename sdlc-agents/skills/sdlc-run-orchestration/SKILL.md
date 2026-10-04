---
name: sdlc-run-orchestration
description: How the sdlc orchestrator runs a ticket end to end with a human in the loop - kickoff, co-planning, delegating stages to sdlc sub-agents, review loops, checkpoints, and recording decisions. Use when leading a run or continuing one.
---
# Running a ticket with a human in the loop

The human brings a ticket; you leave them with a reviewed branch, a PR description, and better repo context.
Along the way they make a few well-informed decisions instead of many small ones.

## Run files (all in `.kiro/specs/<slug>/`)
| File | Written by | Purpose |
|------|-----------|---------|
| run-log.md | you (sub-agents append their sections) | the run's memory: session id, process version, decisions, stage outcomes, context findings |
| requirements.md | analyst | what and why, acceptance criteria |
| design.md, tasks.md | architect | how, in task-sized pieces |
| design-review.md | design-critic | independent findings |
| plan.md | you, with the human | stages, task order, checkpoints, autonomy |
| verification-T-n.md | verifier | evidence per task |
| pr.md | documentarian | the PR description |
| context-delta.md | curator | what the repo's agent context learned |
| reviews/ | improver (after the run) | session reviews |

Use `references/run-log-template.md` and `references/plan-template.md`.

## 1. Kickoff
1. Restate the ticket in two or three sentences and confirm you've understood the goal.
2. Choose a slug (kebab-case, 2-4 words) and create `run-log.md` from the template. Fill in the date, the ticket,
   and the process version: run `git -C ~/.kiro/sdlc log -1 --format=%h` and record the result.
3. Ask the human to paste the output of `/session-id`. Record it in run-log.md; the improver uses it to find
   this conversation and every sub-agent session it spawned.
4. Read AGENTS.md and the steering files. If build/test commands, the repo map, or domain notes are missing,
   tell the human what's missing and offer a curator bootstrap pass before planning.

## 2. Understand (ends at G1)
- Brief `sdlc/analyst` (template in `references/brief-template.md`). While it works, you can discuss the ticket's
  background with the human.
- Present the analyst's open questions one at a time, each with its default answer, and write the human's answer
  into requirements.md next to the question. Questions answered from the human's knowledge of the domain often
  belong in the repo context too, so add them to run-log.md under "Context findings".
- G1: ask the human to confirm the requirements. Record the decision in run-log.md.

## 3. Plan (ends at G2)
- Brief `sdlc/architect`, then `sdlc/design-critic`. Set this up as a review loop: when the critic ends with
  `NEEDS_CHANGES`, the architect runs again with `design-review.md` as input, for up to 3 rounds. After 3 rounds,
  bring the open findings to the human.
- Tailor the stages to the work and propose them in plan.md. Typical shapes:
  - Bug fix with a clear cause: intake → short design (tasks only) → implement/verify → document → curate.
  - Feature: all stages.
  - Spike or investigation: intake → analyst research report → human decision.
- Ask the human where they want checkpoints: after each task, after all tasks, or only before the PR. Record it
  in plan.md. Recommend "after each task" for the first few runs in a repo and for risky areas.
- G2: the human approves design.md, tasks.md, plan.md, and any critic findings left open. Record it.

## 4. Execute
1. Create the branch `<type>/<slug>` from the current base with `git switch -c`.
2. For each task in plan.md order, run `sdlc/implementer` then `sdlc/verifier` as a review loop: on `NEEDS_CHANGES`,
   the implementer runs again with `verification-<task>.md`, for up to 3 rounds. Tasks marked parallel-safe in
   tasks.md can run side by side (up to four sub-agents at once).
3. After each task, add one line per stage to run-log.md: agent, signal, rounds, output path.
4. Stop and come back to the human at every plan.md checkpoint, on `NEEDS_HUMAN`, on `BLOCKED`, and after 3
   unsuccessful rounds. Bring a short summary, the relevant file paths, and the decision you need.

## 5. Wrap up (ends at G3)
- Brief `sdlc/documentarian`, then `sdlc/curator` (give it run-log.md and the branch name).
- G3: ask the human to review the branch, pr.md, and context-delta.md, then push and open the PR. Context changes
  ship in the same PR, so teammates review them along with the code.

## 6. Close
Write the "Run summary" section of run-log.md: outcome, rounds per stage, checkpoints used, and anything that
felt slow or awkward. Then suggest: "Start `sdlc/improver` with `review run <slug>` to learn from this run."
When the PR receives review comments, ask the human to paste the notable ones into run-log.md under "Team review";
they are some of the most valuable evidence the improver gets.

## Recording decisions
Every checkpoint decision goes in run-log.md's Decisions table. When the human sends work back, ask which reason
code fits best from `references/reason-codes.md` and record it with their note. Reason codes let the improver count
patterns across runs and across the team.

## Briefing sub-agents well
A sub-agent starts with only its own agent file, its skill, the repo context, and your brief. The best briefs:
- state the goal in one sentence and why it matters for this ticket
- list the input files by path, and the output file path
- include the human's relevant decisions verbatim
- name the skill to follow and the exit signals to end with
- say what "done" looks like for this stage
