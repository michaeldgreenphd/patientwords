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

Since 2026-11-10 the check reads two more things from this repository. A change to
either needs the paired engine change in the same review.

- **The engine checkout step of `.github/workflows/site_checks.yml`.** The check
  builds its temporary engine layout from that step's `sparse-checkout` block
  (today `scripts`, `data`, `ops`, `docs`) plus the engine's root files. It refuses to
  run when the file has no such block, has more than one, or lists a pattern instead
  of a directory name.
- **Two sentences that print the scenario summary.** `#hero-caveat` in `index.html`
  and `#word-caveat` in `wording-differences/index.html` print
  `summary.penalty.n_phrases` and `summary.penalty.mean_phrase_deduped` from
  `data/simulated_scenarios.json`. The check loads both pages on a synthetic payload in
  which one clinical phrase occurs in two batches, and compares each sentence with a
  full sentence typed in the engine's `tests/fixtures/frontend_boundary.json`
  (`expected.summary_sentences`). Rewording one of the two sentences, or renaming one
  of the two elements, fails the check until that fixture is updated. Until 2026-11-11
  the home page printed the summary twice and a third element, `#sim-stat`, was
  compared. The synthetic payload does not hold the home page's pinned example pair,
  so the check also exercises the page's rule that the aggregate is printed from
  whatever file loaded, whether or not the example pair is in it. On those two pages only these sentences read the
  synthetic payload; the rest is this repository's published content, and the
  temporary disclosure inserted in the copy says so.

`boundary-check.yml.example` is an inactive manual CI proposal, outside the
workflow directory. It records the actual immutable engine SHA rather than
trusting a same-named branch. It retains the existing two site gates and runs
only the selected offline tests and loopback browser slice. It adds test-only
package/browser downloads if later activated, no API keys or inference.

Review/merge the engine change first. With separate activation approval, review
moving the example into `.github/workflows/`; inspect its engine SHA and sparse
paths before any push. The example needs `scripts` (including contracts/client)
and `tests` in addition to the existing checker's `data`, `ops`, `docs` paths.
The example's pytest line names five test modules. The check itself now selects
eight (`UNIT_TESTS` in the engine's `scripts/check_frontend_boundary.py`) and runs
them in its own layout, so that line is a subset, not the check's list.
Do not deploy synthetic exports or copy them into this repository's `data/`.
Hosted checks have not run. The owner retains merge/deployment control.
