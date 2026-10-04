# Entry format

    - [<ID>] <positive, specific statement>. (src: <slug or doc>, verified <date>[, amended <slug>])

Examples
- [K-0003] Run unit tests with `make test-fast` (~40 s); `make test` adds integration tests and needs Docker running. (src: bootstrap, verified 2026-10-04)
- [K-0011] `libfoo` is pinned to 2.3.x because 2.4 changed float rounding in invoices; upgrading needs a migration of stored totals. (src: ADR-0007)
- [R-0019] Refunds above the original charge amount are rejected by the processor; validate before calling `refund()`. (src: refund-limits)
- [L-0004] `legacy/importer.py` swallows `KeyError` on purpose: partner feeds omit optional fields. Keep it; handle new required fields explicitly. (src: owner decision 2026-09)
- ~~[K-0007] Staging is at staging-old.example.internal.~~ (deprecated infra-move: replaced by K-0031)
