# PatientWords

Patients don't speak like doctors. This is the public gallery for a
mechanistic-interpretability study of what that difference does inside
language models: how the same clinical situation, phrased in standard
clinical terminology versus the colloquial words patients actually use,
changes a model's next-word predictions, the circuits that produce them,
and — in a separate measured arm — the advice deployed assistants give.
Nothing here is medical advice; the study measures model behavior.

**Live site:** https://michaeldgreenphd.github.io/patientwords/

## What the study measures

- **Next-token behavior and attribution graphs** on `gemma-2-2b` (Gemma Scope
  transcoders), traced through [Neuronpedia](https://neuronpedia.org)'s hosted
  [circuit-tracer](https://github.com/safety-research/circuit-tracer): the
  probability the clinical answer loses when wording turns colloquial (the
  *wording gap*), and which tagged features carry the change.
- **Cross-model behavior** — CPU next-token measurement on ten open-weights
  models, with claim-grade per-model statistics (bootstrap CIs, corrected
  sign tests, pre-registration and a sealed confirmatory holdout).
- **Depth readouts** — Jacobian-lens per-layer readings of when the clinical
  answer forms, is lost, or never appears (observational), with activation
  patching and steering as the causal checks.
- **The advice arm** — the same scenario asked two ways of deployed frontier
  assistants; full responses archived verbatim and machine-coded against a
  draft care-urgency rubric (domain review pending).

## What's on the site

| Page | What it shows |
|---|---|
| [Start Here](https://michaeldgreenphd.github.io/patientwords/start-here/) | The study in plain language |
| [Methods](https://michaeldgreenphd.github.io/patientwords/methods.html) | The pipeline step by step, its audit, and its limitations |
| [Technical](https://michaeldgreenphd.github.io/patientwords/technical/) | The Jacobian lens, the capture-vs-hijack taxonomy, and the cross-model statistics |
| [Wording Differences](https://michaeldgreenphd.github.io/patientwords/wording-differences/) | One-word swaps and the grammar × wording 2×2, as live attribution graphs |
| [Dialect Differences](https://michaeldgreenphd.github.io/patientwords/dialect-differences/) | Clinical terms held fixed across LLM-approximated dialect/register framings |
| [Translation](https://michaeldgreenphd.github.io/patientwords/translation/) | Rewriting patient wording into clinical terms restores circuit and prediction |
| [Simulated Scenarios](https://michaeldgreenphd.github.io/patientwords/simulated-scenarios/) | The generated stress-pair corpus: every measurement, searchable, per model |
| [LLM](https://michaeldgreenphd.github.io/patientwords/llm/) | The advice arm: verbatim assistant responses to both wordings |
| [Phrase Dataset](https://michaeldgreenphd.github.io/patientwords/phrase-dataset/) | The hand-built set from real patient language, measured by hand |

Two provenances appear throughout and are always labeled: LLM-written
scenarios with real live traces, and the hand-built phrase dataset from real
patient language. Intentional misspellings in the stimuli are stress-test
stimuli, not typos. Care-urgency tier content is owner-reviewed v1, domain
review pending.

## Running it locally

There is no build system. Every page is a self-contained HTML file — inline
CSS, inline vanilla JS, no CDN, no imports.

```bash
git clone https://github.com/michaeldgreenphd/patientwords
cd patientwords
python3 -m http.server 8900        # then open http://localhost:8900/
```

Serving matters (don't open files directly): the pages fetch `data/*.json` at
load. To verify changes the way this repo's sessions do, drive the served
pages with Playwright and check for console errors, row counts that match the
payloads, working sort/filter/model switching, and intact pending/em-dash
states. The measurement side has three checks that must stay green
(run from an engine checkout): `scripts/claim_check.py`,
`scripts/validate_frontend_contract.py --site ../patientwords`, and
`scripts/seal_check.py --site ../patientwords`.

## Data architecture

This repo is presentation only; everything shown is generated or measured by
the public backend, [patientwords-engine](https://github.com/michaeldgreenphd/patientwords-engine)
(expected as a sibling checkout at `../patientwords-engine`), and refreshed by
its nightly cycle.

- `data/` — engine-written JSON the pages fetch at load. Never hand-edited;
  every number on a page traces to one of these files, a `modes/` figure, or
  page JS computing from fetched data. Highlights:
  `simulated_scenarios.json` (per-scenario measurements; `gemma-2-2b` at the
  top level, other models under `scenario.models[<id>]`, `models_meta` driving
  the model selector), `model_stats.json` (claim-grade per-model statistics),
  `urgency_shift.json` (care-urgency joins), `jlens_insights.json` /
  `jlens_depth.json` / `jlens_transport.json` / `jlens_loglens.json`
  (Jacobian-lens readouts), `advice_scenarios.json` (the advice arm's archived
  responses), `convergence.json`, `timeline.json`, `provenance.json`, and the
  collaborator export `simulated_archive.{csv,json}`.
- `modes/` — engine-generated interactive renders (self-contained HTML),
  replaced wholesale by exports, never patched here. The public set is capped
  to the most consequential scenarios; full render sets live in the engine
  repo's GitHub Releases.
- Root and per-section HTML — the gallery pages. `CLAUDE.md` records the
  working rules (data contracts, palette, accessibility floor, figure style).

## Rewriting the narrative

[`SITE_COPY_OUTLINE.md`](SITE_COPY_OUTLINE.md) holds every piece of static
prose on the site, page by page in reading order, with stable block ids for
mapping edits back to their pages. It is regenerated by the engine's
`scripts/extract_site_text.py` — regenerate rather than hand-sync.

## Citing and licenses

Cite via [`CITATION.cff`](CITATION.cff). Code (page HTML/JS and tooling) is
[MIT](LICENSE); the published data is covered by [`DATA_LICENSE.md`](DATA_LICENSE.md).
