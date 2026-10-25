# AGENTS.md

Canonical repository instructions; `CLAUDE.md` imports this file. Read any
applicable ancestor and nested `AGENTS.md` / `AGENTS.override.md` instructions
(including lowercase variants present in the checkout) before editing.
Any active override must also direct agents to [verify.md](verify.md).

## Start here

PatientWords is the public static research gallery. This repository displays
committed measurements and renders from sibling `../patientwords-engine`; the
engine owns generation, measurement, statistics, provenance and exports. Pages
fetch local JSON, not a live backend API. There is deliberately no build system,
Node dependency, framework or Python source here: self-contained HTML pages use
inline CSS and vanilla JS, including deliberate cross-page duplication.
The voice is a careful research notebook: short declarative sentences, exact
technical terms, no marketing.

- [README.md](README.md): purpose, page map and local preview.
- [verify.md](verify.md): canonical setup, change-specific checks and completion evidence.
- [docs/agent_reference.md](docs/agent_reference.md): required reference for data ownership,
  contracts, research limitations, UI conventions and deployment decisions.
- `index.html`, `methods.html` and section `index.html` files: authored pages;
  `simulated-scenarios/scenario.html`: detail view using `?sim=`.
- [docs/boundary-check.md](docs/boundary-check.md): the synthetic index boundary
  check and inactive workflow proposal; current commands and scope are in `verify.md`.
- `data/`: published payloads; `modes/`: generated figures;
  `.github/workflows/site_checks.yml`: actual CI gates and engine pairing.

## Working procedure

1. Read applicable nested instructions, the relevant sections of
   [verify.md](verify.md), and [agent_reference.md](docs/agent_reference.md) while
   planning. Inspect branch, working tree and both revisions before paired work;
   preserve unrelated or concurrent edits. Current source/configuration governs;
   past reports describe their recorded revisions, not today's test result.
2. Define observable success and the affected data consumer or rendered behavior.
   Make one focused change, preserving the decisions below.
3. Run the applicable verification-guide checks. Before declaring completion,
   reread its change-type and evidence sections; inspect the full diff and run
   `git diff --check`. Report exact commands, results, warnings, skips and gaps,
   including the counterpart revision/artifact for paired checks. Keep session
   logs in the completion report; preserve durable decisions in linked docs.

## Invariants

- Never patch `modes/` or engine-written data here; fix and regenerate in the
  engine. The exceptions are `data/model_provenance.json` (hand-maintained) and
  `data/specialties.json` (hand-synced from
  `../patientwords-engine/data/specialty_map.draft.json`).
  The reference's writer table defines ownership, including owner-run exports.
- Every published number traces to committed data, a figure or runtime computation.
  Keep synthetic scenarios, real measured traces and real-patient-language dataset
  provenance distinct. Keep sample notices, draft/domain-review labels, intentional
  misspellings and the provenance/acknowledgments footer.
- Preserve stable `(batch, batch_index)` identities, per-model metadata and the
  base-model compatibility mirror. `scenario.index` is display order, not a stable
  research ID. Missing measurements remain pending/em-dash states, including older
  payloads without `models_meta`, `models` or `archive`; never borrow another
  model's measurements under an unmeasured model's label.
- `../patientwords-engine/scripts/contracts/simulated_scenarios.v1.schema.json`
  defines structural compatibility; the export validator adds semantic checks. Keep its
  OpenAPI description, test client and consumer assertions consistent with changes.
- Preserve holdout/publication restrictions and reproducibility. Do not quietly
  correct historical measurements or promote one pair's penalty/flip to a research
  claim. Read the reference's measurement limitations before writing such claims.
- GitHub Pages publishes at `/patientwords/`. Deployment/source/domain changes are
  architectural changes requiring explicit justification and project-path checks.
- Both repositories are public: never commit secrets.

## Figure style

Tufte: readable figures, direct labels, hairline structure, muted context and
no chartjunk. Preserve the semantic palette and accessibility conventions in
[agent_reference.md](docs/agent_reference.md), including the Multi-turn exception.

## Dual-AI PR Review Architecture

- **Codex** audits hunk-level diff logic, local edge cases and isolated code correctness.
- **Gemini CLI ([GEMINI.md](GEMINI.md))** audits whole-repo blast radius, untouched
  downstream callers, data provenance and `patientwords-engine` ↔ `patientwords`
  contract sync. It reports only cross-file findings with both changed and untouched
  evidence; it never duplicates Codex's local syntax, type or isolated logic checks.

## Code Review Rules

Codex applies these requirements during each review:

* Flag changes that could corrupt, silently alter, or irreversibly delete stored data.
* Flag backward-incompatible API, database, configuration, or schema changes that lack a documented migration or compatibility path.
* For authentication and authorization changes, verify every relevant entry point—not only the primary request path.
* Prioritize concrete correctness, security, data-loss, and regression risks over stylistic preferences.
* Confirm that behavior-changing code has appropriate tests, or identify the specific untested behavior and resulting risk.
* Do not report formatting or lint issues that should be handled deterministically by CI.
* Include the affected scenario and evidence when reporting a finding; do not report speculative issues without a plausible failure path.

### What those rules mean in this repository

Review data-writer ownership, compatibility fallbacks and source-backed claims
against [agent_reference.md](docs/agent_reference.md). Review findings are hypotheses:
verify each against source or rendered behavior, record its disposition, and resolve
only findings actually fixed. Keep PRs focused and include compatibility notes for
cross-repository changes. The generic block above and `CLAUDE.md`'s shared-conventions
block are compared by `../patientwords-engine/tests/test_shared_conventions.py`.
Edit both repositories when changing either shared block.
