---
name: sdlc-design
description: How to produce design.md, tasks.md and ADRs from approved requirements - studying existing patterns, choosing between options with principles, sizing tasks for single implementer sessions, and planning risk and rollback. Use for the design stage.
---
# Design

A good design lets a fresh implementer build each task correctly from the documents alone, and lets the critic
check it against reality. It's grounded in how the codebase already works.

## Steps
1. Read requirements.md (including the human's answers) and the affected code. Write "How it works today" with
   paths; the critic will open those files.
2. For non-trivial changes, describe at least two options. Choose one, citing the principles behind the choice
   (team principles skill plus repo `principles.md`), and name what you rejected and why.
3. Describe the design: components, interfaces, data changes, error handling, observability, and how the change
   is rolled out and rolled back.
4. Write an ADR in `docs/adr/NNNN-<title>.md` (`references/adr-template.md`) for each decision that is expensive to
   reverse: a new dependency, a schema change, a public interface, a cross-cutting pattern.
5. Break the work into tasks (`references/tasks-template.md`). Each task names its files and its tests, maps its
   done-criteria to AC ids, and is size S or M. Mark tasks parallel-safe when they touch disjoint files.
6. List the risks, how to notice each one, and how to back it out.
7. In a revision round, add a "Review response" table mapping each design-review finding to your change.
8. Write `design.md` (`references/design-template.md`) and `tasks.md`; append your section to run-log.md with Context findings.
9. End with `STAGE_COMPLETE`, or `NEEDS_HUMAN` when the human needs to choose between materially different designs.

## Done means
- Every AC maps to at least one task, and every task is S or M with named files and tests.
- Each ADR names the alternative it rejected.
- The design reuses the codebase's existing patterns, or an ADR explains the new one.
