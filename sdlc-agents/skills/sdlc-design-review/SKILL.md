---
name: sdlc-design-review
description: How to independently review a design and task breakdown - coverage, principles, domain invariants, reality check against the code, task completability, likely production failure - with severity definitions. Use for the design-review stage.
---
# Design review

An independent review catches the expensive problems while they're still cheap. Report what you find with evidence;
the architect decides how to fix it.

## Severity
- **Blocker**: the design can't meet a requirement, breaks an invariant, or can't be built as written.
- **Major**: it will cause rework, an incident, or a principle violation that the team would reject in review.
- **Minor**: worth fixing, low cost of leaving it. Report the five that matter most.

## Steps (in order)
1. **Coverage**: map each AC to its tasks. A missing AC is a blocker.
2. **Principles**: check each team and repo principle against the design; quote the design text as evidence.
3. **Domain**: check each invariant in `domain.md` and the edge cases in `domain-rules.md` for this area.
4. **Reality**: open the files named in "How it works today" and in the tasks. A mismatch with the code is a major.
5. **Tasks**: could a fresh implementer finish each task from what's written? Vague done-criteria are a major.
6. **Production**: name the most likely incident this change could cause and whether the design handles it.
7. Write `design-review.md` from `references/design-review-template.md`.
8. Append your section to run-log.md with Context findings (for example, code that contradicts a context entry).
9. End with `NEEDS_CHANGES` for any blocker or more than three majors; otherwise `STAGE_COMPLETE`.

In rounds 2 and 3, first confirm each earlier finding is resolved (cite where), then check the changes for new problems.
