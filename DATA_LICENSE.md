# Data license

The code in this repository (page HTML/JS and tooling) is licensed under the
MIT License (see `LICENSE`). This file states the terms for the **data** the
site publishes, which the MIT license does not cover. The canonical statement
lives in the engine repository
([patientwords-engine/DATA_LICENSE.md](https://github.com/michaeldgreenphd/patientwords-engine/blob/main/DATA_LICENSE.md));
this file applies the same terms to the copies published here.

## What is covered

The project-authored datasets and measurement outputs published in this
repository are licensed under
[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/):

- `data/*.json` — the published measurement payloads (scenario measurements,
  per-model statistics, urgency rows, lens readout summaries, timelines, and
  the rest).
- `data/simulated_archive.csv` / `.json` — the collaborator download.
- The figure renders under `modes/` (engine-generated from the same
  measurements).

Attribution: cite as described in `CITATION.cff` (Michael D. Green,
*PatientWords*), or link to <https://michaeldgreenphd.github.io/patientwords/>.

## What is not covered

- Third-party content fetched from external services is **not** relicensed
  here: feature auto-interp descriptions and attribution graphs originate from
  [Neuronpedia](https://neuronpedia.org)'s APIs and remain Neuronpedia content.
- Model weights and tokenizers of the measured models are distributed by their
  publishers under their own licenses.
