# Finding taxonomy

Fixed codes so findings can be counted across runs, repos, and teammates. New codes are added through a proposal.

## EF — wasted effort
| Code | What happened | Typical root cause |
|------|---------------|--------------------|
| EF-REREAD | read the same file repeatedly with no new purpose | missing summary in context; no note-taking step |
| EF-WANDER | explored code unrelated to the task | vague brief; missing repo map |
| EF-RETRY | repeated a failing command without changing approach | missing troubleshooting fact; no stop rule |
| EF-BLOAT | pulled huge outputs into context (whole files, full logs) | no "search first, then read the slice" guidance; verbose test command |
| EF-LATE | found key information late that was already available | context not loaded or not prominent |
| EF-OVERWORK | went beyond the task | scope wording |
| EF-TOOL | used a clumsy tool for the job | missing tool guidance |

## MS — mistakes
| Code | What happened |
|------|---------------|
| MS-INSTRUCTION | misread or overlooked a clear instruction |
| MS-STEP | skipped a skill step |
| MS-ASSUME | acted on an unverified assumption |
| MS-INVENT | cited a file, symbol, command, or API that doesn't exist |
| MS-TEST | weakened, skipped, or implementation-coupled tests |
| MS-SCOPE | worked outside its role or task |
| MS-SIGNAL | ended with a wrong, missing, or premature exit signal |
| MS-DEVIATION | departed from the design without logging it |
| MS-DOMAIN | broke a domain rule or invariant |
| MS-PRINCIPLE | broke a design principle |

## IN — input defects (the system's to fix)
| Code | What happened |
|------|---------------|
| IN-AMBIGUOUS | an instruction allowed several reasonable readings |
| IN-CONFLICT | two instructions pulled in different directions |
| IN-NEGATIVE | an instruction said what to avoid without saying what to do, and the agent filled the gap poorly |
| IN-MISSING-CONTEXT | the agent had to discover something that belongs in repo context |
| IN-STALE-CONTEXT | a context entry was wrong or outdated (cite its id) |
| IN-BRIEF | the orchestrator's brief lacked something the sub-agent needed |
| IN-FRICTION | a legitimate action was blocked by permissions or tooling |
| IN-TEMPLATE | a template lacked a needed field, or had a field nobody fills meaningfully |
| IN-UPSTREAM | the problem originated in an earlier stage's output |

## KEEP
| Code | What happened |
|------|---------------|
| KEEP | a behaviour that clearly worked and should survive future changes |

## Root cause layers
agent file · skill · skill reference/template · orchestrator brief · repo context (steering / AGENTS.md) ·
permissions · upstream stage · model capability
