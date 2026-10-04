---
name: sdlc-curate-context
description: How to maintain a repo's agent context - .kiro/steering files and AGENTS.md files - as verified, itemized, growing knowledge; covers where each kind of fact belongs, the entry format, delta editing, and bootstrapping a repo. Use when curating context after a run, applying review findings, or setting up a new repo.
---
# Curating repo context

Repo context is everything an agent needs to know about *this* repository: what lives where, how to build and test
it, the odd dependencies, the domain rules, the gotchas. It lives in the repo, so the whole team and every Kiro or
Claude Code session share it, and it's reviewed in PRs like code.

## Where things go (`references/steering-layout.md` has the full layout)
| Kind of knowledge | Home |
|-------------------|------|
| Build, test, lint, run commands; environments; CI; odd dependencies; hazards | `.kiro/steering/project.md` (always loaded) |
| Repo map, layering, key patterns, where to add new things | `.kiro/steering/architecture.md` (always loaded) |
| Glossary and domain invariants | `.kiro/steering/domain.md` (always loaded) |
| Business rules, edge cases, external system quirks, intentional oddities | `.kiro/steering/domain-rules.md` (auto-included when relevant) |
| Repo-specific design principles that extend the team's | `.kiro/steering/principles.md` (always loaded) |
| How a specific module works, its local commands and gotchas | `<module>/AGENTS.md` (loaded when working there) |
| Map pointing to all of the above | root `AGENTS.md` |

## Entry format
Each fact is one bullet with a stable id and its provenance (`references/entry-format.md`):

    - [K-0042] Payment retries are idempotent only through `IdempotencyKey`; call `charge_with_key()`. (src: refund-limits, verified 2026-10-12)

Ids: K = project/architecture facts, D = domain invariants, R = rules and edge cases, X = external systems,
L = intentional oddities ("looks wrong, is right"), P = repo principles. Module AGENTS.md entries use the module
prefix, e.g. [BILLING-007].

## Curating after a run
1. Collect findings from run-log.md "Context findings" and from any review files in your brief.
2. Deduplicate: search the steering files and AGENTS.md files for the id or the key terms.
3. Verify each finding yourself against the code, config, or a command. Keep the evidence (path:line or command).
4. Apply each one as a delta:
   - **Add**: next free id in that file, with provenance.
   - **Amend**: edit in place, keep the id, append "(amended <slug>)".
   - **Deprecate**: wrap the old text in ~~strikethrough~~, add "(deprecated <slug>: reason)". The next curator
     removes deprecated entries after they've been visible in one merged PR.
   Keep every existing detail and the existing order. Context gets better by growing in specifics, so when a file
   grows past roughly 300 lines, move a module's entries into that module's AGENTS.md and leave a pointer.
5. Phrase each entry as a positive, specific statement of what's true or what to do (`sdlc-writing-instructions`).
6. Domain invariants (D-) and principles (P-) carry team decisions: write proposed additions or changes in
   context-delta.md under "Needs owner decision" for the human to take to the owner.
7. Write `.kiro/specs/<slug>/context-delta.md` from `references/context-delta-template.md`.

## Bootstrapping a repo (no slug)
Follow `references/bootstrap.md`. Draft from evidence, mark entries `DRAFT`, end with `NEEDS_HUMAN`.

## Good entries
- Specific: names files, commands, symbols, numbers.
- Verified: you checked it in this session.
- Durable: true for everyone on the team, not just one machine or one branch.
- Free of secrets and personal data.
