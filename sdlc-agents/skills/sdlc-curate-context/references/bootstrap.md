# Bootstrapping repo context

Goal: a first version of the steering files that an agent can start from, every entry backed by evidence, and
clearly marked for the human to verify.

1. **Commands**: read package manifests, build files, Makefiles, CI workflows, Dockerfiles, and README. Record
   build, test (fast and full), lint, typecheck, and run commands exactly as CI runs them.
2. **Repo map**: list top-level directories and the main entry points; identify layers and where tests live.
3. **Odd dependencies**: pinned versions with comments, vendored code, forks, private registries, system packages,
   services needed for tests.
4. **Domain**: collect recurring nouns from models, schemas, and API types for the glossary; collect edge cases from
   test names and fixtures for domain-rules.md; collect external systems from config and clients.
5. **Hazards**: slow or flaky test markers, migration directories, generated code, files with "do not edit" headers.
6. Write each entry with `DRAFT` after the id and the evidence path:
   `- [K-0001] DRAFT Build with `make build`. (evidence: Makefile:12, .github/workflows/ci.yml:30)`
7. Create root AGENTS.md as a map, and CLAUDE.md containing `@AGENTS.md`.
8. End with `NEEDS_HUMAN`, listing the entries you're least sure about first. The human removes `DRAFT` as they verify.
