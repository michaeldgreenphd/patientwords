# Local synthetic scenario-boundary check

The engine now carries a bounded exporter → static JSON → browser test of
`simulated-scenarios/index.html`. Its authoritative schema, OpenAPI description,
locked test-only tools, independent fixture, generated response models and
validated HTTP client live in `patientwords-engine/scripts/` and `tests/`.
The concise instructions and receipt are in the engine's
`docs/exploratory/frontend_boundary.md` and `frontend_boundary_receipt.json`.

No production page, payload, dependency, workflow or deployment setting changes
in this frontend branch. This check proves synthetic software behavior only;
it does not certify published measurements or clinical correctness.

`boundary-check.yml.example` is an inactive manual CI proposal, outside the
workflow directory. It records the actual immutable engine SHA rather than
trusting a same-named branch. It retains the existing two site gates and runs
only the selected offline tests and loopback browser slice. It adds test-only
package/browser downloads if later activated, no API keys or inference.

Review/merge the engine change first. With separate activation approval, review
moving the example into `.github/workflows/`; inspect its engine SHA and sparse
paths before any push. The example needs `scripts` (including contracts/client)
and `tests` in addition to the existing checker's `data`, `ops`, `docs` paths.
Do not deploy synthetic exports or copy them into this repository's `data/`.
Hosted checks have not run. The owner retains merge/deployment control.
