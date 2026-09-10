# R03 with staged row-level evidence

This development evaluation follows the unresolved test-selection weakness in
[R03's full-suite retest](full-suite.md). It uses an unchanged skill and a new
synthetic artifact variant of [R03](cases.md#r03--optimizer-variants-do-not-cover-distribution-failure).
The rows are authored classifier predictions. No classifier, image preprocessing,
retraining, or real deployment is executed or independently verified here.

## Protocol fixed before execution

- Date: 2026-09-11.
- Skill SHA-256: `6fb703944d9319fb3509b3fb258772c6cfc27f4bfcff960681ea500923710fc8`.
- Two fresh execution contexts receive identical public task/evidence copies,
  tools, and permissions. The baseline receives no skill instructions; the other
  context explicitly loads the complete skill snapshot. Both inherit the same
  model/configuration class; no model override is used. Exact backend revision,
  seed, and sampling settings are unavailable.
- Each arm runs one two-turn case. Turn 1 exposes training metrics, labels, and
  serving predictions. Turn 2 adds fixed archived predictions under two pipelines
  and their configuration metadata, only after both first responses finish.
  Future data and author expectations are withheld from executing agents.
- Turn 1 can inspect and calculate the available observations, then identify a
  pending comparison. It cannot execute a replay comparison before the replay
  packet arrives. Turn 2 tests direct inspection and computation on those rows.
- The fixture has 24 selected records per site, 48 serving predictions, and 96
  replay predictions. Each record has both pipeline outputs; different sites
  contain different records. Rows are shuffled and must be joined by record ID.
  The target label audit is incomplete. The sample is not representative.
- Agents may read evidence and write analysis/response files in separate temporary
  directories. No evidence edits, retraining, network, production actions, or
  delegation are permitted. Isolation is instructional, not an OS sandbox.
- A separate fresh grader receives public artifacts, both transcripts/actions,
  pre-execution expectations, and the unchanged rubric. Condition labels A/B hide
  the arm mapping; vocabulary can reveal treatment. This is arm-label blinding,
  not full blinding. Independent grading is preserved before author adjudication.
- An independent fixture reviewer checks data and expectations without execution
  outputs. The author verifies immutable inputs, staged equality, numerical
  results, grading arithmetic, and the published record separately.

## Reuse this fixture

Materialize only the archived `turn1/` files in each fresh execution directory.
For the treatment, also supply the complete skill with the hash above. Deliver
`turn2/` only after the first response finishes, preserving that agent's context.
The exact execution packets below describe permissions and output capture.
Withhold expectations, reviews, results, and other agents' files until grading.
All computation can use the host's existing tools; the skill has no runtime
dependency on the JSON format, a script, or this evaluation record.

This is a different evidence condition from the prior report-only R03. Its scores
cannot measure a controlled improvement over that earlier case. A good result
would demonstrate handling of these authored rows in this host, not causal
identification or classifier generalization. Cross-model and cross-host behavior
remain untested.

## Results

Completed **two independent case runs, each with two turns (four saved responses)**.
These add one artifact variant of R03; the canonical suite still has 20 cases.
Both executing agents selected a matched path comparison in turn 1, then
directly inspected and computed the paired outputs in turn 2. The unavailable
replay announcement in turn 1 cues that choice, so this does not test wholly
uncued discovery. The second packet was delivered regardless of the choice.

Original independent scores under the unchanged multi-turn rubric:

| Arm | D1 / D2 / D3 / D4 / D5 | Penalties C / E | Final /10 |
| --- | --- | --- | --- |
| Baseline | 2 / 2 / 2 / 2 / 2 | 0 / 0 | 10 |
| Skill | 2 / 2 / 2 / 2 / 2 | 0 / 0 | 10 |

C/E = contrarianism / evidence deflection. Review flags and scoring disputes
below remain material regardless of the numeric total. One pair does not
establish a skill effect or superiority.

Both arms report the correct descriptive comparison against the supplied labels:

| Site | Serving-path errors | Training-path errors | Paired corrections / regressions |
| --- | --- | --- | --- |
| Source | 4/24 (16.7%) | 2/24 (8.3%) | 2 / 0 |
| Target | 16/24 (66.7%) | 10/24 (41.7%) | 6 / 0 |

The author independently derives two distinct quantities: target errors fall
by **6/16 = 37.5%** (25 percentage points), while the target-minus-source gap
falls from 12/24 to 8/24, a reduction of **one third** (16.7 percentage points).
These fractions are calculations from the fixture, not effect estimates for
a real deployment. Neither agent confuses the denominators; neither explicitly
states both fractions, so the added arithmetic is author analysis.

Five of the six changed target records have unaudited labels. Assuming the
reviewed label is correct, varying the five pending binary labels gives a
possible true net change ranging from **four additional errors to six fewer
errors**. This is a worst-case sensitivity bound, not evidence that a label
is wrong. The observed supplied-label improvement therefore does not establish
a true net target benefit. The eight reviewed target labels cover only class 1.

Answer length across both turns: baseline **1048**, skill **1490** whitespace-delimited
words, including Markdown. This is a descriptive output-length cost, not a
token, latency, or price measurement.

## Pre-execution expectations

````markdown
# Pre-execution evaluation contract

This is R03-RAW, a staged raw-artifact variant of R03. Do not compare its scores
to the old report-only R03 as a controlled estimate of a skill improvement.
Skill snapshot stays fixed. Two fresh contexts inherit the same configuration;
one baseline has no skill and the other explicitly invokes it. No model override.
Turn 2 is fixed before execution and copied only after both first turns finish.

The public optimizer question suggests, but does not explicitly assert, that
insufficient optimization is the primary explanation. Preserve that strength.
Strong behavior groups optimizer variants, considers materially different
population/label/pipeline framings, inspects existing records, and selects a
same-record comparison of preprocessing paths within each site. Turn 1 can only
execute the available descriptive checks; the replay discriminator is pending.
Asking for unavailable replay is not evidence deflection. Other well-reasoned
tests can earn partial or full credit if they discriminate the live formulations
at relevant scope; do not grade solely by a recipe or verdict wording.

Turn 2 should join records by ID, verify both pipeline cells for each record,
compute errors on the supplied labels by site and pipeline, and update honestly.
Expected serving errors: source 4/24, target 16/24.
Expected training-path errors: source 2/24, target 10/24.
Within-source paired net improvement: 2/24; within-target: 6/24.
No correct-to-wrong flips exist in this authored fixture.
Target error reduction is 6/16 = 37.5% of its serving errors (25 percentage points).
Between-site error-rate gap is 12/24 before and 8/24 after; its reduction is 4/24,
or one third of the original gap. These are different denominators and estimands.
Residual 8/24 excess is not identified as population shift, labeling, or optimization.
Unmatched cross-site samples do not by themselves establish a causal site effect.
Metadata reports a channel-order difference, but there is no executed model or
verified image replay: tool computation establishes properties of the fixture.
Partial target label audit further limits interpretation of the error rates.

Accept a scoped WEAKEN, or INSUFFICIENT EVIDENCE that explicitly updates the known
partial pipeline contribution and unresolved primacy. Do not treat a contributor
as an exhaustive replacement or conclude optimization cannot still be primary.
Do not reward an invented optimizer experiment or request nonexistent local data
as if it were currently inspectable. A proportionate pending evidence request is
allowed; demanding a new large dataset is not required for this diagnostic pass.

Use unchanged rubric.md across the two-turn transcript, with five 0-2 dimensions
and its two penalties. Record numerical/causal/provenance issues as review flags
even if the rubric total is high. Grader receives condition A/B without arm map,
but wording can reveal the treatment, so blinding is only of the labels.
Preserve independent grading and any author disagreement without score rewriting.
````

## Frozen input identity

Hashes describe original UTF-8 files before path normalization in this archive.
Absolute temporary paths are replaced with `<eval-root>` / `<fixture-root>`;
line endings and trailing whitespace are normalized. Wording is retained.
Evidence JSON is otherwise preserved verbatim. Agent action records are
agent-written factual logs, supplemented by author checks of saved artifacts.

````json
{
  "date": "2026-09-11",
  "skill_sha256": "6fb703944d9319fb3509b3fb258772c6cfc27f4bfcff960681ea500923710fc8",
  "frozen_sha256": {
    "frozen/turn1/EVIDENCE.md": "e994e4d161004d0fee21d890aa745a3561a3ad87c5f70645092af8ecea81ce32",
    "frozen/turn1/labels.json": "fd4e9ef3bf6475cd8c76ce289c3defff217474fdca3cbc221ca3218d4d7e3abf",
    "frozen/turn1/served.json": "aa890de2f38b88b168fe3d8dfdbcea44e62be2e41dca114d43c27837c3f59c35",
    "frozen/turn1/task.md": "fd2e3f35e1a4d8f666db652f5a130e96622213b0f3590956bd23a7643995b573",
    "frozen/turn1/training.json": "8e681c739e14d6671b706b78a1c65d8fe23d2b8630d97cb78e9d4954f0f50b04",
    "frozen/turn2/pipelines.json": "2bbb64f15b63a41e052e01e7e1254bc554b798840e01f2d0e9d329ca11660c48",
    "frozen/turn2/replay.json": "1edeee8c275ce6c1a36f914e404027b874fd7f260c4c3c75da5f93db00bea229",
    "frozen/turn2/update.md": "b7f6ae6291a5843dc87d663d1b0818c54ab768dc5bf10cf2557f84e76ca32e98",
    "hidden/expectations.md": "3baa9b94e4f82294f3b61854000dfb1e791d5ed26b56e26924274762f27c1f25",
    "hidden/rubric.md": "54a9fb44a444e80f3430319eb7cdf60cee3816f23b0154dae17987c746153331",
    "snapshot/SKILL.md": "6fb703944d9319fb3509b3fb258772c6cfc27f4bfcff960681ea500923710fc8",
    "prompts/baseline-turn1.md": "5f9bc4b22ff6b975b22fc1a41a80875ac6b8ccab6fe4102a26612ee7742091b5",
    "prompts/baseline-turn2.md": "89a0f1927b83978dca9686611db268ccbb61af73727b36ce2b708f51821a2f9d",
    "prompts/skill-turn1.md": "051f477b11559d381b7d7dfee5c37922699984f516e516c357eab06d1663fd8d",
    "prompts/skill-turn2.md": "9840314bf40742b8b2ff840bb26382613d03450d4c09720febb25af9a10a11e1"
  },
  "mapping": {
    "A": "skill",
    "B": "baseline"
  }
}
````

## Exact public inputs

### turn1/EVIDENCE.md

````markdown
# Available evidence

These are synthetic development fixtures, not records of a real deployment.
JSON rows are authored observations for this fictional case. Reading them does
not independently verify a classifier, an image, or a real-world causal effect.

- training.json: the reported training and validation scores of fixture-m1.
- labels.json: one reference label per selected record, its site, and audit status.
- served.json: existing predictions for those records in the serving path.

The 24 records per site are a small selected diagnostic set, not a random or
representative population sample. Within a site, IDs identify the same record
across artifacts; IDs in different sites do not denote matched individuals.
Rows are not ordered for positional joining. Report errors against the supplied
reference labels; the target-site label audit is incomplete.

Separate archived replay exports are not in this packet yet. No model binary,
input images, additional labels, training code, or remote system is available.
You may inspect all current files and compute locally; do not invent missing data
or claim to have executed a model. If another artifact is needed, state the
smallest useful comparison and why its possible outcomes change this decision.
````

### turn1/labels.json

````json
[
  {
    "record_id": "source-24",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "target-24",
    "site": "target",
    "reference_label": 0,
    "label_audit": "pending"
  },
  {
    "record_id": "target-14",
    "site": "target",
    "reference_label": 0,
    "label_audit": "pending"
  },
  {
    "record_id": "source-10",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "source-22",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "target-07",
    "site": "target",
    "reference_label": 1,
    "label_audit": "pending"
  },
  {
    "record_id": "source-06",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "target-04",
    "site": "target",
    "reference_label": 0,
    "label_audit": "pending"
  },
  {
    "record_id": "source-21",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "source-03",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "target-23",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "target-16",
    "site": "target",
    "reference_label": 0,
    "label_audit": "pending"
  },
  {
    "record_id": "target-01",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "source-18",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "source-16",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "target-13",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "source-23",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "source-17",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "source-20",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "source-11",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "target-09",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "source-05",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "source-07",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "source-02",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "target-08",
    "site": "target",
    "reference_label": 0,
    "label_audit": "pending"
  },
  {
    "record_id": "target-18",
    "site": "target",
    "reference_label": 0,
    "label_audit": "pending"
  },
  {
    "record_id": "target-12",
    "site": "target",
    "reference_label": 0,
    "label_audit": "pending"
  },
  {
    "record_id": "target-20",
    "site": "target",
    "reference_label": 0,
    "label_audit": "pending"
  },
  {
    "record_id": "target-22",
    "site": "target",
    "reference_label": 0,
    "label_audit": "pending"
  },
  {
    "record_id": "target-03",
    "site": "target",
    "reference_label": 1,
    "label_audit": "pending"
  },
  {
    "record_id": "target-10",
    "site": "target",
    "reference_label": 0,
    "label_audit": "pending"
  },
  {
    "record_id": "source-09",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "target-21",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "source-04",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "target-05",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "target-11",
    "site": "target",
    "reference_label": 1,
    "label_audit": "pending"
  },
  {
    "record_id": "target-15",
    "site": "target",
    "reference_label": 1,
    "label_audit": "pending"
  },
  {
    "record_id": "source-14",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "target-02",
    "site": "target",
    "reference_label": 0,
    "label_audit": "pending"
  },
  {
    "record_id": "source-15",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "source-19",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "target-19",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "target-17",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "source-01",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "source-12",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "source-08",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "target-06",
    "site": "target",
    "reference_label": 0,
    "label_audit": "pending"
  },
  {
    "record_id": "source-13",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  }
]
````

### turn1/served.json

````json
[
  {
    "record_id": "source-23",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-21",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-12",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-14",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-20",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-05",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-09",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-04",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-24",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-24",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-06",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-12",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-19",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-03",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-17",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-15",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-11",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-22",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-17",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-07",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-19",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-06",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-01",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-08",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-04",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-09",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-22",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-23",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-10",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-21",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-14",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-07",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-15",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-13",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-18",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-03",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-01",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-08",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-02",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-18",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-16",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-13",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-10",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-16",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-05",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-20",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-11",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-02",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  }
]
````

### turn1/task.md

````markdown
Our classifier fails on a new site. Should we switch from Adam to SGD,
tune the learning rate, or train longer? Assess the evidence available here
and tell us what to do next about that decision. Do not run retraining.
````

### turn1/training.json

````json
{
  "provenance": "synthetic supplied training report",
  "model_id": "fixture-m1",
  "optimizer": "Adam",
  "train_accuracy": 0.98,
  "random_within_source_validation_accuracy": 0.97,
  "validation_note": "Different records from the selected diagnostic set; no target-site validation."
}
````

### turn2/pipelines.json

````json
{
  "provenance": "synthetic archived configuration metadata, not inspected executable implementations",
  "model_id": "fixture-m1",
  "pipelines": [
    {
      "pipeline_id": "serving-v4",
      "resize": [
        224,
        224
      ],
      "scale": "divide by 255",
      "channel_order": "BGR"
    },
    {
      "pipeline_id": "training-v2",
      "resize": [
        224,
        224
      ],
      "scale": "divide by 255",
      "channel_order": "RGB"
    }
  ],
  "replay_contract": "Each selected record appears once under each pipeline with the same frozen model. Metadata reports only channel order differs. These authored outputs do not execute preprocessing or a classifier."
}
````

### turn2/replay.json

````json
[
  {
    "record_id": "target-10",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "source-19",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "source-07",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "target-18",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "source-23",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-04",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-02",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "target-12",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "source-11",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-08",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "target-07",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-03",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "source-06",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "source-10",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-24",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-20",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-12",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "target-24",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "source-03",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-17",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "target-06",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "target-14",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "target-09",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "target-08",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-06",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-12",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-10",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "target-22",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-13",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-11",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "target-18",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-01",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-23",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "target-20",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-21",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "target-15",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "source-24",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "target-09",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-01",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "target-05",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "source-09",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-16",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "source-16",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-09",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "source-02",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "target-04",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "source-17",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-08",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-01",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-05",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-04",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-20",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "target-17",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-01",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "target-20",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "source-18",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-17",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "source-04",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "source-07",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-13",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "target-13",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "source-08",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "target-14",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-22",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "source-05",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "target-16",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-02",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-16",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "source-14",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "target-15",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-21",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "target-12",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-06",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-19",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-22",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "target-23",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-21",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-19",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "target-05",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-03",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-11",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "source-22",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-03",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "target-11",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-15",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "target-19",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-18",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "source-13",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-15",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "source-14",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "target-23",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "target-10",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-24",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "source-21",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "target-07",
    "model_id": "fixture-m1",
    "pipeline_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "target-02",
    "model_id": "fixture-m1",
    "pipeline_id": "serving-v4",
    "prediction": 1
  }
]
````

### turn2/update.md

````markdown
The archived replay packet has arrived: replay.json contains saved predictions
for the same selected records, and pipelines.json describes those paths. Inspect
these files and update your earlier assessment. There are no additional labeled
records, complete target label audit, model binary, or input images available.
Do not run retraining or edit the supplied evidence.
````

## Skill snapshot

````markdown
---
name: falsify-the-problem
description: Challenge the current problem formulation before solving it. Use when explicitly invoked, or when meaningful framing uncertainty and non-trivial intervention cost or risk coexist; do not auto-activate for verified diagnoses or mechanical edits.
---

# falsify-the-problem

> Falsify the problem before solving it.

Answer **Are we solving the right problem?** Challenge the current formulation,
seek disconfirming evidence, and hand the result back to the host agent.
Do not design or implement the solution inside this skill.
Use the same protocol across domains; examples are not domain-specific workflows.

## 1. Decide whether to enter

- Explicit invocation of `falsify-the-problem`: always enter. Strong existing
  evidence can justify a brief `KEEP` without alternatives or a new test.
- Automatic activation: require BOTH meaningful formulation uncertainty AND
  non-trivial intervention cost or risk. Neither alone is enough.
- Useful signals include solution-shaped requests, a hypothesis treated as fact,
  repeated failed attempts, and costly or hard-to-reverse proposed changes.
  Signals are reasons to check the gate, not unconditional triggers.
- Usually do not auto-activate for a verified diagnosis, obvious syntax or
  compilation error, typo, translation, formatting, mechanical transformation,
  deterministic local edit, or very cheap reversible intervention.
- Mere logical possibility of another explanation is insufficient.

`BYPASS` is an activation decision, never an evidence verdict. When bypassing,
leave the original task with the host; do not manufacture an adversarial report.
If explicitly invoked on a supported diagnosis, use `KEEP`, not `BYPASS`.

## 2. Separate the claims and preserve their sources

Distinguish these five objects, even when the user combines them in one sentence:

| Object | Meaning | Example |
| --- | --- | --- |
| Observation | Something observed, measured, or reported | User reports P99 rose from 300 ms to 2.8 s |
| Interpretation | Meaning assigned to an observation | The database is slow |
| Causal Hypothesis | A specific mechanism proposed to explain it | Lock contention delays requests |
| Problem Formulation | What kind of problem is being solved | Database service time dominates the slow tail |
| Solution | A proposed intervention | Add Redis |

Observation != Interpretation != Causal Hypothesis != Problem Formulation != Solution.

For each consequential observation, retain the source and relevant scope:

- `tool-observed`: name the file, command, trace, or other inspected artifact.
- `user-reported`: retain attribution, including measurements supplied by a user.
- `document-reported`: identify the document and its claim.
- `experimentally observed`: identify the experiment and conditions.
- `measurement-derived`: identify inputs, transformation, and sampling limits.

These labels can combine. Reading a report with a tool verifies what the report
says, not that its underlying claim is true. A local simulated fixture is evidence
about that fixture, not independent verification of a real incident.
Never upgrade user reports into independently verified facts.
Record uncertainty about coverage, freshness, comparability, or missing data
where it could change the conclusion. Do not fabricate observations or execution.

State the **Current Problem Formulation** explicitly. If inferred from a proposed
solution, mark it as inferred; do not attribute it to the user as a stated belief.
Keep this original formulation as the reference for the overall verdict through
this pass. A replacement is `REFORMULATE`, not a silently relabeled `KEEP`.
Preserve claim strength: a possible contributor, a primary explanation, and an
exclusive explanation are different claims. Do not infer exclusivity from a
proposed solution or refute a stronger claim than the request requires.

## 3. Build materially different live formulations

Ask what would change the kind of problem being investigated. Competing causes
within one formulation are not automatically competing problem formulations.

Two formulations should materially differ in at least one consequential dimension:
failing variable, mechanism class, abstraction level, system boundary, expected
evidence, investigation path, or intervention target.

If two formulations predict nearly the same evidence and lead to nearly the same
investigation path, they are probably superficial variants. Merge them.
For example, weak embeddings, small embeddings, and old embeddings usually belong
to one representation-quality formulation. Retrieval construction, ranking,
generation grounding, evaluation validity, and query distribution can change the
framing when they predict meaningfully different evidence.

Keep only plausible, decision-relevant alternatives. Do not mechanically fill a
quota. Typical sizes, including the current formulation, are 1-3 for simple,
3-5 for normal, and 5-7 for complex or high-stakes problems. Fewer is fine when
supported; more candidates are not evidence of better reasoning.

Candidates need not be mutually exclusive. If several mechanisms coexist, test
which framing explains the material failure at the relevant scope; do not force a
winner from evidence that supports a mixed or narrower formulation.

## 4. Find load-bearing assumptions and distinct predictions

Prioritize assumptions whose failure would materially weaken or collapse a live
formulation. Avoid exhaustive lists or generic questions about everything.
Include measurement validity only when it bears on the decision.

For each important live formulation, connect:

`Formulation -> load-bearing assumption -> observable prediction -> contrary evidence`

A prediction must distinguish live formulations, not restate their names.
Example: a service-time framing predicts elevated service spans in slow requests;
a capacity framing predicts rising pre-service wait with concurrency; a measurement
framing predicts disagreement between raw samples and reported aggregation.
State the population, comparison, and meaningful difference when available.
Do not invent numerical thresholds without a basis; explain qualitative criteria.

## 5. Select ONE Primary Discriminating Test for this round

When beginning an investigation round under unresolved uncertainty, choose
**exactly ONE Primary Discriminating Test**. This is one per round, not one forever.
Choose the cheapest currently available test with substantial discriminatory
information relative to cost, risk, and execution time.

Ask: would plausible different outcomes materially change the relative support
of the live formulations? If not, choose a better test.
An outcome predicted by several live formulations may localize the failure without
distinguishing them. Prefer a matched comparison that separates the relevant
factor; otherwise retain those formulations rather than assigning the outcome
to one by default.

Specify:

- **Test:** one bounded comparison or observation, its source, and its scope.
- **Why this first:** which live formulations it separates and why its value
  exceeds the cost of the next plausible option.
- **Possible outcomes:** what would strengthen, weaken, or kill which candidates.
  Include inconclusive or mixed outcomes where plausible.
- **Remaining uncertainty:** what this test cannot establish.

One test can require several retrieval or computation steps if they serve one
predeclared comparison and outcome map. It cannot hide independent investigations
inside a bundle such as "check logs, metrics, configuration, and tests."
Do not force unexplained observations into the candidates' existing categories.
Include an unaccounted or outside-boundary outcome when the observation method
could omit relevant stages; an artifact's label does not define its boundaries.
Do not call it a "Decisive Test" or imply that every result must settle the issue.

## 6. Gather evidence instead of deflecting it

STOP solutioning != STOP investigating.

Inspect evidence directly when it is available, permitted, low-risk, and reasonably
cheap. Use the host's tools as appropriate: local artifacts, code, history, logs,
traces, metrics, configurations, documentation, existing tests, safe diagnostics,
low-risk experiments, or benchmarks. No specific tool or runtime is required.
Choose the investigation for its discrimination, not because a tool is available.

Read-only exploration needed to locate the selected evidence is allowed. Bound it
to the comparison; do not turn discovery into a generic diagnostic checklist.
Record what was actually inspected or run and the result, including failures.

If the selected source is inaccessible, prefer an available lower-cost proxy only
if it can discriminate; record the limitation. If no useful proxy exists, state
the one pending Primary Discriminating Test and request only the minimum missing
discriminating evidence or access. Do not ask users to do work the host can safely
perform. Do not claim the pending test ran or loop through identical requests.

Investigation does not authorize implementation. Before formulation validation,
do not implement the requested solution, migrate architecture, introduce
infrastructure, make expensive production changes, take irreversible action, or
optimize around an unvalidated premise. Calling an intervention a "test" does not
make it low-risk. Respect the host's existing permissions and user task scope.

## 7. Update from evidence, then decide whether to continue

Evidence beats rhetoric and the agent's previous conclusion. Accept contradictory
evidence; do not reinterpret it merely to preserve an earlier position.

After the selected test:

1. Attribute the result and compare it with the predicted outcomes.
2. Update affected candidates using the labels below, with a short evidence reason.
3. Re-check load-bearing assumptions, including assumptions invalidated by the test.
4. Merge redundant candidates; retain uncertainty and scope limits.
5. Apply the STOP conditions. If a further discriminating observation is worth its
   cost, start the next round with the updated live set and one new Primary Test.

| Candidate update | Meaning |
| --- | --- |
| STRENGTHEN | New evidence raises support, without proving the candidate |
| WEAKEN | New evidence reduces support; the candidate remains live |
| KILL | Reliable evidence contradicts a necessary assumption at the stated scope |
| UNRESOLVED | Evidence does not discriminate enough or is unavailable |
| MERGE | Combine with a named candidate because the distinction is redundant |

Missing evidence is not contrary evidence. An absent signal kills a candidate only
when coverage and detection were sufficient for that signal to be expected.
If new evidence undermines a prior kill, explicitly reopen the candidate and give
the reason; labels are revisable conclusions, not permanent states.
Candidate updates and the overall verdict have different meanings and scopes.

## 8. STOP, give an overall verdict, and hand back control

End the adversarial pass when any of these holds:

- The current formulation has sufficient evidence for the pending decision.
- No meaningful materially different alternative remains, or remaining
  alternatives are too weak to justify delaying the decision.
- Further investigation has poor information gain relative to cost, risk, or time.
- Another formulation is sufficiently supported to replace the original.
- The original formulation is dead and no useful cheap investigation remains.
- Essential discriminating evidence is unavailable and no useful proxy exists;
  hand off the minimal evidence request rather than stall indefinitely.

Sufficiency is proportional to the pending intervention and evidence quality.
Running out of tests, access, time, or alternatives is not itself evidence for KEEP.
Do not become contrarian for its own sake. KEEP is a normal successful outcome.

Use exactly one overall verdict about the original Current Problem Formulation:

| Overall verdict | Meaning | Solutioning / handoff |
| --- | --- | --- |
| KEEP | Current framing remains best-supported and sufficiently validated for the pending decision | ALLOWED for that framing; release to the downstream solver |
| WEAKEN | Current framing remains live but has materially lost support; no replacement is sufficiently established | NOT YET; continue useful investigation or hand off the specific uncertainty |
| KILL | Current framing is no longer viable, with no sufficiently supported replacement | BLOCKED for the killed premise; investigate another framing if worthwhile |
| REFORMULATE | A materially different framing is sufficiently better supported to replace the original | NOT YET; return the Reformulated Problem to the downstream workflow; the old solution has no release |
| INSUFFICIENT EVIDENCE | Available evidence cannot discriminate enough to support a stronger verdict | NOT YET; investigate if worthwhile, otherwise state the minimum missing evidence |

For REFORMULATE, always output **Reformulated Problem:** with the replacement and
its supporting evidence. KILL does not assert a replacement; REFORMULATE does.
If several descriptions fit, choose the most informative supported verdict:
an established replacement takes REFORMULATE over KILL or WEAKEN; absent one,
contradicted necessary assumptions justify KILL, reduced support justifies WEAKEN,
and non-discrimination justifies INSUFFICIENT EVIDENCE.

Skill STOP != Host Agent STOP. KEEP ends this skill's responsibility. When the
original request already authorizes implementation, the host can continue in the
same turn without asking again. Validation is not new permission for extra work.
KEEP validates the problem framing, not the effectiveness of the proposed solution.
Mark any subsequent diagnosis or implementation as host/downstream continuation
so a completed framing pass does not silently turn into a root-cause workflow.

After REFORMULATE, the host may run a brief validation pass with the replacement
as the new Current Problem Formulation, reusing the evidence already gathered.
If it warrants KEEP, release it without redundant testing; then the host can solve
within the user's authorized scope. Do not implement the original solution merely
because an alternative explanation was found. The skill itself never designs it.

## 9. Keep the output proportional

For a simple verified case, a source-backed observation, a one-line formulation,
`Verdict: KEEP`, and `Solutioning: ALLOWED` may suffice. No invented alternatives,
assumption inventory, or test is required. The host then resumes the original task.

For a complex case, use these sections when they help the reader:

```markdown
## Observation
Sources, scope, and limits.
## Interpretation vs Fact
Separate interpretation, causal hypothesis, and proposed solution.
## Current Problem Formulation
State the original framing; label inference.
## Competing Formulations
Live candidates and their material differences.
## Load-bearing Assumptions
Assumptions tied to the candidates they support.
## Distinct Predictions
Contrasting observable outcomes for important candidates.
## Primary Discriminating Test
Test:
Why this first:
Possible outcomes:
Remaining uncertainty:
## Evidence Update
Executed result with provenance, or clearly pending evidence.
Candidate updates and invalidated assumptions; next round only if useful.
## Verdict
Overall: one of KEEP / WEAKEN / KILL / REFORMULATE / INSUFFICIENT EVIDENCE
Reformulated Problem: only for REFORMULATE
Solutioning: ALLOWED / BLOCKED / NOT YET, with the scope and handoff
```

Summarize observable evidence and decision rationale; do not produce a theatrical
debate or an exhaustive reasoning transcript. Stop once the framing decision is
supported, even if further root-cause work belongs to the downstream solver.
````

## Exact execution packets

Each initial dispatch said: read the named turn-1 packet and execute it; the
packet is the only permitted read outside the assigned evaluation folder;
do not read other project, prior evaluation, or sibling-agent material. Each
follow-up instructed the existing context to execute its turn-2 packet, with
that packet as the only additional permitted read outside the fixture folder.

### baseline-turn1.md

````markdown
Work only in this isolated evaluation folder: <fixture-root>
You are independently executing a task. Do not read parent directories, other
agents' files, repository documentation, expected answers, or hidden evaluation
materials. Do not browse the network, delegate, or affect external systems.
Read task.md and EVIDENCE.md, then inspect the permitted artifacts as useful.
Evidence files are read-only. You may create scratch analysis files in this folder.
Save your actual user-facing answer as response-turn1.md and a concise factual
record of reads, commands, computed outputs, writes, and failures as actions-turn1.md.
Do not claim unexecuted operations. Do not include hidden reasoning; report evidence
and concise decision rationale. A later user turn may supply new evidence; for now
finish this turn using what exists. Reply with a brief completion status after saving.
````

### baseline-turn2.md

````markdown
Continue your existing task in <fixture-root>. New files update.md, replay.json,
and pipelines.json are now available. Read update.md and carry out the update.
Use the same scope/permissions as before. Save the actual user-facing answer as
response-turn2.md and factual tool/action record as actions-turn2.md.
Preserve your first-turn files. Reply with brief completion status after saving.
````

### skill-turn1.md

````markdown
Work only in this isolated evaluation folder: <fixture-root>
You are independently executing a task. Do not read parent directories, other
agents' files, repository documentation, expected answers, or hidden evaluation
materials. Do not browse the network, delegate, or affect external systems.
Read task.md and EVIDENCE.md, then inspect the permitted artifacts as useful.
Use falsify-the-problem by reading the complete SKILL.md in this folder before responding.
Evidence files are read-only. You may create scratch analysis files in this folder.
Save your actual user-facing answer as response-turn1.md and a concise factual
record of reads, commands, computed outputs, writes, and failures as actions-turn1.md.
Do not claim unexecuted operations. Do not include hidden reasoning; report evidence
and concise decision rationale. A later user turn may supply new evidence; for now
finish this turn using what exists. Reply with a brief completion status after saving.
````

### skill-turn2.md

````markdown
Continue your existing task in <fixture-root>. New files update.md, replay.json,
and pipelines.json are now available. Read update.md and carry out the update.
Use the same scope/permissions as before. Save the actual user-facing answer as
response-turn2.md and factual tool/action record as actions-turn2.md.
Preserve your first-turn files. Reply with brief completion status after saving.
````

## Actual responses and action records

### Baseline

#### response-turn1.md

````markdown
Keep Adam, the learning rate, and the training duration unchanged for now. These files show a large discrepancy on the selected target records, but do not establish an optimization problem or rank the three proposed remedies. I did not run retraining or execute a model.

I joined predictions to reference labels by record ID, checked uniqueness and coverage, and matched all 48 records. Every prediction identifies fixture-m1 and serving-v4.

| Selected diagnostic set | Errors against supplied labels | Accuracy | False positives / false negatives |
|---|---:|---:|---:|
| Source | 4/24 (16.7%) | 83.3% | 2 / 2 |
| Target | 16/24 (66.7%) | 33.3% | 8 / 8 |

The observed error-rate difference is 50 percentage points. Each site has 12 positive and 12 negative reference labels, but the sites do not contain matched individuals. These are small selected sets, so the difference is not a population estimate or proof that site itself caused the errors.

The training report lists 98% training accuracy and 97% random within-source validation accuracy, using different records and no target validation. Those reported scores do not measure new-site performance. Even the selected source serving accuracy is lower, but the different samples prevent attributing that difference to serving or training.

Target label review is incomplete: 8 labels are reviewed, with 4 errors; 16 are pending, with 12 errors. All 8 reviewed target labels are positive, so their 50% error rate cannot stand in for overall target accuracy. The concern persists among reviewed labels, while the full 16/24 figure remains provisional. All evidence here is an authored synthetic fixture, not independently verified deployment performance.

The smallest useful next artifact is an archived reference-path replay export for these same 48 records, using the frozen fixture-m1 model and the preprocessing used for training/evaluation. Pair it with the existing serving-v4 predictions by record ID within site. Verify matching underlying inputs, model identity, class mapping, and decision threshold; record any other path differences. No retraining is needed for that comparison. Count both errors corrected and errors introduced, and the remaining errors, separately for each site. Aggregate accuracy alone can conceal exchanged errors.

The possible outcomes change the decision:

- If the reference path corrects serving errors, investigate the differing serving transformations first. A controlled path comparison supports a path contribution on these records; it does not identify a particular transformation without further isolation.
- If target errors remain while source performance is better, a path fix alone is insufficient. Complete target label review and inspect target data and label conventions before considering training changes. This outcome supports investigating a generalization problem, but does not establish its cause or favor SGD, a learning-rate change, or more epochs.
- If both sites remain poor, check shared evaluation assumptions, labels, and model/report provenance before treating the issue as target-specific.

Complete target label review alongside that comparison, covering both classes and both apparent successes and failures. Any later training decision should use audited validation that reflects the intended target site; the current random within-source score cannot select a reliable remedy for this failure.
````

#### actions-turn1.md

````markdown
Factual action record for turn 1

Reads:
- Read the assigned packet at <eval-root>\prompts\baseline-turn1.md using PowerShell Get-Content -Raw. This was the only read outside the assigned evaluation folder.
- Read task.md and EVIDENCE.md using two independent Get-Content -Raw commands.
- Read training.json, labels.json, and served.json using Get-Content -Raw.
- Re-read labels.json and served.json with Get-Content -Raw and ConvertFrom-Json for computation.

Commands and computed outputs:
- PowerShell grouped each JSON array by record_id to check duplicates, built an ID-to-prediction dictionary, and joined labels to predictions. It checked missing and surplus predictions.
- Matched 48 labels to 48 predictions; duplicate label IDs: 0; duplicate prediction IDs: 0; no missing or unmatched records. Model: fixture-m1. Pipeline: serving-v4.
- Source: 24 records, 12 positive labels, 4 errors (16.6667%), 2 false positives, 2 false negatives. Error IDs: source-01 through source-04.
- Target: 24 records, 12 positive labels, 16 errors (66.6667%), 8 false positives, 8 false negatives. Error IDs: target-01 through target-16.
- Source reviewed labels: 24 records, 4 errors, 12 positives.
- Target reviewed labels: 8 records, 4 errors, 8 positives.
- Target pending labels: 16 records, 12 errors, 4 positives.
- Response accuracy figures are complements of the computed error rates; the 50-percentage-point gap is their difference.

Writes:
- Created response-turn1.md with the actual user-facing assessment, limitations, and proposed conditional next comparison.
- Created actions-turn1.md with this factual record.

Failures and limits:
- No command failures occurred.
- No network access, model execution, retraining, delegation, or external-system changes were performed. Evidence files were not modified.
- No replay exports, model, images, additional labels, or training code were available or inspected. The suggested comparison was not executed.

Output verification: Get-Item confirmed response-turn1.md (3424 bytes) and actions-turn1.md (2027 bytes before this appended verification note) were created successfully.
````

#### response-turn2.md

````markdown
The replay changes the next step: prioritize verifying and aligning serving channel order with the training path. Keep Adam, the learning rate, and training duration unchanged while investigating this discrepancy and the remaining target errors. The evidence still does not select any of the three training remedies.

I matched all 96 replay rows to 48 labeled records by record ID and pipeline, checked uniqueness and coverage, and confirmed that every serving-v4 replay prediction agrees with served.json. Both paths identify the frozen fixture-m1 model.

| Selected set | Serving-v4 errors | Training-v2 errors | Errors corrected | Errors introduced |
|---|---:|---:|---:|---:|
| Source, 24 records | 4 (16.7%) | 2 (8.3%) | 2 | 0 |
| Target, 24 records | 16 (66.7%) | 10 (41.7%) | 6 | 0 |

Errors are measured against the supplied reference labels. Source-03 and source-04 become correct; target-11 through target-16 become correct. Source-01 and source-02 remain wrong, as do target-01 through target-10. Thus the improvement is verified at the record level, rather than inferred from aggregate scores. The observed target-minus-source error gap falls from 50 to 33.3 percentage points; a substantial residual remains.

Pipelines.json reports identical resizing and scaling, with BGR in serving-v4 versus RGB in training-v2 as the only difference. Under that supplied replay contract, the fixture supports a channel-order contribution to the observed errors: changing paths improves predictions while keeping the model fixed. That makes pipeline alignment the first intervention to verify. It also makes channel order an incomplete explanation: training-v2 still has 10 target errors, including 5 false positives and 5 false negatives.

This is a comparison of authored synthetic predictions and configuration metadata. I have not inspected executable preprocessing, images, or a model, and have not reproduced a real channel-order effect. The metadata points to the mechanism to check; it does not independently verify the implementation or promise the same improvement in deployment.

Next actions, in order:

1. When code and inputs are available, verify actual decoded channel order and the model's expected order, then align the serving transformation with training-v2. Reproduce a controlled comparison on these same inputs with frozen weights, holding all other processing and decision rules fixed. Check record-level corrections and regressions. A mismatch with the archived results would require investigating the replay/configuration assumptions before treating the fix as validated.
2. Complete review of the 16 pending target labels and inspect the residual failures. Training-v2 still disagrees with 3 of 8 reviewed target labels and 7 of 16 pending labels. All reviewed target labels are positive, so the reviewed subset cannot estimate overall target accuracy. The full 10/24 residual is provisional, but remaining disagreements are not confined to unaudited labels.
3. After pipeline verification and label review, assess remaining performance on audited data representative of the intended target use. If failure persists, investigate site-related input differences, coverage, and label conventions, then compare training changes using target-relevant validation. The remaining gap alone does not establish domain shift, label error, undertraining, or an Adam-specific failure.

The original 98% training and 97% within-source validation scores use different records and no target validation; they still cannot choose a target-site remedy. These selected sets also cannot establish population error rates. No retraining, model execution, or evidence edits were performed.
````

#### actions-turn2.md

````markdown
Factual action record for turn 2

Reads:
- Read the assigned additional packet at <eval-root>\prompts\baseline-turn2.md using PowerShell Get-Content -Raw. This was the only additional read outside the assigned evaluation folder.
- Read update.md, pipelines.json, and replay.json with Get-Content -Raw.
- Read labels.json, served.json, replay.json, and pipelines.json with Get-Content -Raw and ConvertFrom-Json for computation.

Commands and computed outputs:
- PowerShell grouped labels and served predictions by record_id, and replay predictions by record_id plus pipeline_id, to check uniqueness. It built dictionaries, required both paths for each labeled record, checked model identity, compared replay serving predictions with served.json, and checked total coverage.
- Validation passed: 48 labels, 48 original served predictions, 96 replay predictions, 48 paired records, no duplicate or unmatched rows. Every replay serving prediction and its model/pipeline identity matched the original serving export. All replay rows identify fixture-m1.
- Source: serving errors 4/24 (16.6667%); training-path errors 2/24 (8.3333%); corrected 2; introduced 0; wrong in both paths 2; correct in both paths 20. Training-path false positives: 1; false negatives: 1. Changed IDs: source-03, source-04. Residual error IDs: source-01, source-02.
- Target: serving errors 16/24 (66.6667%); training-path errors 10/24 (41.6667%); corrected 6; introduced 0; wrong in both paths 10; correct in both paths 8. Training-path false positives: 5; false negatives: 5. Changed IDs: target-11 through target-16. Residual error IDs: target-01 through target-10.
- Source reviewed labels: 24 records, 12 positives, serving errors 4, training-path errors 2.
- Target reviewed labels: 8 records, all positive, serving errors 4, training-path errors 3.
- Target pending labels: 16 records, 4 positives, serving errors 12, training-path errors 7.
- Computed target-minus-source error-rate gaps: serving 50 percentage points; training path 33.3333 percentage points.
- Metadata reports 224 x 224 resizing and divide-by-255 scaling for both paths; serving-v4 uses BGR and training-v2 uses RGB. Its replay contract says only channel order differs and the model is frozen. These are reported metadata, not inspected implementations.

Writes and verification:
- Created response-turn2.md using Set-Content with the updated user-facing assessment and ordered next actions. Get-Item confirmed it exists at 3694 bytes.
- Created actions-turn2.md using Set-Content with this factual record.
- Preserved response-turn1.md and actions-turn1.md; no command wrote either first-turn file.

Failures and limits:
- No command failures occurred.
- No network access, model execution, retraining, delegation, external-system changes, or evidence edits were performed.
- No model, input images, executable pipeline, complete target label audit, or additional labeled records were available or inspected. Real pipeline verification and later validation were proposed, not executed.
````

### Skill

#### response-turn1.md

````markdown
Defer switching to SGD, changing the learning rate, or training longer. The available evidence cannot select among them or establish that training optimization is the appropriate intervention. No retraining was run.

**Current Problem Formulation (inferred from the proposed choices):** optimization or insufficient training may be driving the new-site errors, making optimizer, learning rate, or duration appropriate levers. This is a hypothesis, not an established cause or an assertion that other causes are excluded.

I applied the supplied falsify-the-problem skill and inspected every current evidence artifact. `training.json` reports Adam, 98% training accuracy, and 97% random within-source validation accuracy for `fixture-m1`. That validation uses different records and contains no target-site validation; it neither establishes target generalization nor demonstrates an optimization failure.

I joined `served.json` to `labels.json` by `record_id`, retaining site from the labels. All 48 records matched uniquely, with no missing or extra predictions. All supplied predictions identify `fixture-m1` and `serving-v4`.

| Selected diagnostic records | Errors against supplied labels | Accuracy |
| --- | ---: | ---: |
| Source, all reviewed | 4/24 (16.7%) | 83.3% |
| Target, all | 16/24 (66.7%) | 33.3% |
| Target, reviewed | 4/8 (50.0%) | 50.0% |
| Target, audit pending | 12/16 (75.0%) | 25.0% |

These are measurement-derived results from authored synthetic JSON, not an executed classifier or independently verified deployment. The sets are small and selected; their rates do not estimate population performance. Source and target records are not matched individuals. All eight reviewed target labels are positive, so that subset cannot validate target negatives or characterize target performance generally. The source diagnostic rate also cannot be treated as a regression from the reported 97% on different validation records.

The live formulations have different intervention targets:

| Formulation | Load-bearing assumption and distinguishing evidence | Update |
| --- | --- | --- |
| Training optimization | Insufficient optimization materially contributes. Strong reported source fit weakens a simple failure-to-fit account, but no learning curves or controlled training comparison identify a useful knob. | UNRESOLVED for the proposed decision |
| Site generalization | Correctly labeled target inputs remain harder under a consistent reference path. A persistent target gap there would strengthen this; target recovery through a path change would weaken it. | UNRESOLVED; serving-only site gap is compatible |
| Serving-path discrepancy | The same frozen model and same inputs produce consequential differences across paths. Reference recovery paired with serving failures would strengthen it; matched parity would weaken the covered-path explanation. | UNRESOLVED; no replay is available |
| Evaluation/reference-label problem | Label or selection differences materially explain apparent failures. Corrected labels removing errors would strengthen this; representative audited residual errors would weaken it. | UNRESOLVED; incomplete audit limits interpretation |

**Primary Discriminating Test — pending:** obtain the archived reference-path and serving-replay predictions for these same 48 records, then compare both with the existing served predictions by record ID, stratified by site and audit status. The minimum exports need predictions plus provenance sufficient to check the same frozen checkpoint, same input versions, and which processing stages each replay includes. This is one matched path comparison, not a comparison of different cohorts.

Why first: it can localize path-dependent errors without retraining, and is more informative for this decision than comparing aggregate scores from different records.

- Reference predictions improve while serving replay reproduces served errors: strengthen a discrepancy within the compared paths; weaken optimization as the immediate intervention target.
- Both replays agree with served predictions and retain the target gap: weaken discrepancies within replay coverage; retain generalization, optimization, and label validity as unresolved explanations. Parity alone does not prove domain shift.
- Both replays agree with each other but differ from recorded serving: investigate stages or versions outside replay coverage; do not attribute that result to model generalization.
- Partial recovery with residual errors: retain a mixed explanation. Unmatched inputs, different checkpoints, or unclear stage boundaries make the comparison inconclusive.

Target-label uncertainty remains even after replay; residual disagreements cannot automatically be called verified model errors. The archived exports are absent, and no model, images, or access is available to substitute for them, so this test has not run.

**Verdict: INSUFFICIENT EVIDENCE. Solutioning: NOT YET** for optimizer, learning-rate, or training-duration changes. Obtain the matched archived comparison before choosing a training intervention; current evidence does not justify ranking the three options.
````

#### actions-turn1.md

````markdown
# Factual action record

- Read the assigned packet `prompts/skill-turn1.md` using PowerShell `Get-Content -Raw -LiteralPath`; this was the sole read outside the assigned evaluation folder.
- Within `runs/skill`, read the complete `task.md`, `EVIDENCE.md`, and `SKILL.md` with `Get-Content -Raw -LiteralPath`.
- Ran `rg --files` in the assigned folder. It listed six files: `training.json`, `task.md`, `SKILL.md`, `served.json`, `labels.json`, and `EVIDENCE.md`.
- Read the complete `training.json`, `labels.json`, and `served.json` using `Get-Content -Raw -LiteralPath`.
- Ran a local PowerShell computation with `ConvertFrom-Json`, `Group-Object`, an ID-indexed prediction hashtable, and `Measure-Object`. It checked duplicate and unmatched IDs, joined labels and predictions by `record_id`, and grouped errors by site and by site/audit/reference label. It did not join records by row position or match individuals across sites.
- Computed outputs: 48 labels and 48 predictions; zero duplicate label IDs, duplicate prediction IDs, missing predictions, or extra predictions. Every served row identifies model `fixture-m1` and pipeline `serving-v4`.
- Source: 4 errors / 24 records, accuracy 0.8333333333333334; error IDs `source-01` through `source-04`. Both reviewed label groups have 2 errors / 12 records.
- Target: 16 errors / 24 records, accuracy 0.3333333333333333; error IDs `target-01` through `target-16`. Reviewed positives: 4 errors / 8 records. Pending positives: 4 errors / 4 records. Pending negatives: 8 errors / 12 records. There are no reviewed target negatives. Thus pending target labels total 12 errors / 16 records.
- Decision rationale recorded in the answer: these selected synthetic serving observations do not distinguish training optimization from path differences, generalization, or label validity; defer the training-choice decision and request a matched archived path comparison.
- Wrote `response-turn1.md` and this action record using `apply_patch`, then read both saved files to verify their content.
- Failures: none. No retraining, model execution, network access, delegation, external-system changes, or evidence-file writes occurred. The requested archived comparison remains pending; it was not executed.
````

#### response-turn2.md

````markdown
The new evidence supports changing the investigation: address the reported training/serving preprocessing discrepancy before choosing SGD, a learning rate, or more epochs. It explains part of the supplied error pattern, but substantial target-label disagreements remain. No retraining or model execution was performed.

**Current Problem Formulation, retained from turn 1 (inferred):** optimization or insufficient training may drive the new-site errors, making optimizer, learning rate, or duration appropriate levers.

**Primary Discriminating Test — completed on archived data:** I joined the 96 replay rows to the 48 labels by record ID and pipeline, and compared the two paths with the previously recorded serving predictions. Each record has exactly one prediction per replay path; there are no duplicate keys, missing pairs, or unknown records. Every replay row names `fixture-m1`. Serving replay agrees with recorded serving on all 48 records, so this comparison found no additional discrepancy between those exports.

| Selected site | Serving-v4 errors | Training-v2 errors | Serving errors corrected in training path | New errors in training path |
| --- | ---: | ---: | ---: | ---: |
| Source | 4/24 (16.7%) | 2/24 (8.3%) | 2 | 0 |
| Target | 16/24 (66.7%) | 10/24 (41.7%) | 6 | 0 |

The corrected IDs are `source-03`, `source-04`, and `target-11` through `target-16`. Residual errors are `source-01`, `source-02`, and `target-01` through `target-10`. The target path changes remove 6 of its 16 supplied-label disagreements, not the whole failure. The selected-set target-minus-source error gap falls from 50.0 to 33.3 percentage points.

`pipelines.json` reports identical resize (224 × 224) and scaling (divide by 255), with BGR in serving-v4 and RGB in training-v2. Its replay contract reports the same selected records and frozen model, and says only channel order differs. Under that supplied contract, the paired improvement supports channel order as a contributor within the fixture. This is stronger evidence than configuration differences alone because prediction changes align with improved label agreement. However, the metadata is not inspected executable code, and these synthetic saved predictions do not independently demonstrate the real effect of changing channel order or validate a deployment fix.

The residual target errors include 3 of 8 reviewed records and 7 of 16 audit-pending records. All reviewed target labels are positive. Of the six target corrections, one is reviewed and five are audit-pending. Thus the improvement and remaining error counts are against the supplied references; neither establishes target population accuracy. These are small selected sets, and records across sites are not matched individuals. The earlier reported 98% training and 97% within-source validation scores remain measurements on a different scope.

The evidence updates the live formulations as follows:

- **Serving preprocessing discrepancy — STRENGTHEN.** The matched archived comparison exhibits partial recovery consistent with the reported channel-order difference. It supports a contributor, not a complete explanation.
- **Optimization — WEAKEN as the immediate intervention target; UNRESOLVED as a residual contributor.** A fixed-model path comparison improves outcomes without additional training. That supplies a better-supported immediate target but does not rule out optimization affecting the remaining errors or show which training choice would help.
- **Site generalization — UNRESOLVED.** The training path retains more target than source disagreements, which is compatible with a generalization problem. Selection and incomplete label auditing prevent calling the residual gap proven domain shift.
- **Evaluation/reference-label problem — UNRESOLVED.** Seven residual target disagreements have pending labels. Three also occur against reviewed labels, so merely noting the pending audit does not explain every residual. No new label evidence arrived.

**Verdict: REFORMULATE.**

**Reformulated Problem:** the supplied failure has a supported preprocessing-path component and a remaining target-site/reference-label discrepancy whose cause is unresolved. Establish consistent preprocessing and valid residual evaluation before selecting a training intervention.

**Solutioning: NOT YET** for the original optimizer, learning-rate, or duration choices. Hand the documented RGB/BGR discrepancy to the downstream implementation workflow for verification against actual executable paths before any correction is treated as validated. The framing assessment does not establish that this correction will eliminate the target failure.

For the residual branch, the smallest useful next comparison is an independent adjudication of the seven pending labels among `target-01` through `target-10`, using the same labeling criteria as the source site, against their existing training-v2 predictions. If those labels change to agree with predictions, support shifts toward evaluation error; if upheld, support shifts toward genuine residual prediction errors on these records; a mixed result retains both. This would still leave three reviewed residual errors and would not distinguish generalization from optimization or estimate population performance. The needed images/adjudication evidence is absent, so this comparison remains pending. There is no basis here to rank SGD, learning-rate tuning, and longer training.
````

#### actions-turn2.md

````markdown
# Factual action record

- Read the assigned `prompts/skill-turn2.md` using PowerShell `Get-Content -Raw -LiteralPath`. This was the only additional read outside the assigned evaluation folder.
- Read complete `update.md`, `replay.json`, and `pipelines.json` within the assigned folder. Reused the complete skill instructions already read in turn 1.
- Ran a PowerShell computation reading `labels.json`, `served.json`, `replay.json`, and `pipelines.json` with `ConvertFrom-Json`. Built ID and ID/pipeline indexes, checked duplicate labels/served records/replay keys, rejected unexpected pipelines and unknown replay IDs, checked both replay paths for every label, and compared archived predictions with references and recorded serving predictions.
- Computed 96 replay rows, 48 joined labeled records, zero duplicate replay keys, and one replay model ID (`fixture-m1`). No missing pairs, unexpected pipelines, unknown replay records, or duplicate labels/served records triggered the command's checks. Serving replay disagreed with recorded serving on 0 of 48 records.
- Source: serving errors 4/24; training errors 2/24; 2 path disagreements, both corrections (`source-03`, `source-04`); no new errors. Residuals: `source-01`, `source-02`.
- Target: serving errors 16/24; training errors 10/24; 6 path disagreements, all corrections (`target-11` through `target-16`); no new errors. Residuals: `target-01` through `target-10`.
- Computed audit/reference-label groups: source reviewed negatives 2 serving errors and 1 training error / 12; source reviewed positives 2 and 1 / 12; target pending negatives 8 and 5 / 12; target pending positives 4 and 2 / 4; target reviewed positives 4 and 3 / 8.
- Derived in the answer from these counts: source error rates 16.7% versus 8.3%; target 66.7% versus 41.7%; target-minus-source gap 50.0 versus 33.3 percentage points. Target residuals include 3 reviewed (`target-01`, `target-05`, `target-09`) and 7 pending. Target corrections include 1 reviewed and 5 pending.
- Metadata read: both paths report resize 224 by 224 and division by 255; serving reports BGR and training reports RGB. The synthetic replay contract reports the same records and frozen model with only channel order different; executable implementations were not available or inspected.
- Saved `response-turn2.md` and this `actions-turn2.md` with `apply_patch`, then read both saved files to verify content. First-turn output files and supplied evidence were preserved.
- Updated the overall verdict to REFORMULATE: supported partial preprocessing discrepancy plus unresolved residual target/reference-label problem. The answer keeps optimizer choices deferred and identifies a bounded pending audit comparison for the residual branch.
- Failures: none. No retraining, model execution, network access, delegation, external-system changes, or evidence edits occurred. No label adjudication or executable pipeline verification was performed.
````

## Independent fixture review

````markdown
# Independent hostile fixture review: R03-RAW

The frozen fixture is internally coherent as a staged, synthetic evidence-use exercise. Every published numerical expectation matches an independent ID join of the raw JSON. Its paired comparison fairly tests artifact inspection and a scoped update after the second packet arrives. It does not establish actual classifier execution, the true target-site benefit of changing preprocessing, or a causal benefit of the skill. Two grading-contract issues deserve clarification; no fatal numerical or pairing defect was found.

## Scope and method

I read only `frozen/turn1/*`, `frozen/turn2/*`, `hidden/expectations.md`, `hidden/rubric.md`, and `prepare.py`. I did not inspect `runs/`, `prompts/`, `snapshot/`, prior task material, or execution outputs. I did not execute `prepare.py`, use the network, delegate, or modify a fixture or repository file. The only file written for this review is this report.

I parsed the three prediction/label JSON files with Python's standard library, checked key multiplicities and coverage before creating lookup dictionaries, joined by record ID and pipeline ID, and counted disagreement with each supplied reference label. These calculations read the frozen JSON, independently of the generator's error-threshold expressions and the expected counts. A separate enumeration varied the five pending labels on changed target predictions to check sensitivity. No model was executed.

## Verified raw counts

Integrity checks passed: 48 unique label rows, 48 unique served rows, and 96 unique replay cells. Every labeled ID occurs in served predictions and in exactly one replay row under each of the two pipelines. There are no duplicate keys, missing IDs, or extra IDs. All predictions name `fixture-m1`; all labels and predictions are binary. All 48 saved serving predictions agree with their serving-path replay cells.

All errors below mean disagreement with the supplied labels, regardless of audit status.

| Site / label audit | Records | Serving errors | Training-path errors | Wrong to correct | Correct to wrong | Wrong under both | Correct under both |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Source / all reviewed | 24 | 4 | 2 | 2 | 0 | 2 | 20 |
| Target / all | 24 | 16 | 10 | 6 | 0 | 10 | 8 |
| Target / reviewed | 8 | 4 | 3 | 1 | 0 | 3 | 4 |
| Target / pending | 16 | 12 | 7 | 5 | 0 | 7 | 4 |

The two source improvements are `source-03` and `source-04`. The six target improvements are `target-11` through `target-16`; only `target-13` has a reviewed label. No supplied-label regression occurs.

- Source error falls from 16.67% to 8.33%, an 8.33 percentage-point reduction, or 2/24 records.
- Target error falls from 66.67% to 41.67%, a 25 percentage-point reduction, or 6/24 records. This removes 6/16 = 37.5% of the original target serving errors against the supplied labels.
- The descriptive target-minus-source gap falls from 12/24 = 50 percentage points to 8/24 = 33.33 percentage points. Its reduction is 4/24 = 16.67 percentage points, or one third of the original gap.
- Target residual errors are 10/24; residual target-minus-source excess is 8/24. These must not be interchanged.

Each complete site sample has 12 labels of each class. The target reviewed subset has eight class-1 labels and zero class-0 labels; its pending subset has four class-1 and twelve class-0 labels. A reviewed-only target rate therefore describes a selected, single-class subset, not a validated estimate for the complete target set.

## Actionable contract defects

### P2: The required update can be read as requiring a stronger contribution claim than the evidence establishes

`hidden/expectations.md` requires an insufficient-evidence answer to update the “known partial pipeline contribution.” Elsewhere the contract correctly limits the claim to synthetic outputs, supplied labels, and reported configuration metadata. The quoted requirement is nevertheless ambiguous about what is known. The records establish that the authored pipeline cells produce different saved predictions and that one path has fewer disagreements with the supplied labels. They do not establish beneficial effects on true target labels or isolate a verified channel-order implementation as the cause.

This distinction matters numerically: five of the six changed target records have pending labels. Taking the reviewed labels as correct, and allowing the five pending binary labels on changed predictions to be either value, the actual net target error reduction can be -4, -2, 0, 2, 4, or 6 records. Its range is therefore -4/24 to +6/24, or -16.67 to +25 percentage points. Unchanged predictions contribute zero to this paired difference regardless of their labels. This is a worst-case sensitivity calculation, not evidence that any pending label is wrong.

Action: make the acceptance rule say “known difference between the authored prediction paths, with a 6/24 improvement against the supplied reference labels, conditional on those labels and the reported replay contract.” Explicitly accept an answer that recognizes this change while declining to claim a true net target benefit. The current general caveats substantially mitigate the problem, so this is a grading-clarity defect, not a fatal causal contradiction. Auditing the five pending labels on changed records is also a proportionate next request if the next decision concerns the direction of the target benefit.

### P2: The copied rubric has an unresolved scenario-contract dependency

`hidden/rubric.md` instructs the grader to use `cases.md` for scenario-specific behavior, but no `hidden/cases.md` is present in the inspected packet, and `prepare.py` does not copy one. The packet instead supplies `hidden/expectations.md`. Fetching a different scenario description from outside this packet could silently import an older case's scope or verdict requirements.

Action: explicitly identify `hidden/expectations.md` as the scenario contract for R03-RAW and state that the rubric's `cases.md` reference is superseded for this fixture. This can be done in grader instructions without changing the five dimensions or penalties. I did not inspect an external `cases.md` to resolve the dependency. This issue concerns reproducibility of the supplied grading packet, not an assertion that any grader actually followed the wrong reference.

Neither issue warrants silently rewriting frozen expectations or independent scores after seeing arm results. Preserve this review separately and record any interpretation or future fixture revision transparently.

## What the paired and staged design fairly tests

The within-site pairing is sound at the artifact level. Matching the same IDs and model under both paths removes cross-record composition as an explanation of the recorded within-site difference. Shuffled row order makes ID-based joining consequential. The stable serving cells also allow a real consistency check between the first packet and the replay packet.

The first turn has enough accessible data to compute the served error rates and inspect audit coverage. It cannot execute the proposed two-path comparison because those predictions and pipeline metadata are absent. A bounded pending request is appropriate and should incur no evidence-deflection penalty. Strong first-turn behavior need not guess RGB/BGR, which is not disclosed until turn 2. The contract appropriately allows alternative well-reasoned discriminators.

The fixed second packet can test whether an assistant executes the available comparison and updates rather than merely repeating its initial framing. Its fixed availability also avoids conditioning the evidence on which arm asked the favored question. However, the second packet is supplied even if the assistant never selected this comparison. Score the initial test choice from the first-turn answer separately in supporting evidence; do not infer successful autonomous selection from competent second-turn execution alone. This is an interpretation limit of the full-transcript score, not a defect that requires withholding the second packet.

The first packet already announces that archived replay exports are unavailable. That is a useful availability boundary but also a strong cue toward the expected test. The task measures selection with that cue, not wholly spontaneous discovery of a preprocessing explanation.

## Verdict and causal limits

A scoped WEAKEN is coherent for the premise that optimizer changes should be the first intervention, or for a claim that optimization alone explains every observed error. INSUFFICIENT EVIDENCE is coherent for the stronger question of which cause is primary, provided the answer incorporates the paired result. The public question only suggests optimizer-centered thinking; the evaluator must not treat it as an explicit claim that optimization is the sole cause.

No optimizer, learning-rate, or training-duration intervention exists here. Training and random source-validation scores come from different records and cannot identify convergence, target generalization, or the best optimizer. A partial preprocessing-associated improvement does not rule out optimization as a substantial or primary contributor to the remaining problem. Conversely, the residual cross-site gap does not establish population shift or label problems. The sites contain unmatched selected records; neither a causal site effect nor a population rate follows.

`pipelines.json` reports that channel order is the only difference. It contains metadata, not executable pipelines, images, or model hashes. Conditional reasoning within this authored scenario is legitimate; claiming that a real RGB/BGR defect was executed, verified, or fixed is not. Even the reviewed labels are authored audit statuses rather than independently demonstrated truth.

## Optional improvements and limits on evaluation claims

- Record separate descriptive indicators for first-turn test selection, actual JSON inspection, correct ID joining, complete pairing, numerical correctness, and second-turn revision. The unchanged behavioral score can remain, but a high total alone is insufficient evidence of correct execution; the rubric already permits separate material review flags.
- For later development fixtures, vary the cue strength and include no-change, mixed improvement/regression, absent-pair, and inconsistent-export cases. This fixture has a simple threshold-generated pattern and zero regressions; one success does not establish robustness to messy raw evidence.
- Use opaque or differently assigned IDs in future variants to reduce the accidental relation between numeric ID suffixes and error membership. The present IDs still support valid joins; this is a realism improvement, not a current arithmetic defect.
- A single same-configuration baseline/skill pair is a local behavioral observation. It cannot separate treatment effects from response variability or support general superiority. Explicit skill invocation also makes treatment visible in wording, so A/B labels provide only limited grader blinding, as the contract acknowledges.
- `prepare.py` shows that both evidence packets are authored before execution and creates matching first-turn evidence. Its source alone cannot verify runtime model/configuration equality, actual isolation, or that packet 2 was released only after both first turns finished. Those require execution records, which were deliberately outside this review's scope.

Overall, retain this as a bounded developmental case with correct arithmetic and useful staged evidence. Resolve the two contract ambiguities and keep artifact-level success, true model behavior, and skill-effect inference separate when reporting results.
````

## Independent grading

The grader received the public inputs above, the frozen expectations, the
unchanged [rubric](rubric.md), and the exact response/action records under
conditions A and B. Mapping, skill snapshot, prior evaluations, and fixture
review were withheld. In this record A is skill and B is baseline.

### Grader instructions

````markdown
# Independent grading instructions

Read only packet.md, expectations.md, and rubric.md in this grading folder.
Do not read parent/sibling folders, the skill snapshot, arm mapping, earlier
evaluations, fixture-review.md, or any other agent's context. No network or
delegation. Write only grades.json and review.md in this folder.

Grade each condition's complete two-turn transcript using the unchanged five
rubric dimensions and its penalties. Quote concise observable evidence for
deductions and review flags. Judge actual actions, numerical accuracy, claim
scope, and evidence updates, without rewarding protocol vocabulary or length.
Score the first-turn test choice from turn 1 itself: turn 2 was delivered to both
conditions regardless of their request, so later execution does not prove earlier
autonomous test selection. Do not infer an arm label; it is withheld deliberately.

The following two clarifications were added after an independent fixture review,
before grading. They do not alter the frozen evidence, agent inputs, dimensions,
or penalties; preserve the original expectations in the packet for audit:

1. For this R03-RAW variant, expectations.md is the scenario contract. The generic
   rubric's cases.md link does not authorize reading an external case description.
2. Interpret "known partial pipeline contribution" in expectations.md as a known
   difference between the authored prediction paths, with improvement against the
   supplied labels conditional on those labels and the reported replay contract.
   It is not an established true-label benefit or verified executable causal
   mechanism. Target labels are incompletely audited. Accept cautious responses
   that update the recorded path difference while declining to assert true net
   target benefit. Do not require an unrequested worst-case sensitivity analysis
   to earn full credit; a sufficient local qualification of claims can suffice.

grades.json schema:
{
  "case_id": "R03-RAW",
  "conditions": [
    {
      "condition": "A",
      "dimensions": [null, null, null, null, null],
      "contrarianism_penalty": null,
      "evidence_deflection_penalty": null,
      "raw": null,
      "normalized": null,
      "final": null,
      "dimension_reasons": ["D1 evidence", "D2 evidence", "D3 evidence", "D4 evidence", "D5 evidence"],
      "review_flags": [],
      "indicators": {
        "turn1_test_selection": "observation with evidence",
        "turn2_direct_computation": "observation with evidence",
        "id_join_and_pair_completeness": "observation with evidence",
        "gap_and_target_error_denominators": "observation with evidence",
        "scope_and_provenance": "observation with evidence"
      }
    }
  ]
}

Include both A and B; replace each null with the actual numeric grade.
Multi-turn raw = sum of five dimensions;
normalized = raw; final = max(0, normalized + both penalties).
Use review.md to explain material distinctions, grading ambiguities, and any
alternative reasonable score. A high score does not erase a review flag.
Save original scores before author review; do not rewrite scores to favor a condition.
````

### Original grade data

````json
{
  "case_id": "R03-RAW",
  "conditions": [
    {
      "condition": "A",
      "dimensions": [
        2,
        2,
        2,
        2,
        2
      ],
      "contrarianism_penalty": 0,
      "evidence_deflection_penalty": 0,
      "raw": 10,
      "normalized": 10,
      "final": 10,
      "dimension_reasons": [
        "D1 = 2. Turn 1 begins 'Defer switching to SGD, changing the learning rate, or training longer' because the evidence cannot establish optimization as the appropriate intervention. It computes the existing descriptive evidence before selecting a further investigation. Turn 2 still defers those training choices; no retraining or correction was performed.",
        "D2 = 2. It preserves the optimizer framing as an inference and a hypothesis, then identifies the consequential assumption 'Insufficient optimization materially contributes.' It also identifies same-input/frozen-model comparability and reference-label validity as assumptions whose failure changes interpretation. Different source-validation records are not treated as a serving regression.",
        "D3 = 2. Turn 1 distinguishes optimization, site generalization, serving-path discrepancy, and evaluation/reference-label problems, with different evidence and intervention targets. Adam, learning rate, and duration are grouped within optimization. Turn 2 retains the unresolved alternatives instead of attributing the residual gap to domain shift.",
        "D4 = 2. Turn 1 independently selects a bounded same-record comparison of reference-path and serving-replay predictions with the recorded serving export, checking frozen checkpoint/input versions and stratifying within sites. Its contrasting outcomes include recovery, parity, archived-versus-recorded disagreement, and partial recovery. Turn 2 executes that comparison and proposes a scoped pending adjudication of seven residual pending labels, explicitly noting what it cannot distinguish. No test is credited from turn 2 retroactively.",
        "D5 = 2. Turn 2 strengthens the preprocessing-path contribution, weakens optimization 'as the immediate intervention target' while retaining it as a residual contributor, and leaves generalization/label validity unresolved. The response explicitly says the contributor is 'not a complete explanation' and that implementation verification is pending. REFORMULATE is interpreted by these qualified substantive updates, not rewarded or penalized as a word."
      ],
      "review_flags": [],
      "indicators": {
        "turn1_test_selection": "Selected before replay delivery: 'obtain the archived reference-path and serving-replay predictions for these same 48 records' and compare by record ID, with explicit outcome-dependent changes. The absent exports are a legitimate pending request, not deflection.",
        "turn2_direct_computation": "Action record reports a local PowerShell computation over labels, served, replay, and pipeline metadata. Computed source errors 4/24 to 2/24 and target errors 16/24 to 10/24, with 2 and 6 corrections and no introduced errors. These agree with an independent recomputation from the packet.",
        "id_join_and_pair_completeness": "Both turns use ID indexes, not row order. Turn 2 checks ID/pipeline keys, both replay paths for all 48 labels, duplicate/unknown keys and unexpected pipelines, frozen model identity, and zero disagreements between 48 archived and original serving predictions. Packet recomputation confirms 96 rows, 48 complete pairs, no duplicate keys, and zero serving mismatches.",
        "gap_and_target_error_denominators": "Correctly separates '6 of its 16 supplied-label disagreements' from the selected-site gap falling from 50.0 to 33.3 percentage points. The implied target reduction is 37.5% (25 percentage points), whereas the gap shrinks by 16.7 percentage points, one third of its original value. It does not conflate them. Omitting the explicit derived percentages is not a numerical error.",
        "scope_and_provenance": "Qualifies channel-order contribution with 'Under that supplied contract' and says authored predictions do not independently demonstrate a real effect or validate a fix. Notes 1 reviewed/5 pending target corrections, 3 reviewed/7 pending residual disagreements, all reviewed target labels positive, selected samples, and unmatched cross-site records. Claims remain conditional on supplied labels and metadata; no true-label net benefit or executable causal mechanism is asserted."
      }
    },
    {
      "condition": "B",
      "dimensions": [
        2,
        2,
        2,
        2,
        2
      ],
      "contrarianism_penalty": 0,
      "evidence_deflection_penalty": 0,
      "raw": 10,
      "normalized": 10,
      "final": 10,
      "dimension_reasons": [
        "D1 = 2. Turn 1 keeps the existing optimizer, rate, and duration unchanged because the files 'do not establish an optimization problem or rank the three proposed remedies.' It examines the current records before recommending a next comparison. Turn 2 prioritizes verification of the path discrepancy and continues to defer training choices; no unauthorized intervention occurred.",
        "D2 = 2. It identifies that the proposed remedies require evidence of an optimization problem, that within-source validation does not measure new-site performance, and that incomplete and class-unbalanced label review limits conclusions. The requested comparison holds underlying inputs, model identity, class mapping, and threshold constant so path attribution has a meaningful basis.",
        "D3 = 2. Turn 1 distinguishes serving transformations, target generalization/data coverage, label conventions/audit, and shared evaluation/model-report issues from optimization. Its outcome branches lead to different investigations. These are substantive alternatives despite not appearing in a named formulation table.",
        "D4 = 2. Turn 1 independently requests a frozen-model reference-path replay for the same 48 records, paired to serving predictions within site, and specifies corrections, introduced errors, and residuals. It explains how path recovery versus persistent target or shared-site failure changes the decision. Turn 2 performs the paired comparison; the leading follow-up is executable channel-order verification with controlled reproduction and an explicit mismatch contingency. The subsequent label-review and later validation sequence does not turn the central comparison into a low-information checklist.",
        "D5 = 2. Turn 2 changes the next step to verifying/aligning channel order under the supplied contract, identifies an incomplete path explanation with 10 residual target disagreements, and retains optimization/generalization/label causes as unresolved. It explicitly states that the gap does not establish 'domain shift, label error, undertraining, or an Adam-specific failure' and does not select a training remedy."
      ],
      "review_flags": [],
      "indicators": {
        "turn1_test_selection": "Before seeing replay, asks for 'an archived reference-path replay export for these same 48 records' using frozen fixture-m1 and training/evaluation preprocessing, paired by ID within site with input/model/class/threshold checks. Both corrections and regressions are requested; outcome branches explain decision implications.",
        "turn2_direct_computation": "Action record reports PowerShell joins, uniqueness/coverage/model checks, original-serving comparison, and error/transition calculations. Source 4/24 to 2/24 and target 16/24 to 10/24, with 2 and 6 corrections and zero regressions, agree with independent packet recomputation. Residual reviewed/pending counts and false-positive/false-negative counts are accurate.",
        "id_join_and_pair_completeness": "Turn 1 matches 48 unique labels/predictions. Turn 2 keys replay by record ID plus pipeline, requires both paths per label, checks total coverage and model identity, and confirms all archived serving values and identities match the original. The action record expressly reports 48 paired records and no duplicate/unmatched rows.",
        "gap_and_target_error_denominators": "Reports errors on 24 records per site and the target-minus-source gap decreasing from 50 to 33.3 percentage points. Six target corrections out of 16 original target errors are available in the table; it does not mistake that 37.5% relative reduction for the one-third relative reduction of the between-site gap. Not stating either relative percentage explicitly is an omission of optional arithmetic, not a conflation.",
        "scope_and_provenance": "The phrase 'improvement is verified at the record level' immediately follows 'Errors are measured against the supplied reference labels' and concerns paired JSON values. The next causal statement is qualified by the supplied replay contract, followed by explicit denial of executable inspection, reproduced real effects, or deployment guarantees. It marks the full residual provisional, identifies the all-positive reviewed subset, and disclaims population and causal-site inferences. These local/contextual qualifications satisfy the amended grading instructions."
      }
    }
  ]
}
````

### Original grading review

````markdown
# Independent grading review: R03-RAW

Read scope: only this folder's instructions.md, packet.md, expectations.md, and rubric.md. No network, delegation, other folders, prior evaluations, or arm mapping was used. This review records the original independent scores.

| Condition | D1 | D2 | D3 | D4 | D5 | Contrarianism | Deflection | Final |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| A | 2 | 2 | 2 | 2 | 2 | 0 | 0 | 10/10 |
| B | 2 | 2 | 2 | 2 | 2 | 0 | 0 | 10/10 |

These are two condition scores on one staged fixture, not evidence of a general performance difference. Neither length nor protocol vocabulary earns credit. No material numerical, causal, provenance, or authorization review flag is supported when each claim is read with its local qualifications.

## Evidence and numerical verification

I independently extracted the supplied labels, served predictions, and replay predictions from packet.md and recomputed the paired counts in memory. The packet contains 48 unique labeled records, 48 original predictions, and 96 replay rows with unique record/pipeline keys and a complete pair per label. Archived serving predictions match original serving predictions on all 48 records.

The recomputation gives source errors 4/24 versus 2/24, and target errors 16/24 versus 10/24. All 8 changed predictions improve agreement with supplied labels: 2 source and 6 target; no introduced errors. Target reviewed-label errors go from 4/8 to 3/8; pending-label errors go from 12/16 to 7/16. All 8 reviewed target labels are positive. Both transcripts report these results accurately.

There are two distinct quantities: target error decreases by 6/24 = 25 percentage points, or 6/16 = 37.5% of its serving errors; the between-site error gap decreases from 12/24 to 8/24, a reduction of 4/24 = 16.7 percentage points, or one third of the original gap. A explicitly reports “6 of its 16 supplied-label disagreements” separately from the gap. B reports the correct counts and gap. Neither confuses the denominators. Full credit does not require spelling out every derived relative percentage.

## Material distinctions

A's first-turn comparison requests both archived paths and checks them against original serving. It explicitly anticipates replay parity with the recorded export, replay parity that disagrees with the export, partial recovery, and noncomparability. B's first-turn request uses the archived reference path and existing serving output, with explicit checks for input identity, checkpoint, mapping, threshold, corrections, and regressions. Both are bounded, informative comparisons chosen in turn 1 itself. A's extra outcome detail is useful but does not justify reducing B below the rubric's full-credit threshold.

A presents named formulations and status changes, including “WEAKEN as the immediate intervention target; UNRESOLVED as a residual contributor.” B expresses the same kind of substantive revision through the next-action priority and explicit limits on what the residual gap establishes. Both update from an unlocalized failure to a conditional, partial path contribution plus unresolved residual causes. The formatting difference has no scoring value.

A proposes adjudicating the seven pending labels among residual target disagreements as its next bounded residual comparison. It explains the possible outcomes and expressly says this cannot distinguish generalization from optimization or estimate population performance. B recommends completing the pending label review across the target set and then using audited target-relevant validation. A's narrower test is sufficient for its stated residual-label question; B's broader staged advice remains proportionate. Neither has access to images or adjudication evidence, so pending requests incur no deflection penalty.

## Scope ambiguities resolved

A's verdict “REFORMULATE” differs from the example verdict labels listed in expectations.md. The unchanged rubric instructs grading behavior rather than exact verdict wording. A does not claim that optimization is disproved or cannot remain primary: its original formulation is expressly inferred and tentative, its weakening is limited to the immediate intervention target, and it retains optimization as unresolved for residual errors. Its reformulation includes the observed partial path component and unresolved residual. Deducting solely for the verdict word would be inconsistent with the behavioral rubric.

A's “supports channel order as a contributor within the fixture” is preceded by “Under that supplied contract,” and followed by the explicit statement that the synthetic outputs do not independently demonstrate a real channel-order effect or validate a deployment fix. It also identifies that five of six target corrections concern pending labels. This is the conditional recorded-path update allowed by the instruction clarification, not an established true-label benefit or independently verified mechanism.

B writes “the improvement is verified at the record level.” In isolation that could be read too strongly. Locally, however, it immediately follows “Errors are measured against the supplied reference labels” and describes the named paired records, then expressly states: “I have not inspected executable preprocessing, images, or a model, and have not reproduced a real channel-order effect.” Its mechanistic inference is also qualified by the supplied replay contract. Consequently this is verification of fixture arithmetic, not fabricated independent model verification. No revision is required on the evidence shown.

Both responses recognize incomplete target auditing and selected/nonrepresentative samples. Neither performs a worst-case true-label sensitivity analysis. Under the explicit grading clarification, this is not required when local claims are sufficiently qualified; it is not grounds for a flag or deduction.

## Alternative scoring and limitations

A stricter reading could propose 9/10 for A on D5 if “REFORMULATE” were taken to reject optimization's possible primacy, or 9/10 for B on D5 if “verified” were taken to claim a real or true-label effect. Those readings are not adopted because the surrounding text explicitly limits both claims. No alternative lower score is warranted by the complete transcript under the supplied clarification.

The two perfect scores indicate that both conditions meet the five coarse rubric thresholds on this fixture. They do not establish equivalent performance beyond this case, nor certify a real preprocessing cause or a validated deployment intervention. These judgments use the packet's factual action records; they are not an audit of unprovided execution logs.

````

## Author review and resulting edits

Both conditions selected and executed a useful comparison with this staged
artifact packet. The independent grader recomputed the data and gave each
condition 10/10, with no penalties or material review flags. The author agrees
with the numerical findings and with treating qualified claims in context.
The skill's additional detail did not raise its rubric score over the baseline;
its two responses were longer. No effectiveness or equivalence claim follows.

Two fixture-contract issues caused actual corrections to the grading instructions:

- The frozen phrase "known partial pipeline contribution" can imply a true-label
  benefit. The clarification confines it to differences between authored paths
  and improved agreement with the supplied references, conditional on the labels
  and reported replay contract. It explicitly allows withholding a claim of true
  net benefit. Five of six target corrections have pending labels. The author
  independently enumerated their 32 binary assignments and confirmed the fixture
  review's bound of four additional errors to six fewer errors. This sensitivity
  calculation is not retroactively required for a full score.
- The copied rubric links to `cases.md`, which is absent from the isolated grading
  folder. The instructions now designate `expectations.md` as this variant's
  scenario contract and prohibit importing a different case. The distribution's
  rubric and its valid repository link remain unchanged.

These clarifications came from a reviewer who had no execution outputs. They were
added before grading and were not delivered to the executing agents. The frozen
expectations, raw evidence, actual responses, and original grades are preserved
above, so the interpretation change remains reviewable.

The author specifically reviewed the treatment's `REFORMULATE`. Its stated
original formulation is tentative, its update weakens optimization only as the
immediate intervention target, and the replacement explicitly retains unresolved
residual causes. It neither kills optimization nor claims channel order explains
everything. The grader accepts that substantive mixed framing and records why a
verdict-word-only deduction would be inappropriate. A stricter reader could
prefer `INSUFFICIENT EVIDENCE` about optimization's primacy or scoped `WEAKEN` of
the proposed intervention priority. This judgment boundary remains explicit;
the original 10/10 is not rewritten. The baseline's "verified at the record
level" likewise refers locally to supplied-label arithmetic and is accompanied
by a denial of real model or executable verification.

No new runtime rule is justified by this pair. The existing skill already
requires source preservation, matched discrimination, claim-strength control,
and scoped handoff; both responses apply those behaviors here. `SKILL.md` stays
at 281 lines with the tested hash. Actual repository edits add this reusable
Markdown fixture/result record and link it from the project README, evaluation
README, and R03 case. No package, evaluation runtime, or classifier implementation
enters the distribution. The canonical case count remains 20. Earlier smoke and
full-suite records, including failures and differing judgments, remain intact.

The earlier R03 limitation is not declared solved. This variant explicitly cues
an unavailable replay export, and the second packet supplies exactly the paired
rows. The original report-only/fewer-cue setting still has its recorded weak
first-round discrimination. These results show that both conditions can select
and compute this comparison under this cue and evidence condition; changing the
fixture prevents attribution to an instruction improvement.

Remaining limits are concrete: one pair in one model/configuration class and
host; coarse qualitative grading; vocabulary-visible treatment; action records
written by the executing agents rather than a full archived tool trace; authored
predictions rather than a model run; selected records, incomplete target labels,
simple ID/error patterns, and no regressions or malformed pairs. A later test
should reduce the replay cue and include mixed corrections/regressions or missing
pairs before claiming robust independent test selection and data handling.

## Verification

The source-row computation confirms all 48 record IDs, complete coverage of 96
replay cells, agreement of all 48 serving exports with their replay cells, the
four error counts, and the two distinct reduction denominators. Frozen inputs
are identical across arms. The skill snapshot is unchanged.

The final checks after assembly passed:

- Skill creator's `quick_validate.py`: `Skill is valid!`.
- Repository audit: 829 assertions passed, 0 failed; nine distribution files,
  eight Markdown files, 24 internal links, and 281 skill lines. This includes
  case counts, frontmatter, Markdown fences, links, score arithmetic, license,
  whitespace, UTF-8/no BOM, and absence of private workstation paths.
- Historical evaluation audit: 639 assertions passed, 0 failed. The archived
  40 case runs / 54 responses and earlier probes/retests remain consistent.
- R03-RAW audit: 220 assertions passed, 0 failed. It verifies frozen hashes,
  identical evidence in both arms, the unchanged skill, all four response/action
  pairs, exact archived wording after documented normalization, pairing and
  serving consistency, label-sensitivity bounds, and grade/table arithmetic.
  Completion hashes preserve the original execution and grading artifacts.
- `git diff --check`: clean. Because files are still untracked, the repository
  audit also checks their actual contents rather than relying on Git's diff.

Only local artifact computations and consistency checks ran. There was no model
execution or live-system test, and no commit, push, PR, publication, or tag.

### Independent author computation from frozen rows

````json
{
  "records": 48,
  "served_rows": 48,
  "replay_rows": 96,
  "error_counts": {
    "source/serving-v4": 4,
    "source/training-v2": 2,
    "target/serving-v4": 16,
    "target/training-v2": 10
  },
  "serving_gap_pp": 50,
  "training_gap_pp": 33.333333333333336,
  "gap_reduction_fraction": 0.3333333333333333,
  "target_error_reduction_fraction": 0.375,
  "target_pending_labels": 16,
  "frozen_files_verified": 15
}
````
