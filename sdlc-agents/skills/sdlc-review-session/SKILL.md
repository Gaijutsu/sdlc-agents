---
name: sdlc-review-session
description: How to review one recorded Kiro agent session (orchestrator or sub-agent) with hindsight - locating the session files, reading them efficiently, classifying findings, tracing downstream rework to its origin, and proposing minimal positive improvements. Use when reviewing an agent's thread.
---
# Reviewing an agent session

An independent reader with hindsight can see what the agent couldn't: where it wandered, where an instruction was
ambiguous, which fact it spent ten tool calls discovering, and which early choice caused the rework three stages
later. Your review is the evidence base for every improvement to the team's agents, skills, and repo context.

## Inputs (from your brief)
- Where the session is (session id or directory) and which agent ran it
- The run's `run-log.md` (decisions, stage outcomes, process version, team review comments)
- The output path for your review

## Steps

1. **Read the instructions first.** Open the agent file `~/.kiro/sdlc/agents/<agent>.md` and its skill. If the
   run-log's process version differs from the current one, read the versions in effect:
   `git -C ~/.kiro/sdlc show <version>:agents/<agent>.md`. Then read the brief the agent received (the first user
   message in its session) and the repo context it loaded. You are judging the fit between instructions and behaviour.

2. **Locate and size the session.** Follow `references/locating-sessions.md`. Check the file size with `wc -l`
   before reading, and read large sessions in slices (`head`, `tail`, `sed -n 'a,bp'`, `grep -n`), so your own
   context stays focused.

3. **Walk the session.** Note the line numbers of significant events: tool calls, errors, permission refusals,
   decisions, and the final message. Use `grep -n` for tool names, "error", "rejected", "denied", and the exit signals.

4. **Classify findings** with `references/finding-taxonomy.md`. For each one record: code, line refs, what happened,
   root cause layer, the minimal improvement, and your confidence.

5. **Hindsight pass.** For every downstream problem in run-log.md (critic or verifier findings, human send-backs
   with reason codes, team review comments), find the moment in this session where it could have been avoided,
   if there is one, and name what would have made the better choice natural.

6. **Context pass.** List facts the agent discovered by exploring that belong in repo context (with the evidence
   and the suggested home), context entries it used to good effect (by id), and entries that misled it.

7. **Efficiency snapshot.** Give rough counts: tool calls, failed commands, repeated reads of the same file,
   permission refusals, and the largest outputs pulled into context.

8. **KEEP.** Record behaviours that worked and should survive future edits.

9. **Write improvements** following `sdlc-writing-instructions`: each one a positive, specific instruction with
   its reason, placed in the file and section where the agent makes that decision.

10. Write the review from `references/review-template.md` and end with `STAGE_COMPLETE`.

## What makes a review useful
- Every finding cites line numbers and proposes a concrete change; findings without both are set aside at retro.
- Five sharp findings beat twenty vague ones.
- Mark a finding "single-instance" when you can't tell whether it's a pattern; the improver looks for repeats.
- Attribute causes fairly: an agent following an ambiguous instruction reasonably is an input defect (IN-), not a mistake (MS-).
- Reviewing the orchestrator: judge its briefs (did each sub-agent get what it needed?), its stage tailoring, its
  checkpoint summaries (could the human decide from them?), and how it recorded decisions.
