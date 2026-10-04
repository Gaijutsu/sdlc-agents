# Reason codes for sending work back

Pick the one that fits best; add a short specific note. These codes are counted across runs and teammates.

| Code | The work... | Usually improved by |
|------|-------------|---------------------|
| RC-INTENT | misread what was asked | intake skill, analyst brief |
| RC-SCOPE | covered too much or too little | intake skill |
| RC-DOMAIN | missed or broke a domain rule | repo domain context |
| RC-PRINCIPLE | broke a design principle the critic or verifier missed | principles skill examples, critic/verifier skills |
| RC-REALITY | didn't match how the code actually works | repo architecture context, module AGENTS.md |
| RC-SPLIT | had badly sized or ordered tasks | design skill |
| RC-TEST | had missing, weak, or implementation-coupled tests | implement/verify skills |
| RC-DEVIATION | departed from the design without saying so | implementer agent |
| RC-ROLE | did another role's work | that agent's file, orchestrator briefs |
| RC-DOCS | left docs or the PR description short of what reviewers need | document skill |
| RC-CONTEXT | added noisy, wrong, or vague repo context | curate skill |
| RC-BRIEF | suffered from a brief that lacked needed information | orchestration skill |
| RC-TEAMREVIEW | was sent back by a teammate's PR review | note which check would have caught it |
| RC-PREF | was fine, the human prefers another way | if it recurs, encode the preference in context |
| RC-OTHER | none of the above (note required) | candidate new code |
