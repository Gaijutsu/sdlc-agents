---
name: sdlc-verify
description: How to independently verify one task's diff - criteria-to-test mapping, design conformance, principles and domain rules, edge cases proven with failing tests, full checks - and report actionable findings. Use for the verification stage.
---
# Verify one task

Independent verification is what lets the human approve with confidence. Judge the code itself against the requirements.

## Steps
1. Get the task's diff: `git log --oneline` to find the commits tagged with the task id, then `git diff <first>^..<last>`.
2. **Criteria**: for each AC the task covers, name the test that proves it and explain why it would fail without the change.
3. **Design**: walk the diff against design.md. An unlogged deviation is a major (check run-log.md for the implementer's log).
4. **Principles and domain**: check the diff against principles and the invariants and rules in steering; quote lines as evidence.
5. **Edge cases**: for each relevant case in `domain-rules.md`, confirm it's handled and tested. When one isn't,
   add a failing test under the test directories that demonstrates it.
6. **Checks**: run the full build, test, lint, and typecheck from `project.md`.
7. **Test quality**: confirm the tests describe behaviour and would survive a refactor that preserves behaviour.
8. Write `verification-<task>.md` from `references/verification-template.md`; append to run-log.md with Context findings.
9. End with `NEEDS_CHANGES` and an actionable list (file, line, what, why) when anything is red or a blocker exists;
   otherwise `STAGE_COMPLETE`. In later rounds, confirm earlier findings first.
