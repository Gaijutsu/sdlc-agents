# Before / after rewrites

| Before | After | Why it's better |
|--------|-------|-----------------|
| Don't modify tests to make them pass. | Keep tests as the specification: when a test looks wrong, explain why in run-log.md and ask the human before changing it. | Gives the action to take and the reason |
| NEVER skip the verification step!!! | Run the verifier after every task; its independent check is what lets the human approve without re-reading every line. | Calm, motivated, specific |
| Avoid reading too many files. | Start from the files the task names; read further only where those files call into code you need to understand. | Defines the scope positively |
| Be thorough. | Cover each acceptance criterion with a named test, including the edge cases listed in domain-rules.md. | Concrete and checkable |
| Don't forget about the database. | Schema changes use expand-then-contract: add the new column in one task, switch readers in the next, remove the old column in a later PR. | Specific procedure |
| Do not hallucinate file paths. | Confirm each path with `ls` or `rg --files` before citing it. | An action that prevents the failure |
| Don't push to main. (prompt) | Leave commits local on the feature branch; the human pushes after review. (prompt) + deny rule `git push*` (permissions) | Positive workflow in the prompt; the limit is enforced in config |
| Context entry: "Be careful with the payments module." | Context entry: "[K-0042] Payment retries are idempotent only through `IdempotencyKey`; call `charge_with_key()`, which wraps `charge()`. (src: R-refund-limits)" | Says what's true and what to do, with provenance |
