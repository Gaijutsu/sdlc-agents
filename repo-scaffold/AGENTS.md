# AGENTS.md

Context for AI coding agents working in this repository (Kiro, Claude Code, and others).
Kiro loads `.kiro/steering/` automatically; this file is the map for every tool.

## Start here
- Commands, environments, odd dependencies, hazards: `.kiro/steering/project.md`
- Repo map, layers, patterns, where new code goes: `.kiro/steering/architecture.md`
- Glossary and domain invariants: `.kiro/steering/domain.md`
- Repo-specific design principles: `.kiro/steering/principles.md`
- Business rules, edge cases, external systems, intentional oddities: `.kiro/steering/domain-rules.md`
- Module-specific notes: the `AGENTS.md` inside each module directory
- Decisions and their reasons: `docs/adr/`

## Sharing what you learn
When you discover something the next agent would need (a command, a gotcha, a rule), note it in your PR description
under "Context findings". The team's curator agent verifies it and adds it here, so everyone's sessions benefit.
