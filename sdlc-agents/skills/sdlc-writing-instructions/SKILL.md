---
name: sdlc-writing-instructions
description: How to write and revise instructions for LLM agents - agent prompts, skills, steering entries, AGENTS.md notes and sub-agent briefs - so they are positive, specific, motivated and placed where they will be used. Use whenever proposing or writing a change to agent instructions or repo context.
---
# Writing instructions agents follow well

Agents behave like a brilliant colleague on their first day: highly capable, with no memory of yesterday and no
knowledge of the team's norms beyond what is written down. Every instruction you write is that colleague's whole
briefing. These practices make instructions work.

## The practices

1. **Say what to do.** Describe the behaviour you want. A positive instruction gives the agent a target; a
   prohibition only removes one option and leaves it guessing what to do instead, and it puts the unwanted action
   into the agent's context.
   - Instead of "Don't refactor unrelated code" → "Keep the diff to the task; list other improvements under Follow-ups."
   - Instead of "Never guess requirements" → "When two readings of the ticket differ, write both with your
     recommended default and ask the human."

2. **Be specific.** Name the file, the command, the field, the threshold, the format. Vague instructions get vague
   compliance. "Run the tests" → "Run `make test-fast`; it finishes in about 40 seconds and covers the unit suite."

3. **Give the reason.** One clause of "why" lets the agent apply the instruction sensibly in cases you didn't
   foresee, and lets it weigh the instruction correctly against others. Current models give a reasoned instruction
   more weight than an emphatic one.
   - "Commit with the task id in the message, so the verifier can diff exactly this task."

4. **Calibrate emphasis.** Write in a calm, direct voice. Capitals, "CRITICAL", and "MUST" make agents over-apply
   a rule in places it doesn't fit. When something truly matters, explain the consequence instead.

5. **Put it where it's needed.** Agents act on the instruction in front of them at the moment of decision. Put a
   step-specific instruction in that step of the skill, a module quirk in that module's AGENTS.md, and a role-wide
   behaviour in the agent file. A rule buried in a long preamble gets lost.

6. **Sequence procedures.** Use numbered steps when order matters; describe the output format explicitly with a
   template or a short example.

7. **Use examples deliberately.** Agents imitate examples closely, including their incidental details. Use one
   short example to show a format; use two or three varied examples when you want a pattern generalised.

8. **One home per behaviour.** Each behaviour should be described in exactly one place. When two places disagree,
   the agent picks one unpredictably. When you change a behaviour, find and update every place it's mentioned.

9. **Prefer sharpening over adding.** Before adding an instruction, check whether an existing one is being
   misread; clarifying it is usually better than adding a second. Remove instructions the session reviews show
   are never relevant. Length is fine when it carries specifics; it costs attention when it carries repetition.

10. **Keep hard limits in configuration.** Things that must never happen (pushing, deleting, writing outside a path)
    belong in the agent's permission rules, where they're enforced. The prompt then describes the positive
    workflow around them: "Leave commits local; the human pushes after review."

## Revising from session evidence
When a session review shows an agent doing the wrong thing:
1. Find the instruction (or the gap) that led there. Read it as the agent would, with only its context.
2. Ask what the agent most plausibly believed it was being asked to do. The fix targets that belief.
3. Write the desired behaviour positively, with its reason, in the place where the decision happens.
4. Check for conflicts with other instructions and with KEEP findings.
5. Prefer the lightest layer: brief template, repo context entry, or skill step before agent prompt.

See `references/rewrite-examples.md` for before/after pairs.

## Self-check before you submit a change
- Does each sentence tell the agent what to do, or describe what is true?
- Would a capable newcomer know exactly what to do from this text alone?
- Is the reason given wherever the rule isn't self-evident?
- Is this behaviour described anywhere else that now needs the same update?
- Does any word shout? Replace emphasis with the consequence.
- Search the text for "don't", "do not", "never", "avoid", "must not". Rewrite each one as the positive behaviour,
  unless it's a safety boundary that is also enforced by permissions; in that case pair it with the positive alternative.
