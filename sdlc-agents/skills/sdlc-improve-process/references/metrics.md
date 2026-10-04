# Process metrics

Counted at each retro from run-logs and reviews made since the previous retro. Append one row to
`~/.kiro/sdlc/proposals/metrics.md`; each teammate's retro adds its own row with its repo name.

- **Send-back rate**: checkpoint send-backs ÷ checkpoint decisions (by gate)
- **Rounds per task**: average implement/verify rounds
- **Design rounds**: average architect/critic rounds
- **Human stops**: NEEDS_HUMAN + BLOCKED per run (beyond planned checkpoints)
- **Team review send-backs**: RC-TEAMREVIEW per PR
- **Finding density**: findings per reviewed session, split EF / MS / IN (should fall over time)
- **Context yield**: context entries added or amended per run
- **Change hit rate**: merged changes whose target codes dropped ÷ merged changes evaluated

| Date | Who | Repo | Runs | Send-back | Rounds/task | Design rounds | Human stops | Team send-backs | EF/MS/IN per session | Context yield | Process version |
|------|-----|------|------|-----------|-------------|---------------|-------------|-----------------|----------------------|---------------|-----------------|
