---
name: sdlc-document
description: How to document a finished change for humans - maintained docs, ADR status, changelog, runbooks, and a PR description that teammates outside the flow can review from. Use for the documentation stage.
---
# Document the change

Teammates will review this PR without having watched it being made. Give them everything they need in the PR and the docs.

## Steps
1. Classify the change: behaviour, configuration, operations, public interface, or internal.
2. Update each doc that `project.md` lists as maintained and that this change affects, written for that doc's reader.
3. Set this run's ADRs to accepted.
4. Add a changelog entry.
5. For each new flag, config value, or migration, write numbered runbook steps with a rollback.
6. Write `.kiro/specs/<slug>/pr.md` from `references/pr-template.md`.
7. Append your section to run-log.md with Context findings (for example, docs that turned out to be stale).
8. End with `STAGE_COMPLETE`.
