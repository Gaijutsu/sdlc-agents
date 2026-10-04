# Repo context layout

```
AGENTS.md                         map: one line per context file, plus the five things every agent needs first
CLAUDE.md                         "@AGENTS.md" (so Claude Code reads the same map)
.kiro/steering/
  project.md        inclusion: always   commands, environments, CI, odd dependencies, hazards
  architecture.md   inclusion: always   repo map, layers, patterns, where new things go
  domain.md         inclusion: always   glossary, invariants
  principles.md     inclusion: always   repo-specific principles extending the team's sdlc-design-principles
  domain-rules.md   inclusion: auto     rules, edge cases, externals, intentional oddities
<module>/AGENTS.md                  module-local knowledge (Kiro and Claude Code both pick these up)
docs/adr/                           decisions with their reasons
.kiro/specs/<slug>/                 per-run artifacts (requirements, design, tasks, run-log, reviews)
```
Keep always-loaded files tight and specific (they cost context in every session); move detail that only matters in
one area into auto-included steering or a module AGENTS.md.
