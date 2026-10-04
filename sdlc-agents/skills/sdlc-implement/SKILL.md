---
name: sdlc-implement
description: How to implement exactly one task - test-first from done-criteria, smallest change in local style, finishing green, logging deviations, committing with the task id. Use for the implementation stage.
---
# Implement one task

A small, test-backed diff that matches the design is fast to verify and pleasant for teammates to review.

## Steps
1. Read the task row in tasks.md, the design sections it cites, and the files it names. Read further only where
   those files call into code you need to understand. In a revision round, read `verification-<task>.md`.
2. Write or extend tests that encode the done-criteria. Run them and confirm they fail for the expected reason.
3. Make the smallest change that passes, matching the patterns of the surrounding code.
4. Run the build, test, lint, and typecheck commands from `project.md`. Iterate until all are green.
   When a test itself seems wrong, write your reasoning in run-log.md and end with `NEEDS_HUMAN`, leaving the test as is.
5. Compare your change to the design. Log each deviation with its reason in run-log.md. When the design can't work
   as written (an interface or data shape has to change), end with `BLOCKED: <what and why>`.
6. Commit: `<type>(<scope>): <summary> [<slug> <task-id>]`. Set the task's status to `done` in tasks.md.
7. Append your section to run-log.md: files changed, tests added, deviations, follow-ups, Context findings
   (especially commands, setup steps, or gotchas you had to figure out).
8. End with `STAGE_COMPLETE`.

## Done means
- Green locally on the repo's full check set.
- The diff contains the task's files and their tests.
- Deviations and follow-ups are logged.
