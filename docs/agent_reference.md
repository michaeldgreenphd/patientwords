# PatientWords agent reference

Required alongside [AGENTS.md](../AGENTS.md) when planning changes. This is the
standing architecture, contract and research reference; exact setup and checks
live in [verify.md](../verify.md). Paths in the tables are site-root-relative;
named scripts and research documents live in sibling `patientwords-engine`
unless stated otherwise. Page prose uses a careful research-notebook voice:
short declarative sentences, exact technical terms, no marketing. Source and configuration take precedence over historical
counts or reports. Update this reference when a durable decision changes.

## No build system

Every page is a self-contained HTML file: inline CSS, inline vanilla JS, no CDN, no
imports. **Cross-page duplication of CSS/JS is deliberate** — pages must work standalone.
A change to shared behavior (masthead, chips, palette variables) means editing each page.

Semantic palette (do not change): clinical green `#15803d`, patient ink `#111827`,
structural grey `#c3c9d2`, penalty red `#b4483d`, paper `#faf9f5`, muted `#6d6c66`
(chosen for WCAG AA on paper). Serif display + mono data on the pages not listed under
*Reading pages* below; those three pages have their own type and colour rules. One page-level addition, the owner's
decision of 2026-09-29: the Multi-turn page shows its three wordings as texting bubbles
and colours each wording the same way in its charts, with colloquial blue `#2563eb`,
careful-lay amber `#b45309` and the clinical green above (white text at 5:1 or better;
colour-blind separation checked). Patient ink stays the patient colour on every other page.

## Data contracts (what page JS reads)

- `data/simulated_scenarios.json` — payload from the engine exporter. Per-scenario
  measurements for the base model (gemma-2-2b) sit at the top level; other models under
  `scenario.models[<id>]`. `payload.models_meta` drives the model-selector chips
  (`features:false` → grey the clinical-circuit meter; `graphs:false` → say "next-token
  behavior only", never imply a hidden render). Pages must fall back gracefully when
  `models_meta`/`models`/`archive` are absent (older payload shapes).
- `data/urgency_shift.json` — urgency rows joined by `(batch, batch_index, model)`;
  drives the Urgency column and downgrade badges.
- `data/model_evaluations.json`, `data/dialects.json`, `data/stress_pairs.json`,
  `data/provenance.json`, `data/simulated_archive.csv` and `data/simulated_archive.json` (collaborator download).
- `data/model_stats.json` — claim-grade per-model statistics (engine
  `paired_stats_rigor.py` site copy, models_meta embedded); drives the cross-model
  comparison in `technical/` Part 4 (`model-evaluations/` is a redirect stub
  since the 2026-07-14 consolidation). `data/convergence.json` — cumulative
  per-model penalty estimates (accumulation fold in `technical/` Part 4;
  moved from methods Fig. 5 on 2026-07-14, owner decision; methods keeps a
  pointer). `data/timeline.json` — study
  timeline from committed artifacts (simulated-scenarios strip). All three are
  written by engine operator tools that nothing schedules (`paired_stats_rigor.py`,
  `convergence_tracker.py`, `study_timeline.py`): the owner or a session runs them
  by hand, outside the publish chain (engine `scripts/README.md`, *Site data written
  outside the publish chain*); the generation-engine audit moved to
  `methods.html#generation-eval` (2026-07-10, owner-directed).

### The rest of the published set, by consuming page

The table records consumers explicitly, including files with no page consumer.
All are written by an engine script and overwritten by its next export **except
the two whose Engine writer column reads "no engine writer"** — those are hand-maintained here, and editing
them is the documented workflow. That column is load-bearing, not annotation:
the data-alteration rule below keys off it. The engine's
`../patientwords-engine/scripts/validate_frontend_contract.py --site` validates the declared payload
contracts after export. For simulated scenarios it reads the authoritative
`../patientwords-engine/scripts/contracts/simulated_scenarios.v1.schema.json` and adds semantic checks
for counts, joins and the base-model mirror. It does not derive or verify the
consumer column in this table.

| File | Read by | Engine writer |
|---|---|---|
| `advice_scenarios.json` | `llm/index.html` | `export_advice_scenarios.py` |
| `advice_coding_sample.json` | `llm/code.html` (human-coding worksheet) | `advice_human_coding.py` |
| `display_vocab.json` | **no page** (`dialect-differences/` names it only in a code comment; it fetches `dialects.json` and `provenance.json`) | `export_dialect_matrix.py` |
| `translation_scale.json` | `translation/index.html` | `translation_scale.py` |
| `drift_series.json` | `methods.html` (daily sentinel series), `technical/` | `drift_sentinel.py` |
| `tag_mass.json` | `methods.html` (attribution mass by phrasing) | `export_tag_mass.py` |
| `retrace_consistency.json` | `methods.html`, `simulated-scenarios/`, `technical/` | `retrace_consistency.py` |
| `jspace.json` | `methods.html`, `technical/` | `export_jspace.py` |
| `judge_agreement.json` | `methods.html`, `llm/index.html`, `technical/` | `export_judge_agreement.py` |
| `jev_calibration.json` | `methods.html` (Step 5b, calibrated classifier), `llm/index.html` (per-cell classifier grading) | `export_jev_calibration.py` — **run by hand from a Jev audit report, not the daily Routine** |
| `petri_register_drift.json` | `multi-turn/index.html` (exploratory register section; classifier tone on each reply of the run it read) | `export_jev_calibration.py` — **run by hand from a Jev audit report, not the daily Routine**; published only beside `jev_calibration.json` from the same report |
| `jlens_depth.json` | `methods.html`, `simulated-scenarios/`, `technical/` | `export_jlens_depth.py` |
| `jlens_loglens.json`, `jlens_transport.json` | `technical/` (j-lens chain) | `export_jlens_loglens.py`, `export_jlens_transport.py` |
| `jlens_insights.json`, `jlens_swaps.json` | `technical/` (j-lens chain) | `jlens_insights.py`, `export_pair_swaps.py` |
| `results_catalogue/index.json`, `results_catalogue/rows/*.json`, `results_catalogue/stimuli/*.json`, `results_catalogue/rows.csv`, `results_catalogue/stimuli.csv` | `results/index.html` (the results catalogue: search and filters, then the runs with five columns per run — experiment, model, measurements, run status, study context — then downloads; the status every run shares is stated once above the table and a row states its clinical-review status only where it differs; rows and prompts loaded per run, with the difference headed "everyday − medical, in probability"; run ids, part hashes, membership rules and release conditions under Methods & source; address parameters `q`, `evidence`, `stimulus`, `state`, `visibility`, `membership`, `review`, `rows`, `sort`, `issue`, `run`) | `export_results_catalogue.py` (publish chain step 6b, since 2026-11-10). Structure: `../patientwords-engine/scripts/contracts/results_catalogue.v1.schema.json`; `validate_frontend_contract.py` also checks that every named file exists, that none is orphaned and that the totals equal the per-run sums |
| `data/experiments/index.json` (path from the site root) | `experiments/index.html` (lists the published experiment comparisons; an empty list shows "No experiment comparisons published yet" with links to `results/` and `methods.html`) | `export_experiment_index.py`, run by hand after a bundle file is added or removed; not in the publish chain. Lists a bundle only when its evidence block says not synthetic, `public`, no restriction reason. Structure: `../patientwords-engine/scripts/contracts/experiment_index.v1.schema.json`; checked by `experiment_index_contract.py` |
| *(no committed file today)* a bundle the index lists, or one named by the page's `bundle` address parameter (a relative path under the site's data directory; an optional `case` parameter opens one case by its family id) | `experiments/index.html` ("Compare methods": per case the paired wording and one plot of the primary target's probability first, then the other targets, internal measurements and intervention evidence in folds; then run status, and methods & source with the labels, hashes and schema strings; target text is shown only where the bundle exports `target_text`; a synthetic bundle keeps the line "Synthetic fixture: not a measurement" in view; `noindex`, not in the navigation) | `python -m scripts.experiments.cli bundle` in the engine. No study bundle exists and synthetic fixture bundles are never published. Structure: `../patientwords-engine/schemas/experiments/bundle.v1.schema.json`. Checked by `../patientwords-engine/scripts/check_experiment_preview.py` against a synthetic bundle in a temporary copy of the site; the same script with `--serve` serves that temporary copy for a developer to open |
| `simulated_archive.csv` | `simulated-scenarios/scenario.html` (collaborator download) | `export_archive.py` |
| `simulated_archive.json` | **no page** (written alongside the CSV; staged) | `export_archive.py` |
| `model_provenance.json` | `technical/` (per-model build info) | **no engine writer** — hand-maintained here |
| `specialties.json` | `simulated-scenarios/` (specialty filter) | **no engine writer** — hand-synced from the engine's `../patientwords-engine/data/specialty_map.draft.json`; `validate_frontend_contract.py` checks the two agree |
| `petri_multiturn_summary.json` | `multi-turn/index.html` (headline, D figure, repeats table, provenance) | `export_petri_multiturn.py` (on engine `main` since 2026-09-25, 8575ef9b) — **owner-run, not the daily Routine** |
| `petri_multiturn_conversations.json` | `multi-turn/index.html` (explore viewer) | `export_petri_multiturn.py` (on engine `main` since 2026-09-25, 8575ef9b) — **owner-run, not the daily Routine** |

Every file under `data/` is classified in the engine's `../patientwords-engine/scripts/results_snapshot.py`, either as a published statistics file (`STATISTICS_FILES`) or as data a snapshot does not version. A new data file is added to one of the two lists in the engine in the same change: the engine's release check refuses a publish that changes an unclassified file, and `../patientwords-engine/tests/test_results_release.py` fails while the site tracks one.

`*.sample.json` files are development fixtures, but two ARE fetched by live pages
when the URL carries `?sample=1` (`llm/index.html` → `advice_scenarios.sample.json`,
`llm/code.html` → `advice_coding_sample.sample.json`), so their shape is part of the
contract too.

The Multi-turn page has two more sample fixtures: `petri_multiturn_summary.sample.json` and
`petri_multiturn_conversations.sample.json`. They are SYNTHETIC (placeholder text,
random grades, `"sample": true` and a `_note` saying so). They were created to build
the page before publication and remain explicit development fixtures. The current
`REAL_DATA_PUBLISHED` constant is `true`, so the page loads committed real files
by default; `?sample=1` selects the synthetic fixtures, and nothing else does. When
that constant is `false`, the page requests no result file and says that no results
are published. It shows a "sample data" notice whenever it renders the fixtures. Real
files have the same keys without `sample`. The two files are one unit: if either real
file fails to load, the page says the results did not load and draws nothing from
either file (a sample never replaces a published file). A pair that loads and lists no
triple and no conversation reads as no results published. The constant exists because
`check_pages.py` fails on any 404 under `data/`, so a fetch of the real files before
they exist would turn site CI red. The page was gated on the final
pre-registered analysis, the engine exporter on `main`, the vendor reproduction pack
(engine wave-2 decision 16) and the owner's sign-off. The owner set the pack's send
aside before publication (engine deviation D3, 2026-09-27, in
`../patientwords-engine/docs/preregistration_advice.md`): the page cites the pack and shows it as not yet
sent, and the contract gate accepts that for the one pack version the deviation
names (`../patientwords-engine/data/petri/publication_deviations.json` in the engine).

Five published files currently have **no page consumer** —
`advice_scenarios_nat.json`, `patch_profile.json`, `specialty_breakdown.json`,
`simulated_archive.json`, `display_vocab.json`. They are staged data waiting on a page; do not assume a
page breaks if they change, and do not delete them assuming they are dead. The
consumer column above is hand-maintained and nothing checks it: the 2026-09-04
fact-check found two rows missing `technical/`. `validate_frontend_contract.py`
checks file shapes, not who reads them.

## Established UI conventions

- Masthead navigation, the same markup on the 16 pages that have a masthead (edit each
  page; nothing generates it): `<nav aria-label="Site">` with four primary links
  (Start here, Scenarios, Results, Methods) and one `<details class="nav-more">`
  disclosure, "More", that holds nine links (Wording differences, Dialect differences,
  Translation, LLM responses, Multi-turn, Phrase dataset, Technical, Clinical brief,
  GitHub). It is a native disclosure, so it opens from the keyboard and without
  JavaScript. The current page's link carries `aria-current="page"`; when that link is
  inside the disclosure the summary reads "More · <page name>" (`.nav-here`).
  `experiments/` stays `noindex` and is not linked from the navigation.
  `docs/site_routes.json` states this navigation: the labels, their order, the href each
  page uses and which link is current. It also lists every public route, the five
  redirect stubs with their targets, the established anchors, and the address parameters
  and fragments a page reads at run time (`scenario.html?sim=`, `#s<N>` on the LLM page).
  No page loads the file. The engine's
  `../patientwords-engine/scripts/check_site_links.py` compares the pages with it and
  resolves every internal link and fragment. A fragment that is not an element's `id` in
  the page source passes only where the definition declares it. Change the definition in
  the same change as the pages; the command is in [verify.md](../verify.md).
  Ownership: `docs/site_routes.json` is hand-maintained in this repository. No engine
  script writes it.
- Filter/model chips: `.chip` buttons in `.chip-g` groups with `role="group"`,
  `aria-pressed` toggled with the `.on` class.
- Sortable table headers: real `<button>`s inside `th[data-key]`, `aria-sort` on the
  active `th`; first click on the Urgency column sorts most-safety-relevant first.
- Accessibility floor: skip link on every composed page (the five meta-refresh stubs and
  `share/card.html` lack one), `:focus-visible` outlines (never bare
  `outline:none`), `scope="col"` on generated headers, iframe `title`s, decorative
  preview iframes `aria-hidden`.
- Vocabulary used across flip displays: the model *hedges* (top prediction holds, loses
  probability) vs. *redirects* (top prediction changes); a redirect that drops a
  care-urgency tier is a *downgrade*.
- Display labels (2026-11-11): a label comes from an explicit map keyed on the exact stored
  value. A value with no entry is printed as stored and is never transformed, and no title
  is built from a file stem. Identifiers, versions and file names taken out of the main
  interface stay readable, word for word, in an existing Details, Provenance or Source
  section, or, where the page has no such section for them, in a title attribute or a
  link target. The engine's `tests/test_site_display_labels.py` checks this in a browser.

### Start here (owner's standing preference, 2026-11-11)

Preserve `start-here/index.html` as it is designed: the opening question, the sequence
of nine steps, the diagrams (clinician and model, the feature-map sketch, the two
translation drawings, orchestration, the Measure / Mend / Maintain cycle, the mended
system) and the interactions (the "say it the other way" toggle, the care-urgency
ladder, the cycle's three tabs). A redesign of 2026-11-10 was rejected and the page was
restored from its design of 2026-10-27 (`ac82473`). Later work makes small, justified
edits: correct a claim in place, bind a value to its record, improve a narrow-screen
drawing. A figure caption stays only where it identifies the model, explains a visual
encoding or prevents a specific misreading; it does not repeat the paragraph, narrate an
obvious arrow, repeat a site-wide status or add numerical detail the diagram does not
need. Removing a visible caption does not remove the figure's text alternative
(`aria-label`, `data-label`). A status the page's examples share is stated once in the
endnote, not in a warning block; a model's name stays beside each measured example, and
a conceptual diagram's prospective status is carried by its own paragraph and the
Sources note. The engine's `../patientwords-engine/tests/test_start_here_page.py`
and the `start-here/index.html` entries of its claims manifest check the steps, the
diagrams, the interactions and the recorded values.

### Reading pages (2026-11-11): `index.html`, `results/`, `experiments/`

These three pages were revised together as a reading path: research question, one wording
pair, its recorded result, aggregate context, internal measurements, methods and source.
The other pages keep their earlier styles; only their navigation changed. Start here is
not one of them: it keeps its own serif-and-monospace design and palette (above).

- Order. The pair and its recorded output come before aggregate context, and hashes,
  schema strings, run ids and release conditions sit under "Methods & source"
  ("Methods and source" on the homepage). A status that every item shares is stated
  once; an item repeats it only where it differs (the results catalogue's rows state a
  review status only where it is not the shared one, in the short words the page's
  `REVIEW_IN_ROW` table lists for that stored value; the whole label stays in the
  line's title, the Clinical review filter, the open run, About and Label values).
- Type. Serif for headings and prose; the system sans-serif for tables, controls and
  labels, with `font-variant-numeric: tabular-nums` on numbers; monospace only for code
  and identifiers (file paths, run ids, hashes, variant names). Sentence case, no
  letter-spaced capitals. Sizes come from five variables: `--t-body` 17 px for prose,
  `--t-ui` 14 px for controls and tables, `--t-meta` 13 px for metadata, `--t-h3`,
  `--t-h2`. No visible text is below 12 px; the engine's two page checks fail below
  that at 1280 px and at 390 px.
- Spacing and corners. One spacing scale (`--s1` to `--s7`: 4, 8, 12, 16, 24, 32, 48 px)
  and one corner radius (`--radius`, 2 px).
- Colour. The medical wording is green `#15803d` and the everyday wording is ink
  `#111827`, each beside its printed name. No value, difference or status is coloured by
  its sign or by whether it is good or bad: they are in ink, and the sign and the
  subtraction order are printed in words ("everyday − medical"). `#b4483d` appears on
  these pages only as an alert (`--alert`): a file that failed to load
  (`results/` `.cat-err`, `.det-status.is-fail`; `experiments/` `.st-error`) and a
  refused address (`experiments/` `.st-refused`). `index.html` uses no red. The engine's generated figures under `modes/` still draw their negative curve in
  red; that is engine output and is not changed here.
- Names of the wordings. "Medical wording" and "Everyday wording". The experiments page
  shows the bundle's third variant, `normalized`, as "Rewritten wording" and never prints
  that word as a label; the engine's `../patientwords-engine/docs/experiment_interface/preview.md`
  says why and where the file's own name still appears as code.
- Qualifications are stated once, where they apply: a caption under a figure, a label
  beside a value, a source note. A status shared by every item is one line, not a
  repeated block, and a load error, a missing measurement, a restriction and a review
  status keep their own wording.
- Evidence levels stay separate in headings and labels: a change in next-token
  probability, a judged answer, an internal readout, an intervention. The first-token
  probability is never labelled as a score of a whole answer.
- The homepage example is the pair the engine's `../patientwords-engine/data/editorial_pins.json`
  names as `tap_demo` (`featured.tap_demo` in `data/simulated_scenarios.json`), chosen by
  hand. The page says it was chosen and prints, from the payload at run time, where the
  pair's difference ranks among the scored pairs. Its two fallback values in the page
  source are tracked by the engine's `../patientwords-engine/data/claims_manifest.json`.
- Layout floor: no horizontal scroll at 390 px, also with every text size doubled; the
  two page checks test `results/` and `experiments/` for it.

## Figure style (standing preference)

Tufte: simple and readable. Maximum data-ink, hairline structure, direct labeling over
legends, muted context so the semantic colors carry the finding, no chartjunk. Applies to
any inline SVG/chart built on pages (the engine renders modes/ figures to the same
standard).

## Data review obligations

This repo is presentation only, so "stored data" and "schema" mean something
specific here, and a reviewer who does not know it will pass a change that
silently breaks a published page:

* **Data this repo must not alter:** `modes/` and every `data/` file with an
  engine writer in the table above are overwritten wholesale by the next export,
  so a hand edit is data loss and the fix belongs in the engine repo instead.
  **The two exceptions are hand-maintained here and editing them is the
  documented workflow:** `data/model_provenance.json`, which has no engine
  writer at all, and `data/specialties.json`, hand-synced from the engine's
  `../patientwords-engine/data/specialty_map.draft.json` with `validate_frontend_contract.py` checking
  the two agree. Rejecting an edit to those two blocks the only route they have.
* **The schema that breaks silently:** page JS fetches `data/*.json` and reads
  named fields. A payload shape change without the matching page change produces
  a blank or `undefined` cell, not an error, so a reviewer must check the
  consuming page named in the data-contracts table for every field touched. The
  engine's `../patientwords-engine/scripts/validate_frontend_contract.py --site` is the machine check.
* **Compatibility path:** older payloads exist. Pages must keep degrading to
  their pending/em-dash states when `models_meta`, `models`, or `archive` are
  absent, and a change that assumes a new field is present needs a fallback.
* **Claims are load-bearing:** every number on a page must trace to a source in
  this repo, provenance labels must stay accurate, and draft labels on
  urgency-tier content stay until the vocabulary is approved. Weakening any of
  those is a correctness finding here, not a wording preference.

## Stack and deployment

* **This repo contains no Python source.** The current checkout has no `.py` files.
  Every page is self-contained HTML with inline CSS and inline vanilla JS. Python
  appears in two places only: `python3 -m http.server` for local preview, and
  `.github/workflows/site_checks.yml`, which checks out `patientwords-engine` and
  runs its two checkers — the code stays over there. All data extraction,
  statistics, and rendering happen in the engine and arrive here as committed files. A pull request that adds a build step, a
  bundler, a framework, or a Python dependency to this repo is a change of
  architecture, not an improvement, and needs to be argued as one.
* **Served by GitHub Pages from the repository root at the project path
  `/patientwords/`.** There is no `CNAME` file and no Pages workflow: the site is
  project pages, not a custom domain, and its root is `/patientwords/`, not `/`.
* **Deployment safety.** Anything that changes how the site is served — adding a
  `CNAME`, adding a Pages workflow, moving the publishing source or directory,
  or changing DNS in front of it — gets scrutinized and must state why. These
  changes fail in production, not in review: the CI this repo has (`site_checks.yml`)
  validates payload shapes and drives the pages, and inspects nothing about how the
  site is served.

### The custom-domain trap, if a custom domain is ever added

`404.html` hard-codes the `/patientwords/` prefix in **14 absolute links** (12 before the
navigation of 2026-11-11 added Start here and Results; count them with
`grep -o 'href="/patientwords/' 404.html | wc -l`). That
is correct today and deliberate: GitHub Pages serves `404.html` for a missing
path at any depth, so relative links there would resolve against the missing
path and break. Every other page uses relative links — but **16 pages** (12
composed pages and 4 meta-refresh stubs) carry an absolute
`<link rel="canonical" href="https://michaeldgreenphd.github.io/patientwords/…">`
that hard-codes the same host and prefix and goes stale the same way. A custom
domain therefore touches `404.html` plus those 16 canonicals; count them with
`rg -l 'rel="canonical" href="https://michaeldgreenphd.github.io/patientwords' -g '*.html' -g '!modes/**' .`
rather than trusting this number.

But those 14 are absolute *and* carry the project-path prefix. **Adding a custom
domain moves the site root from `/patientwords/` to `/`, and all 14 become
404s** — on the very page a lost visitor lands on. So if a `CNAME` ever appears
in a pull request, `404.html` must change in the same pull request, and a
reviewer should treat a `CNAME` without it as an incomplete change.

## Research provenance and limitations

Every number must trace to a data field, generated figure or computation from fetched
data. Retired hand-authored demonstration renders were removed at the owner's request
(2026-07-08); a demonstration that returns must disclose that provenance in visible
labels and metadata. LLM-written scenarios with measured traces are distinct from
the hand-built real-patient-language phrase dataset. Draft urgency vocabulary stays
"draft pending domain review" until the engine's `../patientwords-engine/docs/tier_review_checklist.md`
records approval. Preserve source acknowledgments and intentional misspellings.

Historical audits establish limitations, not a fresh pass of today's checkout:

- Engine `../patientwords-engine/docs/backend_agreement_20260903.md` records a bfloat16 per-pair error
  term up to 0.032. `../patientwords-engine/docs/negative_control_20260904.md` records unstable per-pair
  penalties and flips: cite the aggregate direction, not a single pair or the
  −0.06 magnitude. The negative-control result was 36/14, p = 0.0026; those are
  audit results, not current corpus totals.
- The old site instruction describing one unfixed neighboring-token measurement
  was incomplete. Engine `../patientwords-engine/data/audits/target_reads_20261007.json` and its
  `../patientwords-engine/AGENTS.md` describe the broader audit: 63 hosted results carried another
  token's value, 40 in a published field. The hosted read path was corrected
  on 2026-10-07; new traces record exact `target_read`. That code correction
  does not establish that historical published measurements were regenerated.
  Re-measurement and republication remain an owner decision; do not patch site
  numbers or silently reinterpret old records.

When research outputs change, update their producer/provenance and the affected
public explanation together: consuming pages, `methods.html`, `technical/`, draft
labels, caption/metadata, and the engine's `../patientwords-engine/data/claims_manifest.json` where it
tracks prose. Review publication disclosures and vendor packs when the engine's
contract gate requires them. The engine's `../patientwords-engine/scripts/extract_site_text.py` writes
its working outline to `../patientwords-engine/ops/site_text_outline.Rmd` by default; it excludes runtime
JS prose. `SITE_COPY_OUTLINE.md` and `docs/site_text_outline*.md` here are historical
working copies, not automatically regenerated current truth.

## Synthetic boundary coverage

The engine's `../patientwords-engine/docs/exploratory/frontend_boundary.md` documents a separate synthetic
exporter → static HTTP resource → scenario-index browser check. Its structural
schema, OpenAPI description, generated response models and validated HTTP client
are test tools in the engine. They add no production frontend SDK or build step.
The handwritten HTTP client validates the response before using generated models;
the generated models alone do not enforce required-nullable or additive-field
compatibility. The index's real JavaScript consumes the temporary exported JSON.

Use [verify.md](../verify.md#synthetic-exporter-to-browser-check) for current commands
and a new receipt. The committed engine receipt is historical evidence of its
recorded revisions. Synthetic checks do not certify clinical correctness, current
research measurements, the detail page or a deployed site. The index has no native
sample mode; the runner inserts a visible synthetic disclosure into its temporary
copy and keeps synthetic exports out of this repository's `data/`.

[boundary-check.yml.example](boundary-check.yml.example) remains an inactive manual
workflow proposal. Activation needs separate authorization and a reviewed immutable
engine SHA; it must retain both existing site gates. Local verification does not
authorize CI activation, pushing, merging or deployment.
