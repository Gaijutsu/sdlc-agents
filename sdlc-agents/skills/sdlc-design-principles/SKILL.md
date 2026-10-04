---
name: sdlc-design-principles
description: The team's shared software design principles with the reasoning and concrete examples behind each, used by architects, critics and verifiers to make and judge design choices. Repos extend these in .kiro/steering/principles.md.
---
# Team design principles

Each principle states what good looks like, why the team cares, and how to recognise it in a design or a diff.
Cite principles by id. Repos add their own (P-R01, …) in `.kiro/steering/principles.md`; when a repo principle and
a team principle pull in different directions, the repo principle reflects a local decision and takes precedence.

> TODO (team): replace the examples with real ones from your codebases. Agents calibrate on the examples far more
> than on the statements, so one real example per principle is worth more than any amount of explanation.

## P-01 Dependencies point inward
Domain logic depends only on domain types; adapters (HTTP, database, queues, frameworks) depend on the domain.
Why: business rules stay testable without infrastructure and survive framework changes.
Recognise: new imports into domain modules come only from domain modules.
Example: <real example: path, what it does right>

## P-02 Each module has one reason to change
Why: changes stay local and reviews stay small.
Recognise: a feature change touches the modules that own that feature's concepts.
Example: <real example>

## P-03 Invariants live in types and constructors
Validate once at the boundary and carry the guarantee in the type, so callers can rely on it.
Why: the rule exists in one place and can't be forgotten by a new caller.
Recognise: a value is validated where it's created and trusted afterwards.
Example: <real example>

## P-04 Choose the simplest design that fits
Extract an abstraction at the third concrete use; add a dependency with an ADR that names what it replaces or enables.
Why: simple code is cheaper to read, review, and change than speculative flexibility.
Recognise: each abstraction in the design has at least three users or an ADR.
Example: <real example>

## P-05 Changes are reversible
Behaviour changes ship behind a flag or with a clear rollback; schema changes use expand-then-contract across PRs.
Why: the team can ship small and back out fast.
Recognise: the design has a rollback section, and migrations and their consumers land in separate steps.
Example: <real example>

## P-06 Tests describe behaviour
Tests exercise public behaviour through the module's interface and survive refactors that preserve behaviour.
Why: tests then protect behaviour instead of freezing implementation.
Recognise: test names read as requirements; mocks sit at process boundaries.
Example: <real example>

## P-07 New paths are observable
Each new endpoint, job, or integration emits the structured logs and metrics needed to debug it in production.
Why: the first incident is diagnosed from telemetry, not from guesswork.
Recognise: the design lists what will be logged and measured.
Example: <real example>
