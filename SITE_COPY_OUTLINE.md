# PatientWords — site copy outline

Every piece of static prose on the public site, page by page, in reading order —
for reviewing and rewriting the narrative. Nothing here is reworded or corrected:
extraction is byte-exact (the intentional misspellings in stimuli are stress-test
stimuli and must survive any rewrite).

**Provenance.** Generated 2026-07-30 by the engine's `scripts/extract_site_text.py`
(`python scripts/extract_site_text.py --site-root ../patientwords`), supplemented with
`llm/code.html` and `simulated-scenarios/scenario.html` through the same parser. The
historical home of this outline is the engine repo's `ops/` (2026-07-09 directive);
this root copy exists at owner request, 2026-07-30. Regenerate rather than hand-sync.
The `index.html` and `start-here/index.html` sections were regenerated on 2026-11-11 with
the same script: `index.html` after its rewrite, and `start-here/index.html` after it was
restored to its design of 2026-10-27 (headings moved one level down to match this file); every other section is as generated on 2026-07-30, and the pages added
since then (`multi-turn/`, `results/`, `experiments/`) are not in this copy.

**How to use it.** Each block is preceded by an HTML comment id
(`<!-- id: <page>.bNNN -->`) mapping it back to its page and position — keep the
comments and do not reorder blocks; to cut text, empty the block but keep its id.
Text that page JS builds at runtime from the data files (tables, counts, chart
labels, captions filled from payloads) is not extractable statically; each page
section says so once. Redirect stubs (`word-differences/`, `syntax-differences/`,
`answer-depth/`, `model-evaluations/`, `llm/natural.html`) carry no prose of their
own — their content lives on the pages that absorbed them. Site navigation is
excluded; the provenance & acknowledgments footers are captured and are
load-bearing — reword only with equal precision.

## PatientWords — does wording change what AI predicts? — `index.html`

> ⚑ meta description: PatientWords compares the same clinical situation written in everyday patient wording and in medical wording, and records in small open-weight language models the probability of the first token of a chosen target word. Simulated stimuli; clinical review pending.

<!-- id: index.b001 -->
### Does wording change what AI predicts?

<!-- id: index.b002 -->
*subtitle:* PatientWords writes the same clinical situation twice, in everyday wording and in medical wording, and measures how a language model’s next-token prediction differs. If models respond less well to everyday words, the people affected are those who describe symptoms in their own language.

<!-- id: index.b003 -->
gemma-2-2b and other models · small open-weight language models · endpoint: the probability that the next token is the first token of a chosen target word

<!-- id: index.b004 -->
### One pair and its recorded result

<!-- id: index.b005 -->
Example pair · gemma-2-2b · model-generated prompts · clinical review pending

<!-- id: index.b006 -->
“When the dust kicks up my asthma flares, so at work I keep a spare ___”

<!-- id: index.b007 -->
“When the dust kicks up my chest gets all tight, so at work I keep a spare ___”

<!-- id: index.b008 -->
#### Probability that the next token is the first token of the target word “inhaler”

<!-- id: index.b009 -->
The recorded values load with JavaScript. They are also on the scenario pages and in the data file.

<!-- id: index.b010 -->
Chosen by hand as an illustration (editorial pin). Its difference is among the largest in the published file; it is not a typical pair.

<!-- id: index.b011 -->
Open this pair's record Open its attribution graphs Browse all scenarios New to this? Start here

<!-- id: index.b012 -->
### What is measured

<!-- id: index.b013 -->
One token’s probability after an unfinished sentence: a small, repeatable measurement of a model, not an assistant’s reply, its clinical quality or an effect on patients. Whole replies are measured separately. Whether the two wordings of a pair are clinically equivalent has not yet been reviewed. Everyday wording is not defective language; the question is whether models and instruments handle it as well as medical wording.

<!-- id: index.b014 -->
### Internal measurements

<!-- id: index.b015 -->
An attribution graph is computed for one prompt. It lists the features an instrument (a transcoder trained on gemma-2-2b) finds in the model's activations and estimates how much each contributed to the predicted token. It is a readout from that instrument: a difference between two wordings’ graphs is not by itself a causal explanation. The methods page describes the intervention checks.

<!-- id: index.b016 -->
*caption:* The example pair, traced Two attribution graphs of the pair above: the medical wording on top, the everyday wording below. The preview shows the top of the figure. It is a later re-trace of the pair, so the probabilities printed in it can differ slightly from the recorded values above.

<!-- id: index.b017 -->
Open the full comparison on the Wording differences page

<!-- id: index.b018 -->
*fold:* How to read this graph

<!-- id: index.b019 -->
Columns are the prompt's words in order; height is depth in the model; the predicted next token sits at the top with its probability. Each dot is a feature, and its size is its attribution. Its colour is the label the instrument gives it: green for a feature labelled medical (the figure's legend says clinical), dark ink for a feature labelled everyday (the legend says off-target), grey for structural context. Curves are attribution paths; a red curve has a negative weight. Hover a dot in the full figure for its identity and size.

<!-- id: index.b020 -->
*fold:* Trace details

<!-- id: index.b021 -->
Model gemma-2-2b · circuit-tracer via Neuronpedia · traced July 7, 2026 · render re-traced July 30, 2026 · the example scenario of the simulated sentences

<!-- id: index.b022 -->
*caption:* A rewritten sentence, traced A language model rewrote an everyday sentence in medical terms, and the rewrite was traced in the same way. Recorded target-token probability in this case: 0.45 after translation (clinical baseline 0.26) · July 7 trace. One traced case; the Translation page gives every reviewed case, including those where the probability did not return.

<!-- id: index.b023 -->
Open the Translation page

<!-- id: index.b024 -->
*fold:* Trace details

<!-- id: index.b025 -->
Model gemma-2-2b · hosted circuit-tracer via Neuronpedia · traced July 7, 2026 · render re-traced July 30, 2026 · phrase 17 of a reviewed set of pairs in which the most probable next token moved to a lower level of the draft care-urgency ladder

<!-- id: index.b026 -->
### More comparisons

<!-- id: index.b027 -->
- Simulated scenarios · every published pair with its measurements and traces

<!-- id: index.b028 -->
- Results catalogue · every measured run, with its status and what it may be used for

<!-- id: index.b029 -->
- Wording differences · one-word swaps, and wording crossed with grammar

<!-- id: index.b030 -->
- Dialect differences · one instruction in several language-model-written approximations of English varieties

<!-- id: index.b031 -->
- Translation · rewriting the everyday sentence in medical terms, case by case

<!-- id: index.b032 -->
- LLM responses · whole replies of deployed assistants, judged; a different endpoint from the one above

<!-- id: index.b033 -->
- Multi-turn · wording across a whole conversation

<!-- id: index.b034 -->
- Phrase dataset · a hand-built set of pairs, assembled by Michael D. Green on Neuronpedia

<!-- id: index.b035 -->
- Urgency of the most probable next token · per-model statistics on a draft care-urgency ladder: tiers owner-reviewed v1 · domain review pending

<!-- id: index.b036 -->
- Clinical brief · a short version for clinicians

<!-- id: index.b037 -->
- Technical page · layer-by-layer readouts and model comparisons, for AI researchers

<!-- id: index.b038 -->
### Methods and source

<!-- id: index.b039 -->
The methods page describes the pipeline step by step, with its limitations. The example pair and the summary on this page are read, when the page loads, from the scenario measurements file; the paraphrase comparison is read from the provenance file.

<!-- id: index.b040 -->
Simulated data. The sentence pairs across this site are written and checked by language models; the predictions and traces are recorded model behaviour. The phrase dataset is the exception: Michael D. Green assembled its pairs by hand on Neuronpedia. The team is interviewing patients about how they use language models and what they ask them.

<!-- id: index.b041 -->
*footer (provenance):* Built with the patientwords-engine pipeline on Neuronpedia · attribution graphs by circuit-tracer · every number on this page traces to a data file in this repository · how the pipeline works

*Not extracted: text this page's JS generates at runtime from data files (tables, counts, chart labels).*

## Start Here — PatientWords — `start-here/index.html`

> ⚑ meta description: A plain-language introduction: doctors interpret many ways of saying the same thing; a language model can answer each one differently. What we trace and measure.

<!-- id: start-here.b001 -->
*dateline:* Start here · the whole idea simplified

<!-- id: start-here.b002 -->
### People say the same thing many ways. What does a machine "hear"?

<!-- id: start-here.b003 -->
*subtitle:* What happens inside a language model when the same medical question is asked in patient words instead of clinical words.

<!-- id: start-here.b004 -->
Research question

<!-- id: start-here.b005 -->
Does the language patients use change how a language model responds to their situation, compared with standard medical wording? To find out, we pair everyday phrasings of a health concern with their medical equivalents, record which internal features of the model each phrasing activates, and measure how far the everyday wording moves the model’s next-word prediction away from a medical target.

<!-- id: start-here.b006 -->
Scope: the models studied here are open-weight, chosen so their internal activity can be traced directly. Whether the same effects hold in larger closed-source models is an open question; a pilot with deployed assistants is on the LLM responses page.

<!-- id: start-here.b007 -->
The next word is a small, repeatable measurement: how probable is the first piece of a chosen medical word after an unfinished sentence? It is not an assistant’s advice; whole replies are studied separately. The circuit view (step 5) shows which internal features differ between the wordings: a readout, not proof of a cause.

<!-- id: start-here.b008 -->
1 · A doctor converges

<!-- id: start-here.b009 -->
### Three phrasings, one interpretation

<!-- id: start-here.b010 -->
Patients rarely use words that appear in medical textbooks. A clinician can understand multiple different wordings, recognizes the same stomach problem, and reaches the same recommendation.

<!-- id: start-here.b011 -->
Illustration · interpretation absorbs the wording

<!-- id: start-here.b012 -->
· Why it matters

<!-- id: start-here.b013 -->
### Why wording matters

<!-- id: start-here.b014 -->
If an assistant responds less well to everyday words, the people affected are those who describe symptoms in their own language, often those with the least access to clinical vocabulary. The direction that worries us most is understating urgency. This motivates the work; we measure models here, not yet patients.

<!-- id: start-here.b015 -->
2 · The model diverges

<!-- id: start-here.b016 -->
### Three phrasings, three different predictions

<!-- id: start-here.b017 -->
We gave a language model the same complaint in three phrasings and recorded its most likely next word. After the medical phrasing it is the start of “antacid”. After the other two it is a food word, even in the sentence that uses a formal term.

<!-- id: start-here.b018 -->
Gemma 2 2B · model-generated prompts · clinical review pending · the model predicts word pieces: “ant” begins “antacid” · the formal-term row is one case

<!-- id: start-here.b019 -->
3 · Try it

<!-- id: start-here.b020 -->
### Watch wording change the prediction

<!-- id: start-here.b021 -->
A language model works by guessing the next word. Flip the phrasing and watch its guesses reshuffle.

<!-- id: start-here.b022 -->
“When the dust kicks up my asthma flares, so at work I keep a spare ___”

<!-- id: start-here.b023 -->
Gemma 2 2B · model-generated prompts · clinical review pending · a hand-picked pair with one of the largest differences · “inhaler” is recorded as its first piece, “inhal” · open scenario 85’s full trace · browse all scenarios

<!-- id: start-here.b024 -->
4 · What we measure

<!-- id: start-here.b025 -->
### Two numbers per sentence pair

<!-- id: start-here.b026 -->
How far the target word’s probability falls when the wording turns everyday, and whether the most likely next word changes. When it changes to a word lower on our draft care-urgency ladder (like “inhaler” becoming “shirt” in step 3), we count an urgency downgrade.

<!-- id: start-here.b027 -->
5 · Look inside

<!-- id: start-here.b028 -->
### Looking inside the prediction

<!-- id: start-here.b029 -->
A circuit trace is a look inside the guess you see in step 3. It records which internal features are active as the model reads, in the instant before it predicts a word. In the sketch below, the medical term lights up features labelled medical (teal); the everyday phrase lights up more everyday ones (dark).

<!-- id: start-here.b030 -->
*fold:* Read more about circuit traces

<!-- id: start-here.b031 -->
Inside the model, small units called “features” switch on as it reads. Some respond to medical ideas; others to non-medical ones. A circuit trace records which features fired and how strongly each fed the predicted next word. The trace is a diagnostic that researchers compute from the model’s internals with a separate instrument. A difference between two traces shows what that instrument reads; it does not by itself show why the prediction changed, which takes an intervention (see Methods). We also ask whether the instrument itself picks up medical terms more readily than everyday descriptions; that is an open question.

<!-- id: start-here.b032 -->
Illustration of a trace’s layout · larger node = stronger influence · faint = barely fired · the recorded traces of this pair hold 732 and 787 features and share 465; the sketch draws a few

<!-- id: start-here.b033 -->
Most figures on PatientWords are circuit traces like this sketch.

<!-- id: start-here.b034 -->
6 · The patch

<!-- id: start-here.b035 -->
### A translation layer, for now

<!-- id: start-here.b036 -->
One stopgap we tested is a clinical translator. It sits between the patient and the model and, before the model ever answers, rewrites the everyday sentence into medical wording.

<!-- id: start-here.b037 -->
Gemma 2 2B · one recorded case, sentences shortened · the dashed path was not measured · in other reviewed cases the rewrite did not restore the prediction

<!-- id: start-here.b038 -->
See the live translation traces.

<!-- id: start-here.b039 -->
7 · The smart patch

<!-- id: start-here.b040 -->
### Beyond translation: Orchestrating care

<!-- id: start-here.b041 -->
A rewrite is fragile. An intermediary could instead route a query by confidence and context, and ask for more detail when the wording is ambiguous.

<!-- id: start-here.b042 -->
Research direction · illustration

<!-- id: start-here.b043 -->
8 · The lasting fix

<!-- id: start-here.b044 -->
### Measure, mend, maintain: a cycle, not a patch

<!-- id: start-here.b045 -->
No single fix closes this gap. Language evolves; dialects, slang, and communities change, and a test built once goes stale. The method has to be a loop.

<!-- id: start-here.b046 -->
- Pair each medical phrasing with its everyday phrasing. Count how often the most likely next word drops in urgency.

<!-- id: start-here.b047 -->
- nowsimulated phrases, pre-registered, a tenth sealed for checking.

<!-- id: start-here.b048 -->
- nextreal patient language, clinician-checked, community-validated dialects.

<!-- id: start-here.b049 -->
- Fortify the model: put a line of medical context in front of the question.

<!-- id: start-here.b050 -->
- Train on patient language: include the way people actually speak in the training data. Models learn idioms, misspellings, and dialects the way clinicians do.

<!-- id: start-here.b051 -->
- Translate only behind a regression check: re-test every rewrite, because rewrites can lose clinical content.

<!-- id: start-here.b052 -->
- Re-run the audit on a schedule.

<!-- id: start-here.b053 -->
- Refresh the phrase sets and urgency of recommendations with clinician and community review.

<!-- id: start-here.b054 -->
- Stress-test the edges with supplementary sets.

<!-- id: start-here.b055 -->
- nextMore edge sets: alarm-sounding wording, misspellings.

<!-- id: start-here.b056 -->
- Watch the circuit for drift as models update.

<!-- id: start-here.b057 -->
#### Two kinds of loss, two kinds of fix

<!-- id: start-here.b058 -->
A layer-by-layer readout shows where the target is lost: some targets form and drop out at the last step, some never form at all. The running census, pair by pair, lives on the Technical page; the methods page shows the causal check.

<!-- id: start-here.b059 -->
9 · The mended system

<!-- id: start-here.b060 -->
### Closing the loop: Native orchestration and human handoff

<!-- id: start-here.b061 -->
The goal is a model that no longer relies on a translation patch. It would map patient wording to safe clinical pathways itself, giving immediate guidance (while communicating confidence) and handing off to human clinicians.

<!-- id: start-here.b062 -->
Research direction · illustration

<!-- id: start-here.b063 -->
SIMULATED DATA: the sentence pairs measured across this site are written by an LLM and checked automatically.

<!-- id: start-here.b064 -->
*footer (provenance):* Built with the patientwords-engine pipeline on Neuronpedia · attribution graphs by circuit-tracer ·

*Not extracted: text this page's JS generates at runtime from data files (tables, counts, chart labels).*

## Methods — PatientWords — `methods.html`

> ⚑ meta description: How PatientWords works: gemma-2-2b with Gemma Scope transcoders, circuit-tracer attribution graphs via Neuronpedia, feature tagging, and the comparison engines.

<!-- id: methods.b001 -->
*dateline:* Methods · how the pipeline works

<!-- id: methods.b002 -->
### From a sentence to a circuit, step by step.

<!-- id: methods.b003 -->
*subtitle:* Every figure starts as two (or four) plain sentences, one in clinician wording and one in patient wording, and ends as an interactive map of the computation gemma-2-2b performs on it.

<!-- id: methods.b004 -->
Step 1 · Model & features

<!-- id: methods.b005 -->
### Splitting the model’s activity into readable features

<!-- id: methods.b006 -->
The study’s subject is gemma-2-2b, a small open language model (Google DeepMind, released July 2024). Watched directly, its inner workings are millions of undifferentiated numbers.

<!-- id: methods.b007 -->
*fold:* How transcoders split numbers into features

<!-- id: methods.b008 -->
Google DeepMind’s Gemma Scope transcoders split those numbers into distinct, readable categories called features. Each feature fires for one recognizable thing. These features help us see which parts of the model’s thinking a sentence switches on.

<!-- id: methods.b009 -->
Step 2 · Attribution

<!-- id: methods.b010 -->
### Tracing which features pushed the model to its next word

<!-- id: methods.b011 -->
For each sentence we run circuit-tracer through Neuronpedia to build an attribution graph: a map of which features, at which depth and position in the sentence, pushed the model toward its next word. Each connection carries a weight: the influence one feature’s firing had on another’s, and on the word the model chose. The technical term for that weight is attribution mass.

<!-- id: methods.b012 -->
*fold:* View repeatability and validation metrics

<!-- id: methods.b013 -->
The instrument repeats itself, within the record we have. Source: the repeatability measurements file on the patient words GitHub.

<!-- id: methods.b014 -->
Step 3 · Tagging

<!-- id: methods.b015 -->
### Every feature gets sorted: clinical, off-target, or structural

<!-- id: methods.b016 -->
Every feature that fires while the model reads gets one of three tags, by what makes it light up:

<!-- id: methods.b017 -->
- Clinical — fires on the medical idea, the reasoning we want (a feature for acid, reflux, heartburn).

<!-- id: methods.b018 -->
- Off-target — fires on something the casual wording dragged in, not the medicine. Say a patient writes “my stomach’s on fire”: a feature for heat or spicy food lights up and tugs the next word toward “ice cream.” That feature is off-target — features like it produce the wording gap.

<!-- id: methods.b019 -->
- Structural — scaffolding for syntax, position, and punctuation. It fires in every trace since it is a part of complete sentences.

<!-- id: methods.b020 -->
*fold:* The formula behind these bars

<!-- id: methods.b021 -->
Each traced pair contributes one split per phrasing, rebuilt from two committed batch-summary scalars: C, the clinical-tagged fraction of transcoder-feature attribution mass (a feature’s mass is the summed |edge weight| incident to it), and E, the share of attribution mass on MLP reconstruction-error nodes — the part of the computation the feature basis does not explain. The three segments, summing to 1:

<!-- id: methods.b022 -->
clin = (1 − E) · C off = (1 − E) · (1 − C) struct = E

<!-- id: methods.b023 -->
The corpus figure is the mean of these splits, per phrasing, across measured gemma-2-2b pairs — the one model whose public transcoders make the clinical tag meaningful — with sealed holdout pairs excluded; displayed values are rounded so the three sum to exactly 100. The caption above discloses whether the bars currently show that measured mean or the illustrative placeholder.

<!-- id: methods.b024 -->
Step 4 · Comparison

<!-- id: methods.b025 -->
### Four views put the two phrasings side by side

<!-- id: methods.b026 -->
The tagged graphs feed four comparison views:

<!-- id: methods.b027 -->
- Wording: the word swap clinpat

<!-- id: methods.b028 -->
- Wording: the grammar swap

<!-- id: methods.b029 -->
- Dialect Differences

<!-- id: methods.b030 -->
- Translation pat → clin

<!-- id: methods.b031 -->
What the wording changes, before the answer. Illustrative schematic — the example words and concept tags are hand-authored, not a measurement. Clinical wording lights up medical concepts inside the model (the “J-space” the Jacobian lens reads); the same situation in patient words lights up everyday ones, and that redirects the next word.

<!-- id: methods.b032 -->
“My dyspepsia flared up.”

<!-- id: methods.b033 -->
“My stomach’s on fire.”

<!-- id: methods.b034 -->
*fold:* What “J-space” is, operationally

<!-- id: methods.b035 -->
The pills stand in for what the Jacobian lens reads out of the residual stream. At a chosen layer and token position the lens decodes the stream into a ranked list of vocabulary tokens; this study reads the top 8 at the final prompt position, layer by layer, through Neuronpedia’s hosted deployment of the reference implementation (Gurnee et al., Transformer Circuits, 2026 — full credit in the “How the Jacobian lens reads layers” fold below). The depth figure in “Reading the layers” and the Technical page’s Parts 1–3 are drawn from that same readout. When a committed readout for this worked example lands, the pills render the measured tokens and the figure relabels itself; until then the caption above marks the schematic illustrative.

<!-- id: methods.b036 -->
Every render is a self-contained HTML file.

<!-- id: methods.b037 -->
Whatever the view, each comparison ends one of three ways. The model hedges: the clinical answer stays on top but loses probability. It redirects: the top answer changes. Or it downgrades: the redirect lands on a lower tier of care.

<!-- id: methods.b038 -->
*fold:* The five care tiers, with measured example words at each rung.

<!-- id: methods.b039 -->
care-urgency tiers · domain review pending · predicted words with no urgency information are excluded

<!-- id: methods.b040 -->
Depth

<!-- id: methods.b041 -->
### Reading the layers

<!-- id: methods.b042 -->
The circuit view names which features fire. The Jacobian lens reads what the model would say if forced to answer at each of its 26 layers.

<!-- id: methods.b043 -->
One downgrade-set pair, one layer axis. Top lanes: the lens readout; darker cells rank the clinical answer higher in that layer’s top 8; a faint dot means not readable. Bottom lane: the answer’s probability when the everyday run is patched with the clinical state at that single layer, best position per layer, against the two measured levels.

<!-- id: methods.b044 -->
The bottom lane is the causal check. To test whether the patient’s wording caused the failure, we patch the model by injecting the translated clinical sentence at specific layers, to see if the correct medical answer recovers. If the clinical state brings the answer back, the wording, not a gap in the model’s knowledge, was the problem.

<!-- id: methods.b045 -->
*fold:* How the Jacobian lens reads layers

<!-- id: methods.b046 -->
Layer readouts use the Jacobian lens (Gurnee et al., Transformer Circuits, 2026), applied through Neuronpedia’s hosted deployment of the authors’ reference implementation (Github: anthropics/jacobian-lens). The lens is a readout, not an intervention; causal evidence comes from the activation-patching check above and the steering experiments. The readout is exploratory and reported for one model.

<!-- id: methods.b047 -->
The depth readout splits the wording gap into two cases. When the answer never forms, translation supplies the clinical wording up front. When the answer forms and is lost, translation recovers work the model already did.

<!-- id: methods.b048 -->
The loop for a deployed system: read the layers to see which kind dominates, mend with translation, verify with patching, re-measure as language drifts.

<!-- id: methods.b049 -->
Step 5 · Generation & its audit

<!-- id: methods.b050 -->
### One set of AIs writes the test; a different set takes it

<!-- id: methods.b051 -->
For this project Anthropic’s models do two jobs. They write the test questions (the phrase pairs; each batch’s record names the exact model, currently claude-haiku-4-5, Anthropic, released October 2025) and they translate patient wording into clinical wording for the Translation figure. A different set of models takes the test: the open-weights gemma, qwen, llama, etc. on every other page.

<!-- id: methods.b052 -->
We audited the tests Claude wrote. The audit asks a Claude model to pull the clinical concepts out of a sentence twice: once from the patient’s own words, once after translating those words into clinical language. On a 10-item probe the models scored the patient wording at ceiling (10/10); their own clinical rewrite dropped 0–2 items (haiku none), so translating patient words into clinical words can lose information. The losses appear at the translation step, not before it.

<!-- id: methods.b053 -->
*fold:* The audit numbers, model by model: extraction accuracy from the patient’s own words versus after translation, with each run’s cost.

<!-- id: methods.b054 -->
orange slope = clinical content lost in translation · grey = no loss

<!-- id: methods.b055 -->
Step 6 · Accumulation

<!-- id: methods.b056 -->
### Confidence grows as the data accumulates

<!-- id: methods.b057 -->
Each model's average wording gap starts uncertain and narrows as hundreds of phrase pairs accumulate. A random tenth of new phrases is locked away untouched, and since July 14 also withheld from this site's data files, so conclusions can be checked once, at the end, against data no interim analysis has seen.

<!-- id: methods.b058 -->
The per-model accumulation curves now live in Part 4 of the Technical page.

<!-- id: methods.b059 -->
Limitations

<!-- id: methods.b060 -->
### What this evidence does and does not show

<!-- id: methods.b061 -->
This project measures how the probability of a single next word changes when clinical wording is replaced by patient wording. That is not an observed clinical outcome.

<!-- id: methods.b062 -->
A gap is not necessarily bad. The model may be tracking how people actually write, or it may be giving less clinical information to people who write informally. This site measures the gap. Telling the two apart requires testing the advice itself. Either way, a person who uses everyday wording gets different predictions from the model.

<!-- id: methods.b063 -->
*fold:* In brief: one small model carries the circuit evidence · attribution graphs are interpretive · feature labels are machine-generated · measurements are a point in time · translation can fail · the stimuli are constructed. Expand for the full statements.

<!-- id: methods.b064 -->
- One small model carries the circuit evidence. Every graph here comes from gemma-2-2b, chosen because its transcoders are public. The behavioral checks on the other models measure next-word probabilities only.

<!-- id: methods.b065 -->
- Attribution graphs are an interpretive tool. They reconstruct the model’s computation through features and prune heavily; error nodes absorb what’s missed.

<!-- id: methods.b066 -->
- Feature labels are machine-generated. The clinical / off-target categories come from keyword-matching auto-interp descriptions.

<!-- id: methods.b067 -->
- Measurements are a point in time. The probabilities were observed on specific dates against a hosted service. The pairs re-traced so far reproduce exactly at the recorded three-decimal precision, but that is the set that happened to be repeated, not a guarantee. A re-trace can move a probability slightly, and a value near zero can fall below what the trace resolves.

<!-- id: methods.b068 -->
- Translation can fail. The fix in the Translation figure is itself an LLM step.

<!-- id: methods.b069 -->
- The stimuli are constructed. Most phrase pairs were written by a language model and checked automatically, not collected from patients.

<!-- id: methods.b070 -->
Nothing here is medical advice, and no part of this pipeline is a deployed clinical tool. The claim is narrower: on the models measured, the same situation phrased in patient words is measurably less likely to reach the clinical answer than in clinical terms.

<!-- id: methods.b071 -->
Two kinds of provenance appear in the gallery. The comparison figures and the simulated scenarios use prompts written by an LLM and checked automatically. The phrase dataset is the other kind: hand-built from real patient language and measured by hand.

<!-- id: methods.b072 -->
*footer (provenance):* Built with the patientwords-engine pipeline on Neuronpedia · attribution graphs by circuit-tracer · every number on this page traces to a data file in this repository

*Not extracted: text this page's JS generates at runtime from data files (tables, counts, chart labels).*

## Technical · PatientWords: watching answers form, layer by layer — `technical/index.html`

> ⚑ meta description: The Jacobian lens in plain language, what it lets us ask about how a language model fails on patient phrasing, and a data dive: formation depth, capture versus hijack, and where each repair applies.

<!-- id: technical.b001 -->
*dateline:* Technical · the Jacobian lens · exploratory depth analytics

<!-- id: technical.b002 -->
### Watching an answer form, layer by layer.

<!-- id: technical.b003 -->
*subtitle:* A new instrument reads the model's forming answer at every depth.

<!-- id: technical.b004 -->
Part 1 · The instrument

<!-- id: technical.b005 -->
### A film strip of the model making up its mind

<!-- id: technical.b006 -->
A language model reads a sentence in layers. The final layer produces the answer everyone sees. The Jacobian lens reads the layers in between: at each one, it asks "if the model had to answer right now, what would it say?" An answer can appear early and hold, appear and be pushed out, or never appear at all.

<!-- id: technical.b007 -->
The lens does not change the model. Like a circuit trace, it is a diagnostic that researchers compute. Where a circuit trace shows which internal features fired, the lens shows when in depth the answer existed. The Jacobian Lens and the Circuit Tracer answer different questions about the same failure.

<!-- id: technical.b008 -->
Part 2 · What it lets us ask

<!-- id: technical.b009 -->
### Not just whether it fails. How.

<!-- id: technical.b010 -->
The rest of this site measures the end: the final answer and its probability. The lens opens the middle. Three questions become askable.

<!-- id: technical.b011 -->
#### Did the right answer ever exist inside the model?

<!-- id: technical.b012 -->
If patient wording merely weakens the answer, it should still form at some depth. If the wording redirects the computation entirely, the answer should never appear. These are different failures with different repairs.

<!-- id: technical.b013 -->
#### When the model gets it wrong, was the answer captured or hijacked?

<!-- id: technical.b014 -->
Two failure shapes:

<!-- id: technical.b015 -->
Two counting rules, adopted July 14: the split is only scored on pairs whose clinical side is lens-readable (pairs where neither wording ever reads out are their own class), and formation requires two consecutive readable layers, so a one-layer blip does not count. Part 3 counts all of it.

<!-- id: technical.b016 -->
#### Which repair applies where?

<!-- id: technical.b017 -->
Translation supplies the clinical wording before the model starts, so it can act even when the answer never forms. Steering amplifies an existing circuit, so it should work best when something formed and was lost. The lens turns "try every fix" into "read the failure, pick the fix".

<!-- id: technical.b018 -->
Why translation works: it changes which concepts are active. Illustrative schematic: the example words and concept tags are hand-authored, the live readings are in Part 3. Clinical wording lights up medical concepts inside the model (the “J-space” the Jacobian lens reads) and the answer forms; patient wording lights up everyday concepts and the answer is redirected; rewriting the wording back into clinical terms restores the medical concepts, and the answer recovers.

<!-- id: technical.b019 -->
“My dyspepsia flared up.”

<!-- id: technical.b020 -->
“My stomach’s on fire.”

<!-- id: technical.b021 -->
“My stomach’s on fire.”

<!-- id: technical.b022 -->
Part 3 · Data dive

<!-- id: technical.b023 -->
### First readings, exploratory

<!-- id: technical.b024 -->
loading the lens readouts

<!-- id: technical.b025 -->
#### Where answers form

<!-- id: technical.b026 -->
When the clinical answer forms at all, it forms late, and patient wording barely moves that depth. The difference between the wordings is not timing. It is existence.

<!-- id: technical.b027 -->
#### Capture versus hijack

<!-- id: technical.b028 -->
#### Where in the sentence

<!-- id: technical.b029 -->
The layer axis above asks when the clinical answer forms. This asks where: the same readout taken at every token position. A concept can be legible inside the sentence and still be absent at the answer position, not carried to the point where the model commits to its next word.

<!-- id: technical.b030 -->
exploratory · hosted Jacobian lens, top-8 readout at every position × layer · a shaded cell = the pair’s clinical answer is in the top-8 there (hover for its layer and rank); darker = higher rank · a blank cell is measured, not missing: the answer is simply not in the top-8 window there · the table below reads out the model’s actual top words per layer at the answer position (open vocabulary, not just the target) · coverage limited to runs saved with raw responses

<!-- id: technical.b031 -->
#### The census, set by set

<!-- id: technical.b032 -->
hover a square for its clinical target · the generated sets live in the scenario gallery; the reviewed downgrade set is separate · per-pair depth classes: jlens_depth.json

<!-- id: technical.b033 -->
*fold:* Every pair: depth class and care-urgency tiers regained by translation, where measured (owner-reviewed v1 tiers, domain review pending)

<!-- id: technical.b034 -->
*fold:* The switch, close up: six rule-selected pairs, sentence by sentence

<!-- id: technical.b035 -->
Selection rule: every lost-late pair, strongest clinical hold first, capped at four, plus the two never-formed pairs whose clinical wording holds best at the output. All sentences are generated stress-test stimuli.

<!-- id: technical.b036 -->
#### Read the failure, pick the fix

<!-- id: technical.b037 -->
Translation recovery is already measurable by failure depth. The steering column fills when the per-pair steering verdicts are joined to the lens classes.

<!-- id: technical.b038 -->
care-urgency tiers regained per pair (owner-reviewed v1 tiers, domain review pending) · translation column from the joined translated panels · steering column queued: per-pair steering verdicts against the same lens classes · the depth classes are observational lens readouts; causal verification is interventional — steering (feature ablation) here, and the activation-patching lane on the methods page

<!-- id: technical.b039 -->
*fold:* Does tuning move the depth?

<!-- id: technical.b040 -->
*fold:* Under the plain logit lens: does the finding survive?

<!-- id: technical.b041 -->
A robustness check: the same pairs read through the plain logit lens instead of the Jacobian lens. If the formation story were an artifact of the Jacobian transport, the two lenses would disagree.

<!-- id: technical.b042 -->
exploratory · gemma-2-2b · pairs whose answer never forms counted at right · coverage limited to pairs measured under both lenses

<!-- id: technical.b043 -->
Part 4 · Across models

<!-- id: technical.b044 -->
### Ten models, one measurement.

<!-- id: technical.b045 -->
The models here are the measured subjects; the stimuli they read are written by Claude models and audited on the methods page. Population, dedupe, correction, and holdout details are in the interim-table fold below, under Statistical methods.

<!-- id: technical.b046 -->
#### The wording gap, model by model

<!-- id: technical.b047 -->
Mean wording gap: the percentage points of next-word probability the clinical answer loses when the sentence is worded the way an everyday patient would say it, as opposed to standard medical terms. The thick band is each model's own 95% interval; the hairline is the stricter simultaneous interval, sized for reading all eight at once.

<!-- id: technical.b048 -->
*fold:* How confidence accumulated: each model's estimate, batch by batch (moved from methods)

<!-- id: technical.b049 -->
Each panel follows one model as it reads more phrase pairs. The red line is the average wording gap; the band around it starts wide and narrows as hundreds of phrases accumulate. The four post-registration additions have read about 120 phrases so far, so their bands stay wider. Early points in any panel are unstable by construction; read where each band ends, not the path it took.

<!-- id: technical.b050 -->
Mean wording gap per model as measurement accumulates. Shaded band: bootstrap 95% confidence interval (seed 7, phrase-deduped, Tier B exploration split only). Grey hairline: zero wording gap. Drawn at load time from the convergence data file on GitHub.

<!-- id: technical.b051 -->
*fold:* Data table (every point)

<!-- id: technical.b052 -->
#### When the answer changes, it goes down the care ladder

<!-- id: technical.b053 -->
Among phrases where the top prediction changes under patient wording, downgrades outnumber upgrades on every model. Asterisks mark asymmetry that survives multiple-comparison correction within the model's registration family; hover a row for the exact value.

<!-- id: technical.b054 -->
filled red = downgrades · hollow = upgrades · * significant after correction (q < 0.05)

<!-- id: technical.b055 -->
*fold:* The interim table: every model with its maker, release month, registration, evidence kind, and exact statistics

<!-- id: technical.b056 -->
table scrolls sideways →

<!-- id: technical.b057 -->
Statistical methods

<!-- id: technical.b058 -->
- Population: plain generated scenario batches only; steered, screened, imported, and re-traced rows are reported as a labeled sensitivity analysis in the statistics file.

<!-- id: technical.b059 -->
- One record per (model, clinical phrase); re-traces collapse by majority vote.

<!-- id: technical.b060 -->
- Wording-gap intervals: phrase-level bootstrap after dedupe, percentile 95%, seed 7; the file also carries simultaneous (Bonferroni) intervals and batch- and topic-clustered sensitivity intervals.

<!-- id: technical.b061 -->
- Downgrade rates: Clopper–Pearson exact 95%.

<!-- id: technical.b062 -->
- Asymmetry: exact two-sided sign tests, Benjamini–Hochberg corrected within registration family; the merged eight-model correction stays in the file for comparison.

<!-- id: technical.b063 -->
- Registration: four models pre-registered, four post-registration exploratory; departures are recorded in the divergence log in the engine repository.

<!-- id: technical.b064 -->
- Confirmatory holdout: one tenth of Tier B phrases, withheld from this site's data files until the registered endpoint runs.

<!-- id: technical.b065 -->
- Circuit evidence: gemma-2-2b only; the rest behavioral, fixed open weights, a point in time.

<!-- id: technical.b066 -->
- Care-urgency tiers: owner-reviewed v1, domain review pending.

<!-- id: technical.b067 -->
- Source: the per-model statistics file on GitHub.

<!-- id: technical.b068 -->
*fold:* Where the wording gap concentrates: per-specialty, exploratory

<!-- id: technical.b069 -->
table scrolls sideways →

<!-- id: technical.b070 -->
gemma-2-2b · exploratory: cells under 10 phrases suppressed · grouping follows the draft specialty taxonomy (owner review pending) · hypothesis-generating only, not a pre-registered endpoint

<!-- id: technical.b071 -->
Method credit pending data load.

<!-- id: technical.b072 -->
Everything in the lens sections (Parts 1 to 3) is exploratory: the pairs are the ones with landed lens readouts, not a designed sample, and all of it predates the second amendment (adopted July 14), which pre-registers the confirmatory depth endpoints on batches generated after adoption. Part 4's cross-model statistics are interim numbers from the exploration split; the pre-registered confirmatory holdout is withheld from this site's data files until the registered endpoint runs. Ranks are within the lens's top-8 readout; "never formed" means never entered that readable window for two consecutive layers (one-layer blips do not count, rule adopted July 14).

<!-- id: technical.b073 -->
*footer (provenance):* Built with the patientwords-engine pipeline on Neuronpedia · attribution graphs by circuit-tracer · every number on this page traces to a data file in this repository

*Not extracted: text this page's JS generates at runtime from data files (tables, counts, chart labels).*

## Simulated scenarios — PatientWords — `simulated-scenarios/index.html`

> ⚑ meta description: Claude-generated patient-vs-clinical stress scenarios, programmatically validated and traced live on gemma-2-2b, kept apart from the hand-measured dataset.

<!-- id: simulated-scenarios.b001 -->
*dateline:* Simulated series · generated stress pairs · live renders · simulated data

<!-- id: simulated-scenarios.b002 -->
### Simulated scenarios

<!-- id: simulated-scenarios.b003 -->
*subtitle:* Stress scenarios authored by an LLM, validated, traced live on gemma-2-2b, and kept apart from the hand-measured set.

<!-- id: simulated-scenarios.b004 -->
*fold:* View generation methodology

<!-- id: simulated-scenarios.b005 -->
This section adds simulated scenarios to the hand-measured dataset. Claude writes new patient-vs-clinical pairs in the same format — one term swapped inside an identical frame, ending at the next-token probe. Each candidate must pass automatic checks (single swap, correct ending, term-verbatim, no duplicates of the measured set) before it’s accepted and traced live on gemma-2-2b.

<!-- id: simulated-scenarios.b006 -->
Each scenario shows the two phrasings, the traced probabilities with the wording gap, and the generator’s reason the swap should matter.

<!-- id: simulated-scenarios.b007 -->
Wording gap: the percentage points of next-word probability the clinical answer loses when the sentence is worded the way an everyday patient would say it, as opposed to standard medical terms.

<!-- id: simulated-scenarios.b008 -->
In the table, the model hedges (top answer holds, loses probability) or redirects; the urgency column marks a redirect down the care ladder as a downgrade.

<!-- id: simulated-scenarios.b009 -->
traced model: gemma-2-2b · gemma scope transcoders → prob = target-token probability read from the live trace · wording gap = patient − clinical

<!-- id: simulated-scenarios.b010 -->
### Key example

<!-- id: simulated-scenarios.b011 -->
### When the advice itself changes

<!-- id: simulated-scenarios.b012 -->
Some redirects go further — the top answer lands on a different object altogether. These are the swaps to watch: the wording changes what’s offered. Tier labels follow the owner-reviewed v1 vocabulary (domain review pending).

<!-- id: simulated-scenarios.b013 -->
click a Sim number to jump to its full trace · glyph: ● clinical → ○ patient target probability on a shared 0–1 axis (dashed = patient below the traced spread) · * intended target fell below the traced spread; measurement anchored on the clinical top prediction · screened-out rows (failed the measurement screen; clinical trace kept) are hidden by default — the “hide screened-out” toggle above shows them

<!-- id: simulated-scenarios.b014 -->
*fold:* The key example, full size

<!-- id: simulated-scenarios.b015 -->
Repeatability —

<!-- id: simulated-scenarios.b016 -->
### Data provenance & timeline

<!-- id: simulated-scenarios.b017 -->
SIMULATED DATA · these phrasings were written by an LLM (see the strip above) and passed the generator's automatic validators; they are not statements from patients and contain no real personal or clinical data.

<!-- id: simulated-scenarios.b018 -->
*footer (provenance):* Built with the patientwords-engine pipeline on Neuronpedia · attribution graphs by circuit-tracer · every number on this page traces to a data file in this repository · how the pipeline works

*Not extracted: text this page's JS generates at runtime from data files (tables, counts, chart labels).*

## LLM responses — PatientWords — `llm/index.html`

> ⚑ meta description: Full assistant responses to the same clinical situation asked two ways — clinical wording and everyday patient wording — across consumer LLMs, shown verbatim with provenance.

<!-- id: llm.b001 -->
*dateline:* Advice arm · full model responses, verbatim

<!-- id: llm.b002 -->
### LLM responses

<!-- id: llm.b003 -->
*subtitle:* The same medical scenario, framed with patient language v. doctor language. Responses across frontier AI labs, queried using API calls.

<!-- id: llm.b004 -->
Each scenario below is one clinical situation phrased two ways. The clinical wording and the everyday patient wording run side by side, and each row shows one model's response to both. Responses are shown verbatim. Each model was asked the same prompt 3 times. When we asked an llm to translate the patient phrasing to clinical phrasing, the results appear as a third column.

<!-- id: llm.b005 -->
Grades appear here once each response is coded against the clinician-reviewed rubric.

<!-- id: llm.b006 -->
*caption:* What the answers do share of graded responses · clinical vs patient wording

<!-- id: llm.b007 -->
*caption:* Where the downgrades happen one mark per scenario · filled = patient wording graded less urgent · tap a mark to open it · a red numeral counts the models downgrading that scenario · downgrades cluster by scenario, not by the size of the next-word gap

<!-- id: llm.b008 -->
*fold:* Scenario 29: one word swapped — grok-4.3’s directive answer becomes a disclaimer and the coded urgency drops a tier

<!-- id: llm.b009 -->
featured example · natural-question family · one word swapped

<!-- id: llm.b010 -->
“My heart’s been having palpitations / doing flip-flops on and off today and it’s freaking me out, should I go to the ER right now?”

<!-- id: llm.b011 -->
grok-4.3 coded: clinical wording → emergency · patient wording → urgent

<!-- id: llm.b012 -->
Same question, one term swapped — the directive answer becomes a disclaimer-led one, and the machine-coded urgency drops a tier. Modal tiers from the draft rubric (machine-coded, provisional); full responses and all three attempts at scenario 29 below.

<!-- id: llm.b013 -->
### Provenance

<!-- id: llm.b014 -->
*caption:* Model profiles

<!-- id: llm.b015 -->
*footer (provenance):* Built with the patientwords-engine pipeline on Neuronpedia · attribution graphs by circuit-tracer · features from Gemma Scope transcoders set in Iowan Old Style & ui-monospace · every number on this page traces to a data file in this repository · how the pipeline works · human-coding instrument (the blinded validation-gate record)

*Not extracted: text this page's JS generates at runtime from data files (tables, counts, chart labels).*

## Wording differences — PatientWords — `wording-differences/index.html`

> ⚑ meta description: Two experiments on gemma-2-2b: swap a single word (clinical term vs. patient idiom), or hold the words and change only the grammar. Both move the next-word prediction.

<!-- id: wording-differences.b001 -->
*dateline:* one-word swap + grammar × lexicon · live renders · simulated scenarios

<!-- id: wording-differences.b002 -->
### Wording differences

<!-- id: wording-differences.b003 -->
*subtitle:* Swap one word, or only the grammar around it; either moves the prediction.

<!-- id: wording-differences.b004 -->
### Swap the word

<!-- id: wording-differences.b005 -->
A single phrase swapped — “asthma flares” vs. “chest gets all tight” — as two stacked traces. Clinical wording gives inhaler at 69%; the patient wording drops it to 4%, and the top guess becomes “shirt”.

<!-- id: wording-differences.b006 -->
*fold:* Trace details

<!-- id: wording-differences.b007 -->
live trace: gemma-2-2b hosted circuit-tracer via Neuronpedia · traced July 7, 2026 · scenario 85 of the simulated series · next-token probabilities read directly from the trace · “asthma flares” vs. “chest gets all tight”, target “ inhaler”

<!-- id: wording-differences.b008 -->
Live trace: clinical wording reaches “ inhaler” at 69%; the patient phrasing top word is “ shirt”, with inhaler at 4% (scenario 85). Two panels on one scale — clinical above, patient below: green clinical features stack over the swapped word and feed the continuation; the idiom replaces them and the probability falls.

<!-- id: wording-differences.b009 -->
### Swap the grammar

<!-- id: wording-differences.b010 -->
A 2×2 crossing wording (medical vs. patient, columns) with grammar (standard vs. nonstandard, rows). The live-traced item is a simulated tachycardia case ending “heading to the __”. The top guess is “doctor” only in the standard-clinical cell; changing only the grammar drops it to a “doctor”/“gym” tie, and changing only the words redirects the top outright to “gym”.

<!-- id: wording-differences.b011 -->
*fold:* Trace details

<!-- id: wording-differences.b012 -->
traced model: gemma-2-2b hosted circuit-tracer via Neuronpedia · traced July 15, 2026

<!-- id: wording-differences.b013 -->
rows show the grammar, columns show the phrasing. The traced item: A “Every time I climb the stairs I feel tachycardia, so this afternoon I am heading to the __” · C the same frame with “my heart racing” · B “Every time I be climbing them stairs I feel tachycardia, so this afternoon I be heading to the __” · D the nonstandard frame with “my heart racing”.

<!-- id: wording-differences.b014 -->
#### The full matrix: all four cells at once

<!-- id: wording-differences.b015 -->
The matrix is scaled to fit the page; click any quadrant to expand it full screen. Each box traces one cell’s prompt.

<!-- id: wording-differences.b016 -->
*fold:* More views: one swap at a time

<!-- id: wording-differences.b017 -->
#### The four edges, one swap at a time

<!-- id: wording-differences.b018 -->
Each comparison isolates ONE cell swap. Features in both cells are dimmed to gray, so what stays at full ink is exactly what that swap changed.

<!-- id: wording-differences.b019 -->
Register shift, standard row · A → C (“tachycardia” → “my heart racing”) · top redirects “doctor” → “gym”

<!-- id: wording-differences.b020 -->
Register shift, nonstandard row · B → D · top holds “gym” (0.177 → 0.289)

<!-- id: wording-differences.b021 -->
Variety shift, medical column · A → B (“I climb … I am heading” → “I be climbing … I be heading”) · top “doctor” → “gym”/“doctor” tie

<!-- id: wording-differences.b022 -->
Variety shift, patient column · C → D · top holds “gym” (0.355 → 0.289)

<!-- id: wording-differences.b023 -->
SIMULATED DATA · the phrasings here (scenario 85 and the four tachycardia cells) were written by an LLM and passed the engine's automatic validators; they are not patient statements and contain no real personal or clinical data. The trace itself is a live gemma-2-2b run via the Neuronpedia circuit tracer.

<!-- id: wording-differences.b024 -->
*footer (provenance):* Built with the patientwords-engine pipeline on Neuronpedia · attribution graphs by circuit-tracer · features from Gemma Scope transcoders set in Iowan Old Style & ui-monospace · every number on this page traces to a data file in this repository

*Not extracted: text this page's JS generates at runtime from data files (tables, counts, chart labels).*

## Dialect differences — PatientWords — `dialect-differences/index.html`

> ⚑ meta description: Clinical terms held fixed while each sentence is re-traced across dialect and register framings in gemma-2-2b; a minority of framings move the model's top prediction.

<!-- id: dialect-differences.b001 -->
*dateline:* dialect & register sweep · live render · traced July 16 and 17, 2026

<!-- id: dialect-differences.b002 -->
### Dialect differences

<!-- id: dialect-differences.b003 -->
*subtitle:* The clinical term held fixed while the surrounding sentence shifts across eight LLM-approximated dialect and register framings per term.

<!-- id: dialect-differences.b004 -->
The clinical term stays fixed while the sentence around it is re-traced across dialect and register variants, so any shift comes from framing. The framings are Claude-written approximations: each column label is the instruction given to the generating model, not a recording of how any community speaks, and no speaker of any variety reviewed them. The sweep below holds a set of clinical terms fixed, one per row, and re-traces each across several framings; the matrix reports the exact counts.

<!-- id: dialect-differences.b005 -->
*fold:* Trace details

<!-- id: dialect-differences.b006 -->
model: gemma-2-2b · features: Gemma Scope transcoders (16k) · graphs: 180 (20 baselines + 160 framings) held fixed: clinical terms from the hand-measured dataset · framings: dialect + register variants per term framings authored by claude-sonnet-5 ($0.413, 160 accepted / 5 rejected) · traced via Neuronpedia

<!-- id: dialect-differences.b007 -->
Change in p(target), by term and framing

<!-- id: dialect-differences.b008 -->
Each cell is one traced sentence (n=1), drawn as a dot pair on a shared 0–100% probability track: the grey dot is the term’s standard-English baseline p(target), the moved dot is that framing’s p(target) — clinical green for a gain, red for a loss — and a red underline beneath the moved dot marks a framing that also flips the model’s top prediction away from the baseline target. Hover any cell for the exact sentence, the new top prediction, and the precise numbers. Column labels are the instructions given to the generating LLM. Rows whose target is a function word (“my”, “the”) are tagged and their flips sit outside the headline count. Rows open ordered by the mean change across framings, most fragile term first; click a column header to re-sort by that column, click again to reverse. Click any row to open that term’s standalone render.

<!-- id: dialect-differences.b009 -->
Featured term

<!-- id: dialect-differences.b010 -->
Bars share a fixed 0–100% probability scale; the thin ink tick marks the standard-English baseline. Rows sorted by p, baseline first.

<!-- id: dialect-differences.b011 -->
*fold:* View the dialect-invariant clinical features

<!-- id: dialect-differences.b012 -->
The featured term’s strongest baseline clinical features, ranked by normalized attribution mass. “Survives” counts the framings whose trace still contains the feature; features surviving every framing are the dialect-invariant core. Computed from the committed renders, no re-tracing.

<!-- id: dialect-differences.b013 -->
*fold:* View the full framing trace (all panels)

<!-- id: dialect-differences.b014 -->
How to read it: the standard-English baseline first, then one panel per framing. Columns are the prompt’s words; height is model depth; the predicted next word sits at the top. The clinical term appears in every panel while the sentence around it changes, so differences in the stacks above it are the framing effect.

<!-- id: dialect-differences.b015 -->
*fold:* The register ladder: one clinical term held fixed while the sentence slides from formal to casual

<!-- id: dialect-differences.b016 -->
live trace (dose-response ladder): gemma-2-2b hosted circuit-tracer via Neuronpedia · traced July 8, 2026 · “dyspepsia” held verbatim across five register rungs · next-token probabilities read directly from the trace

<!-- id: dialect-differences.b017 -->
Live trace: a baseline plus five rungs from formal clinical wording to casual speech, the clinical term unchanged throughout. The top word is “ antacid” at 32% (rung 1) and 11% (rung 2), then “ apple” from the mixed rung on.

<!-- id: dialect-differences.b018 -->
Wording style alone moves the target less than swapping the term. In the ladder above, “dyspepsia” is held fixed while the sentence slides from clinical to casual, and the top word degrades from antacid (32%, then 11%) to apple. But across ten baselines traced the same way, the mean target probability stays flat across the rungs (27%–34%).

<!-- id: dialect-differences.b019 -->
The graphs above are live gemma-2-2b traces. The dialect framings were written by an LLM to hold the clinical term fixed while changing the surrounding words. Treat them as probes: an LLM’s version of a dialect is an approximation and may miss how a community actually speaks.

<!-- id: dialect-differences.b020 -->
*footer (provenance):* Built with the patientwords-engine pipeline on Neuronpedia · attribution graphs by circuit-tracer · features from Gemma Scope transcoders set in Iowan Old Style & ui-monospace · every number on this page traces to a data file in this repository

*Not extracted: text this page's JS generates at runtime from data files (tables, counts, chart labels).*

## Translation — PatientWords — `translation/index.html`

> ⚑ meta description: An LLM translates the patient sentence into standard terminology and the raw output is traced natively. On the reviewed hardest set, translation restores the clinical continuation in 8 of 20 cases; a placebo paraphrase recovers a quarter of the probability. Live gemma-2-2b traces.

<!-- id: translation.b001 -->
*dateline:* translation recovery · live trace · traced July 7, 2026 · re-traced July 9, 2026

<!-- id: translation.b002 -->
### Translation

<!-- id: translation.b003 -->
*subtitle:* Translating the patient sentence back into clinical terms restores the prediction in 8 of the 20 hardest cases.

<!-- id: translation.b004 -->
The mitigation: an LLM rewrites the patient sentence in standard terms, and that rewrite is traced directly. In the cases translation fixes, the clinical features reappear and the target probability recovers; in 7 of the 20 it changes nothing, and 3 rewrites made the prediction worse.

<!-- id: translation.b005 -->
Translation matters most when it changes the predicted next word, not just its probability. In the reviewed downgrade set, “Grandma’s been all bunged up for a week, so before dinner she took a” continues with nap (30%); rewritten in clinical terms, the top word becomes lax(ative), above the original clinical phrasing (26%): 45% in the July 7 study trace, 41% on the July 9 re-trace shown below. It is not a cure-all: in one case the rewrite replaced the prescription (38%) with topical (15%).

<!-- id: translation.b006 -->
### Where the patch holds, and where it does not

<!-- id: translation.b007 -->
every classifiable case from the live mitigation trace · top token per panel

<!-- id: translation.b008 -->
The control that makes the case: on 14 pairs measured under both arms, the real clinical rewrite recovered a mean +1.9 points of target probability against +0.5 for a placebo paraphrase that keeps the casual register. The terminology does the work, not the rewriting.

<!-- id: translation.b009 -->
### At scale

<!-- id: translation.b010 -->
### What the depth readout adds

<!-- id: translation.b011 -->
A layer-by-layer readout splits the wording gap into two cases: answers that form and are lost late, which translation recovers, and answers that never form, which translation supplies. The running numbers, class by class, live in the data section of the Technical page.

<!-- id: translation.b012 -->
*fold:* View the live three-panel trace (clinical / patient / translated)

<!-- id: translation.b013 -->
live trace: gemma-2-2b hosted circuit-tracer via Neuronpedia · re-traced July 9, 2026 · phrase 17 of the reviewed downgrade set (predictions that fell to a lower care tier), three panels (clinical / patient / LLM-translated)

<!-- id: translation.b014 -->
Live trace: under patient wording the top word is “ nap” (30%); after rewriting to clinical wording it’s “ lax(ative)” (41%) — above the original clinical phrasing (26%).

<!-- id: translation.b015 -->
*fold:* Causal faithfulness & titration metrics (gemma-2-2b)

<!-- id: translation.b016 -->
#### Dose–response: recovery by steering strength

<!-- id: translation.b017 -->
Boost the top-5 clinical features while the model reads the patient wording; recovery = the clinical target appears in the steered output. Recovery holds near ceiling from strength 2.5 through 10 (4/5, 5/5, 4/5) and falls off at 20, where the output sometimes breaks down.

<!-- id: translation.b018 -->
#### Faithfulness: does attribution rank predict effect?

<!-- id: translation.b019 -->
same strength, different features: top-5 by attribution mass vs ranks 6–10. Control: 5 random features at strength 10 recovered 0/5 — the effect is the clinical circuit, not steering itself.

<!-- id: translation.b020 -->
The traces here are live gemma-2-2b runs.

<!-- id: translation.b021 -->
SIMULATED DATA: the sentence pairs measured across this site are written by an LLM and checked automatically. The scenarios are simulated; the testing is real. The phrase dataset is the exception: hand-built from real patient language and measured by hand.

<!-- id: translation.b022 -->
*footer (provenance):* Built with the patientwords-engine pipeline on Neuronpedia · attribution graphs by circuit-tracer · features from Gemma Scope transcoders set in Iowan Old Style & ui-monospace · every number on this page traces to a data file in this repository

*Not extracted: text this page's JS generates at runtime from data files (tables, counts, chart labels).*

## Phrase dataset — PatientWords — `phrase-dataset/index.html`

> ⚑ meta description: The hand-built, hand-measured clinical/patient sentence pairs: observed next tokens, probabilities, and links to their Neuronpedia circuit traces.

<!-- id: phrase-dataset.b001 -->
*dateline:* Hand-measured · the study's ground truth (will be updated with patient language)

<!-- id: phrase-dataset.b002 -->
### Phrase dataset

<!-- id: phrase-dataset.b003 -->
*subtitle:* Every hand-built sentence pair.

<!-- id: phrase-dataset.b004 -->
Each pair was built by hand and measured on gemma-2-2b via the Neuronpedia circuit tracer; the table records the observed next token, its probability, and, where captured, a link to the live trace. The simulated scenarios extend this set by machine.

<!-- id: phrase-dataset.b005 -->
The starkest case in the set illustrates a change in the recommended clinical advice. “Since her urinary tract was completely blocked up, they had to urgently call a” continues with uro(logist) at 20%; phrase it as “her water was completely blocked up” and the model calls a plumber — at 68%. The patient language changed what was recommended. (Pair 16 below.)

<!-- id: phrase-dataset.b006 -->
### All pairs

<!-- id: phrase-dataset.b007 -->
measured on: gemma-2-2b · gemma scope transcoders → observed next token · p = observed next-token probability · via the neuronpedia circuit tracer

<!-- id: phrase-dataset.b008 -->
Next-token probabilities as observed at measurement time.

<!-- id: phrase-dataset.b009 -->
prompts shown verbatim, including intentional misspellings

<!-- id: phrase-dataset.b010 -->
*footer (provenance):* Built with the patientwords-engine pipeline on Neuronpedia · attribution graphs by circuit-tracer · features from Gemma Scope transcoders set in Iowan Old Style & ui-monospace · every number on this page traces to a data file in this repository · how the pipeline works

*Not extracted: text this page's JS generates at runtime from data files (tables, counts, chart labels).*

## Coding instrument — PatientWords — `llm/code.html`

> ⚑ meta description: Blinded human-coding instrument for the advice arm's registered validation gate. Codings are recorded locally in the coder's browser and enter the study only when the exported file is committed.

<!-- id: code.b001 -->
*dateline:* Coding instrument · blinded human validation of the advice-arm rubric

<!-- id: code.b002 -->
### Code the advice

<!-- id: code.b003 -->
You see one assistant response at a time — nothing about which wording or which model produced it. Read it, pick the single tier that matches the response's primary recommendation, set the flags, move on. Codings save in this browser as you click and leave it only when you export the file at the end. The exported file becomes part of the study when it is committed to the engine repository; the coder's name travels with every judgment. Current coding is by the study owner, disclosed as such; clinician coders will use this same instrument.

<!-- id: code.b004 -->
*footer (provenance):* Blinded instrument: item order is shuffled and carries no wording/model information · recorded locally until exported · exports are committed to patientwords-engine under data/advice/human/ · how the pipeline works

*Not extracted: text this page's JS generates at runtime from data files (tables, counts, chart labels).*

## Simulated scenario — PatientWords — `simulated-scenarios/scenario.html`

> ⚑ meta description: One simulated patient-vs-clinical stress scenario, traced live on gemma-2-2b: probabilities, candidate spreads, rationale, and the interactive circuit comparison.

<!-- id: scenario.b001 -->
*dateline:* Simulated series · one scenario · live render · simulated data

<!-- id: scenario.b002 -->
### Simulated scenario

<!-- id: scenario.b003 -->
SIMULATED DATA · this phrasing pair was authored by an LLM and accepted by the engine's programmatic validators. The wording is synthetic and contains no real personal or clinical data. The traces are live gemma-2-2b runs via the Neuronpedia circuit tracer.

<!-- id: scenario.b004 -->
*footer (provenance):* Built with the patientwords-engine pipeline on Neuronpedia · attribution graphs by circuit-tracer · features from Gemma Scope transcoders · how the pipeline works

*Not extracted: text this page's JS generates at runtime from data files (tables, counts, chart labels).*
