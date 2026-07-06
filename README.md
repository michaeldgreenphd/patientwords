# PatientWords

**Patients don't speak like doctors. Medical AI must be ready to interpret them.**

Public gallery for a mechanistic-interpretability study of medical language:
how an open-weights language model (gemma-2-2b, read through Gemma Scope
transcoders) processes standard clinical terminology versus the colloquial
language patients actually use.

**Live site:** https://michaeldgreenphd.github.io/patientwords/

## What's on the site

| Section | What it shows |
|---|---|
| [Word differences](https://michaeldgreenphd.github.io/patientwords/word-differences/) | A word-for-word swap — "depression" vs. "the blues" — traced as two stacked attribution graphs |
| [Syntax differences](https://michaeldgreenphd.github.io/patientwords/syntax-differences/) | A 2×2 matrix separating the cost of the medical keyword from the cost of the surrounding phrasing |
| [Dialect differences](https://michaeldgreenphd.github.io/patientwords/dialect-differences/) | The clinical term held fixed across dialect and register variants of the framing *(traces pending)* |
| [Translation](https://michaeldgreenphd.github.io/patientwords/translation/) | Translating patient language back into clinical terms restores the circuit — and the prediction |
| [Phrase dataset](https://michaeldgreenphd.github.io/patientwords/#phrase-dataset) | Hand-measured clinical/patient sentence pairs: observed next tokens, probabilities, and links to their Neuronpedia circuit traces |
| [Model evaluations](https://michaeldgreenphd.github.io/patientwords/#model-evaluations) | Translation models scored on the same extraction task before and after translation |
| [Methods](https://michaeldgreenphd.github.io/patientwords/methods.html) | The pipeline, in plain language |

Every interactive figure is a live render: hover any node for its feature
identity, category, and attribution mass.

## Repository layout

- Root HTML pages — the gallery chrome. Fully self-contained: no build step,
  no CDNs, no external fonts.
- `modes/` — **generated** interactive renders, overwritten on regeneration;
  never hand-edited.
- `data/` — measurement data the pages fetch at load; numbers are never
  hardcoded in the HTML.

Figures and measurements are produced by a separate evaluation pipeline
(private) built on [Neuronpedia](https://neuronpedia.org),
[circuit-tracer](https://github.com/safety-research/circuit-tracer), and
[Gemma Scope](https://huggingface.co/google/gemma-scope-2b-pt-transcoders)
transcoders.

> **Status:** current renders are demonstration outputs from synthetic sample
> graphs, used to validate the visualization end-to-end; traces from live model
> runs will replace them as the study progresses. The phrase dataset is
> hand-measured on gemma-2-2b via the Neuronpedia circuit tracer.

## License

[MIT](LICENSE)
