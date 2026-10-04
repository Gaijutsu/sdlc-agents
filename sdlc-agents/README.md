# sdlc-agents

The team's shared Kiro agents and skills for human-in-the-loop, agentic software development. You start the
orchestrator with a ticket, plan the work together, and it runs each stage with specialist sub-agents, checking in
with you at the points you choose. After each run, an improver reviews every agent's session and turns what it
learns into better repo context and better shared agents.

Everything here is plain Kiro: Markdown custom agents, Agent Skills, native sub-agents, and native session storage.
Repo-specific knowledge lives in each product repo (see `../repo-scaffold`).

## What's in here
```
agents/        Kiro custom agents (Markdown + frontmatter); installed as sdlc/<name>
  orchestrator   run lead: plans with you, delegates, checkpoints
  analyst  architect  design-critic  implementer  verifier  documentarian  curator
  session-reviewer  improver
skills/        Agent Skills: the procedures, templates, and references each agent follows
  sdlc-run-orchestration  sdlc-intake  sdlc-design  sdlc-design-review  sdlc-implement  sdlc-verify
  sdlc-document  sdlc-curate-context  sdlc-review-session  sdlc-improve-process
  sdlc-writing-instructions  sdlc-design-principles
proposals/     evidence-backed improvement proposals (open / accepted / rejected) + metrics.md
CHANGELOG.md   process versions
```

## Install (once per machine)
```bash
git clone <this-repo-url> ~/.kiro/sdlc
mkdir -p ~/.kiro/agents && ln -s ~/.kiro/sdlc/agents ~/.kiro/agents/sdlc
kiro-cli agent list | grep sdlc/      # expect 10 agents
```
The agents reference skills with `skill://~/.kiro/sdlc/skills/...`, so the clone location matters. To also use the
skills as slash commands in ordinary sessions, link them: `for d in ~/.kiro/sdlc/skills/*; do ln -s "$d" ~/.kiro/skills/; done`.
Update with `git -C ~/.kiro/sdlc pull`. Each run records the version it used.

## Set up a product repo (once per repo)
1. Copy `repo-scaffold/` into the repo root (AGENTS.md, CLAUDE.md, `.kiro/steering/`, `docs/adr/`).
2. Start `kiro-cli chat --agent sdlc/curator` and say "bootstrap this repo". Review its DRAFT entries, correct them,
   and remove the DRAFT markers as you verify. Commit through a normal PR.
3. Add the repo's own principles to `.kiro/steering/principles.md` with a real example each.

## Run a ticket
```bash
kiro-cli chat --agent sdlc/orchestrator
> Work on PAY-482: <paste the ticket, or "see tickets/PAY-482.md">
```
The orchestrator restates the ticket, asks you to paste `/session-id` (so the run can be reviewed later), and then:
1. **Understand**: the analyst researches; you answer its open questions together → **G1** requirements.
2. **Plan**: architect designs, critic reviews (looping up to 3 rounds); you choose checkpoints → **G2** design + plan.
3. **Execute**: implementer → verifier per task as a review loop, pausing at your checkpoints.
4. **Wrap up**: documentarian writes docs and `pr.md`; curator updates repo context → **G3** you review, push, open the PR.

Talk to it at any point: ask why, redirect, change checkpoints, or take a task yourself. Ctrl+G shows sub-agent activity.

## Improve from the run
```bash
kiro-cli chat --agent sdlc/improver
> review run pay-482-refund-limit
```
The improver finds the orchestrator's session and every sub-agent session in `~/.kiro/sessions/`, sends a
session-reviewer to each, and writes `.kiro/specs/<slug>/reviews/`. Repo context gaps go to the curator.
Improvements to shared agents and skills go to `~/.kiro/sdlc/proposals/open/` as evidence. Commit those in this
repo through a PR, so teammates' evidence accumulates on the same proposals.

Every couple of weeks: `> retro`. The improver ranks proposals with enough evidence (three or more instances
across two or more runs), confirms the evidence, and drafts the exact change. The team reviews and merges.

## Contributing changes to agents and skills
- Changes arrive as proposals with evidence, or as direct PRs for obvious fixes.
- Write instructions following `skills/sdlc-writing-instructions`: positive, specific, with the reason, placed
  where the decision happens. Reviewers check new text against its self-check list.
- Keep permissions and gates as team decisions, discussed in the PR.
- Bump the CHANGELOG with what changed and which finding codes it targets, so retros can check the effect.

## Verify on your Kiro version (do this once; these are the details most likely to vary)
- [ ] `kiro-cli agent list` shows `sdlc/orchestrator` etc. (sub-directory naming).
- [ ] An agent's frontmatter `resources` resolve: ask `sdlc/analyst` "which skills and steering files do you have
      loaded?" It should list the repo's steering and its `sdlc-intake` skill (relative `file://` paths resolve
      from the workspace; `skill://~/…` expands home).
- [ ] The orchestrator can delegate to `sdlc/*` agents (`availableAgents` glob) and they run with their own permissions.
- [ ] Deny rules hold in sub-agents: ask the verifier to edit a source file and confirm it's refused.
- [ ] `fs_read` access to `~/.kiro/sessions/**` works for the improver and session-reviewer, and you can see
      which session layout your version writes (see `skills/sdlc-review-session/references/locating-sessions.md`).
- [ ] If custom agents on your version don't inherit `.kiro/steering` automatically, the explicit `resources`
      entries cover it; if you see steering loaded twice, set `chat.disableInheritingDefaultResources`.

## Claude Code
Skills follow the open Agent Skills format, so `skills/` also works from `~/.claude/skills/`. The product repo's
CLAUDE.md imports AGENTS.md and the steering files. The agent files are Kiro-specific; thin Claude Code
equivalents (`~/.claude/agents/sdlc-*.md` with `name`, `description`, `tools` and the same body) are a small,
optional addition.
