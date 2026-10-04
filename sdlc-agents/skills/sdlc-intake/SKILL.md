---
name: sdlc-intake
description: How to turn a ticket into a testable requirements.md - researching the code and domain context, writing Given/When/Then acceptance criteria with edge cases, and listing open questions with default answers. Use for the intake stage.
---
# Intake

Requirements are the contract every later stage works from: the architect designs to them, the verifier tests
against them, and the human approves them at G1. Clear requirements are the cheapest place to prevent rework.

## Steps
1. Read the brief and the ticket. Restate the request in the repo's domain terms (glossary in `domain.md`).
   Terms the glossary lacks go under "Context findings" in run-log.md.
2. Identify the actor, the trigger, the observable outcome, and the non-goals.
3. Find how the system handles this today: entry points, files, tests. Check the AGENTS.md in each module involved.
   Write "How it works today" with paths.
4. Write acceptance criteria as Given/When/Then. Add at least one edge or failure case wherever `domain-rules.md`
   lists one for this area.
5. List assumptions. Write each open question with your recommended default, so the human can answer "yes" or correct it.
6. Describe the blast radius: modules, external systems, data, public interfaces.
7. Fill in `references/requirements-template.md` at `.kiro/specs/<slug>/requirements.md`.
8. Append your section to run-log.md, including Context findings.
9. End with `NEEDS_HUMAN` if open questions remain, otherwise `STAGE_COMPLETE`.

## Done means
- A verifier could turn every criterion into a test.
- Every open question has a default answer.
- The document describes the problem and outcomes, leaving solution choices to the architect.
