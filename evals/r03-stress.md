# R03 with fewer cues, regressions, and missing pairs

This synthetic development case follows the [first row-level R03 test](r03-raw.md).
It removes the initial replay-availability hint and tests a mixed result with
incomplete comparison data. The skill snapshot stays unchanged. It is a new
variant of [R03](cases.md#r03--optimizer-variants-do-not-cover-distribution-failure),
not an additional canonical case or a controlled estimate of skill improvement.

## Protocol fixed before execution

- Date: 2026-09-11. Skill SHA-256:
  `6fb703944d9319fb3509b3fb258772c6cfc27f4bfcff960681ea500923710fc8`.
- A fresh baseline context and a fresh skill context receive identical public
  tasks, evidence, tools, and permissions. Only the treatment loads the complete
  skill explicitly. Both inherit the same configuration/model class, with no
  model override; exact backend revision, seed, and sampling settings are unknown.
- First-turn artifacts contain labels, serving predictions, and a training
  report. They do not announce replay exports or a future comparison. Structured
  diagnostic files still provide context, so this is fewer-cue selection rather
  than a wholly uncued real-world diagnosis.
- Second-turn data and expectations are authored and hashed before execution.
  After both first turns finish, their responses/actions are sealed and the same
  fixed comparison packet is delivered to each existing context, regardless of
  its first-turn request. Later execution cannot prove earlier test selection.
- The fixture has 48 selected records, 24 per site, with opaque IDs and shuffled
  rows. All label audit statuses are reported reviewed and cover both classes.
  The second packet has 90 rows: 48 serving and 42 reference-path predictions.
  Six target reference cells are absent. No true completion is authored for them.
- Corrections and regressions coexist. Missing reference cells are concentrated
  among serving errors. Different-coverage marginal rates can suggest improvement
  while the complete target pairs worsen. Full-target benefit remains uncertain.
- All predictions, metadata, and audit statuses are synthetic. There are no raw
  images, classifier binary, executable preprocessing, or real deployment. Direct
  JSON computation verifies properties of these authored rows only.
- Agents may read assigned evidence and write local analysis/responses in separate
  temporary folders. Evidence edits, network, retraining, external actions, and
  delegation are excluded. Isolation is instructional, not an OS sandbox.
- An independent fixture reviewer receives raw inputs and frozen expectations,
  without generator, skill, or execution outputs. A separate fresh grader receives
  inputs, transcript/action records, the unchanged rubric, and variant expectations
  with arm labels withheld. Vocabulary can expose treatment; this is label
  blinding only. Original grading is preserved before author review.

## Reuse and interpretation

Materialize only archived `turn1/` inputs in each fresh execution folder. Supply
the complete archived skill only to the treatment. Keep `turn2/` withheld until
the first response completes; deliver it in the same context. Use the recorded
execution packets for scope and output capture. Withhold results, expectations,
reviews, and sibling outputs from execution agents.

This variant changes cueing, error patterns, missingness, label-audit coverage,
and ID format together. A different result cannot be attributed to any one of
those changes. One same-configuration pair cannot establish general effectiveness,
cross-model portability, or a causal skill benefit. The canonical suite remains
20 cases. This Markdown record is development material, not a runtime dependency.

## Results

Completed **two case runs in separate fresh contexts, with two turns each
(four saved responses)**. Both turn-1 responses propose a same-record, frozen-model path
comparison without being told that comparison exports will arrive. The treatment
also labels an earlier descriptive site comparison as its executed Primary Test;
the independent review below assesses its adequacy separately.

Original independent multi-turn grades:

| Arm | D1 / D2 / D3 / D4 / D5 | Penalties C / E | Final /10 |
| --- | --- | --- | --- |
| Baseline | 2 / 2 / 2 / 2 / 2 | 0 / 0 | 10 |
| Skill | 2 / 2 / 2 / 2 / 2 | 0 / 0 | 10 |

C/E = contrarianism / evidence deflection. Totals do not override material flags
or establish a stable treatment effect. See preserved grading and author review.

Both conditions inspect the new rows, join by record and path, count corrections
and regressions, identify all six missing target cells, and reject the apparent
benefit from different-coverage rates. They distinguish paired target harm from
the unresolved result for the full target set and do not recommend releasing a
preprocessing switch as a proven fix. Both give correct full-target bounds; the
skill additionally states that at least three of the six absent predictions must
be correct to improve the selected target set, while two correct predictions tie.

The baseline expresses the bounds as errors (4-10/24); the skill expresses them
as accuracy (14-20/24), versus serving accuracy 16/24. These are equivalent. Both
describe conditional path effects within the authored fixture and preserve the
distinction from executing a classifier or verifying real channel-order behavior.

The author independently verifies the following quantities against supplied labels:

| Scope | Complete pairs | Serving errors on those pairs | Reference errors on those pairs | Corrections / regressions |
| --- | --- | --- | --- | --- |
| Source | 24 | 4/24 | 2/24 | 3 / 1 |
| Target | 18 | 2/18 | 4/18 | 1 / 3 |
| Pooled | 42 | 6/42 | 6/42 | 4 / 4 |

Six target reference predictions are absent, all on records with serving errors.
Comparing **8/24** serving errors against **4/18** reference errors uses different
records and suggests improvement; the actual complete-pair comparison **2/18 to
4/18** worsens by 11.1 percentage points. Source pairs improve by 8.3 points.

For all 24 target records, reference errors are bounded **4-10**, versus eight
serving errors: from four fewer to two more errors. Full-target direction is
unresolved. Across all 48 records, reference errors are bounded **6-12**, versus
12 serving errors; conditional pooled non-worsening is supported, while strict
pooled improvement and target benefit are not established. These are fixture
sensitivity bounds over 64 possible completions, not known missing predictions
or estimates for a population. No particular completion is imputed.

Answer length across both turns: baseline **1077**, skill **1349** whitespace-delimited
words, including Markdown. This is output length, not token, price, or latency data.

## Pre-execution expectations

````markdown
# R03-STRESS pre-execution scenario contract

This is a new synthetic R03 variant, not a controlled estimate of improvement
over R03-RAW. It removes the first-turn announcement of absent replay exports,
introduces corrections and regressions, and makes reference-path predictions
missing for six target records. All supplied label audit statuses now say reviewed
and cover both classes. IDs are opaque. These multiple changes preclude isolating
which fixture change accounts for a different result. Skill stays unchanged.

Two fresh contexts, same inherited configuration class, identical task/evidence,
tools, and permissions: baseline without skill; treatment explicitly loads it.
Future packets and this contract are withheld from executing agents. Turn 2 is
fixed before execution and delivered after both turn-1 responses finish, regardless
of their requests, to the same respective contexts. No model override is used.
The first packet has no replay/comparison-archive availability announcement. It
still supplies structured diagnostic metadata; do not claim an entirely uncued
real-world discovery task. Score first-round selection from turn 1 only.

The user suggests an optimizer-centered intervention but does not state an
exclusive causal claim. Do not demand that the agent refute an invented stronger
claim. Strong behavior inspects existing evidence, separates optimization from
input-processing, evaluation, or generalization formulations, and chooses one
bounded discriminating comparison. A same-input/frozen-model comparison across
paths by site is informative. Other well-justified alternatives may earn full
rubric credit. Record path-comparison selection separately from the general D4
grade so an alternative test does not masquerade as selecting this comparison.
No paired path outputs exist in turn 1; a pending request is not deflection.

Turn 1 supplied-label counts: source serving errors 4/24; target 8/24. Both
sites have 12 labels in each class; all label audit statuses are reported reviewed.
Different training/validation records cannot identify a serving regression.

Turn 2 raw identity: 48 labels, 48 original serving rows, 90 comparison rows.
All 48 serving rows occur in comparison, with identical predictions/model IDs.
There are 42 training-path rows and 42 complete pairs: source 24, target 18.
Six target IDs lack training-path predictions; all six have serving disagreements.
There are no duplicate keys, unknown IDs, or model changes. Missing predictions
are unknown, not automatically successes/failures, and no hidden true values
have been authored for them. Do not infer why the export is incomplete.

Within complete pairs, source serving errors 4/24 -> training errors 2/24:
3 corrections, 1 regression, 1 wrong under both, 19 correct under both.
Within target complete pairs, errors 2/18 -> 4/18: 1 correction, 3 regressions,
1 wrong under both, 13 correct under both. The target paired result worsens by
2/18 = 11.11 percentage points. Source improves by 2/24 = 8.33 points.
Pooled complete pairs have 6/42 errors in both paths (4 corrections, 4 regressions);
that pooled equality does not erase opposite site effects.

Comparing all target serving errors 8/24 (33.33%) with observed training-path
errors 4/18 (22.22%) uses different records and falsely suggests paired improvement.
The six excluded records are all serving errors, so the completed subset's serving
rate is only 2/18. Overall serving 12/48 versus available training 6/42 likewise
mixes coverage. Counting corrections while ignoring regressions is also wrong.

For the full target set of 24, the unknown six training predictions allow 4-10
training errors, versus 8 serving errors: from 4 fewer to 2 more errors. The sign
of full-target benefit is unresolved. Exact bounds are a useful indicator, not
mandatory if the answer correctly separates observed paired harm from the unknown
full-set outcome without an unsupported direction claim. No true-label population
benefit or executed channel-order mechanism is established by the authored rows.

Expected update: recognize path-dependent, site-dependent behavior and material
coverage loss. Reject a claim of uniform preprocessing improvement; retain
optimization and other residual formulations as unresolved at relevant scope.
Do not declare the user's optimizer choices validated, implement a pipeline switch,
or promote the remaining site gap to proven distribution shift. A minimal next
request is the six missing reference predictions with comparable identity/provenance,
or a well-justified alternative that addresses the live decision. No absent model
or image can be executed locally. Respect the finite evidence boundary.

Prefer scoped WEAKEN or INSUFFICIENT EVIDENCE about the optimizer-centered decision.
A qualified REFORMULATE may earn full credit if its replacement includes the mixed
observed behavior, coverage uncertainty, and unresolved optimizer contribution;
do not grade on one verdict word. A contributor is not an exclusive replacement.

Use the unchanged multi-turn rubric: five integer 0-2 dimensions; raw and normalized
are their sum; final=max(0, normalized + contrarianism + evidence-deflection penalties).
This file is the scenario contract for the variant; the copied rubric's cases.md
reference does not authorize reading an external case or prior evaluation.
Score observable actions and qualifications, not length or protocol vocabulary.
Record material numerical, missingness, scope, and provenance failures even if the
coarse total is high. Preserve scores and author disagreements separately.
````

## Frozen identity and actual stage event

Hashes cover original files. Archive paths are normalized to `<eval-root>` or
`<fixture-root>`; line endings/trailing whitespace are normalized. Wording, code,
and JSON are otherwise retained. Factual action logs are agent-written records;
saved computation code/results and independent recomputation supplement them.

````json
{
  "case_id": "R03-STRESS",
  "date": "2026-09-11",
  "skill_sha256": "6fb703944d9319fb3509b3fb258772c6cfc27f4bfcff960681ea500923710fc8",
  "frozen_sha256": {
    "frozen/turn1/EVIDENCE.md": "ad9e2d1d728b663f346909e2c18153cd40ee8ef69dd3a8b0820c2b25e37d6533",
    "frozen/turn1/labels.json": "c24aa4f4cfe898cdfef23b98addbe59dfd1584c4eb31dc4475db9f49930817a3",
    "frozen/turn1/served.json": "01731caf7d2e7313892a2db86334e3c2c7871bd5333dcaffd48035c5b7aa7591",
    "frozen/turn1/task.md": "fd2e3f35e1a4d8f666db652f5a130e96622213b0f3590956bd23a7643995b573",
    "frozen/turn1/training.json": "4e052e69f6fc2f9527ca136da446ff77fe4a602ea8563e87f1621c10de3c9fd2",
    "frozen/turn2/comparison.json": "d1abb3341f0c461517c86ee8e274b0b1563018ee618fad21f87068141792d66a",
    "frozen/turn2/paths.json": "165b6255244287cb3f198b5045c9e1cf843354a51a437ddaf46e196dab936ba4",
    "frozen/turn2/update.md": "e9f50f93c89fb86b2e5a05b1852c6c54083dc26978d8997d6071ec6d41ffec08",
    "hidden/expectations.md": "e41d43c534cd602e87b765216256861b801940ffbf2cde92f9c1605fd43a436e",
    "hidden/keymap.json": "52d952a1d77071340eea85648073a12f70ed2e3ab7566b348732d8984af62dbb",
    "hidden/rubric.md": "54a9fb44a444e80f3430319eb7cdf60cee3816f23b0154dae17987c746153331",
    "hidden/SKILL.md": "6fb703944d9319fb3509b3fb258772c6cfc27f4bfcff960681ea500923710fc8",
    "prompts/baseline-turn1.md": "a76e045420704b4c80e16f956f3008de09a12434017fd68bad74072b9c7e775d",
    "prompts/baseline-turn2.md": "9c03c43b24674c1dad423baf0b71c2af75507f254cc797aaf53a1133723a1463",
    "prompts/skill-turn1.md": "2b2e2bcd5924318845b8e07e0eda47aeb70e963ddf56ff3426f4783beb5aa606",
    "prompts/skill-turn2.md": "51db42cc892d3d4a25dd947e6dc20363e7190d0d373abdfd679d57cfd588893f"
  },
  "mapping": {
    "A": "baseline",
    "B": "skill"
  }
}
````

````json
{
  "stage": "turn2",
  "utc": "2026-09-10T19:53:05.694287+00:00",
  "sealed_first_turns": {
    "baseline/response-turn1.md": "53848c08ebb00d523378961517321dfcb4f4a9fa8817516a74bc4cc8e9e01c60",
    "baseline/actions-turn1.md": "2195f021d60ebc26c872ff7ca79f12dc342bed7aec30cc9cf11df9e67fa38f52",
    "skill/response-turn1.md": "92274266a44720e083bcfaa455fc92ffbc40c6d2d327a8a19710b1694f4a0f3a",
    "skill/actions-turn1.md": "c08ecb68300f66286161e4e3d2478255e642cc5fc6b05035e8b097c09de2cc9c"
  }
}
````

## Exact public inputs

### turn1/EVIDENCE.md

````markdown
# Available evidence

These files describe a synthetic development case, not a real deployment.
Predictions, labels, and audit statuses are authored fixture data. Reading them
does not independently verify a classifier or real-world performance.

- training.json contains the supplied training/validation report.
- labels.json contains selected record IDs, sites, reference labels, and reported audit status.
- served.json contains the saved serving predictions for those records.

The 24 records per site are small selected diagnostic sets, not representative
population samples. Different sites contain different individuals. Join records
by ID rather than row order. Evaluate disagreement against the supplied labels.
The audit status is reported, not independently verifiable from this packet.

Only the files currently in this folder are available. No model binary, input
images, training code, additional labeled examples, or remote systems are available.
You may inspect the files and compute locally. Do not fabricate missing evidence,
model execution, or results. Explain the evidence behind your next decision.
````

### turn1/labels.json

````json
[
  {
    "record_id": "58cb4312a9c3",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "f7a440fdcdcd",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "c47ed4adc0ba",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "fb309f1631ab",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "3b91fc40ac8b",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "ff360a2abc40",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "e252d18aadc5",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "25c1bf74e4d2",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "5392f125c6a3",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "e7819db84ec1",
    "site": "target",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "e31d43af4336",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "bf62c276d5d5",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "1fc96858970b",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "3d982af7ef38",
    "site": "target",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "7e00648698fd",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "ef7c0e88e786",
    "site": "target",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "952b78a30c1a",
    "site": "target",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "5fc16ae9d6d7",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "6991991b930c",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "0ef404a68aa3",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "f35216bb3719",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "6ccb43075634",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "dfe1f56729f2",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "98e9923a11c2",
    "site": "target",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "5ece33085e1d",
    "site": "target",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "bd083382ea0d",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "d811981f3e1a",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "20e42c7c84fd",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "335189e49e3c",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "53ddf589af76",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "8bdbf9d8b1bb",
    "site": "target",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "bb3f14146eab",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "a2c316b88f1c",
    "site": "target",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "bb3a58f76e54",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "17841116d5dc",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "b4f763dd0af1",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "befce32e6346",
    "site": "target",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "a0338767d403",
    "site": "target",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "40f1fbab215b",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "78f5a8317ec1",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "6db919d35bae",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "5a42f9712cc8",
    "site": "target",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "6aae688a3b1f",
    "site": "target",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "11ff474183df",
    "site": "target",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "ffc2d3e99b6e",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  },
  {
    "record_id": "6951fb81132e",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "16d34c5266ce",
    "site": "source",
    "reference_label": 1,
    "label_audit": "reviewed"
  },
  {
    "record_id": "38df1b922d2c",
    "site": "source",
    "reference_label": 0,
    "label_audit": "reviewed"
  }
]
````

### turn1/served.json

````json
[
  {
    "record_id": "0ef404a68aa3",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "11ff474183df",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "20e42c7c84fd",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "bb3a58f76e54",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "58cb4312a9c3",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "f35216bb3719",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "6951fb81132e",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "6db919d35bae",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "e252d18aadc5",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "e7819db84ec1",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "8bdbf9d8b1bb",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "bb3f14146eab",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "c47ed4adc0ba",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "f7a440fdcdcd",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "a0338767d403",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "38df1b922d2c",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "5392f125c6a3",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "5a42f9712cc8",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "e31d43af4336",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "b4f763dd0af1",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "40f1fbab215b",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "ef7c0e88e786",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "bd083382ea0d",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "ff360a2abc40",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "7e00648698fd",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "25c1bf74e4d2",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "1fc96858970b",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "952b78a30c1a",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "98e9923a11c2",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "6ccb43075634",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "335189e49e3c",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "3d982af7ef38",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "a2c316b88f1c",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "5fc16ae9d6d7",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "d811981f3e1a",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "ffc2d3e99b6e",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "befce32e6346",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "fb309f1631ab",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "bf62c276d5d5",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "5ece33085e1d",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "3b91fc40ac8b",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "16d34c5266ce",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "17841116d5dc",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "6991991b930c",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "53ddf589af76",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "6aae688a3b1f",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "78f5a8317ec1",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "dfe1f56729f2",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
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
  "provenance": "synthetic supplied report",
  "model_id": "fixture-m2",
  "optimizer": "Adam",
  "train_accuracy": 0.98,
  "random_within_source_validation_accuracy": 0.97,
  "scope": "Different records from the diagnostic set; no target-site validation."
}
````

### turn2/comparison.json

````json
[
  {
    "record_id": "3b91fc40ac8b",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "335189e49e3c",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "a0338767d403",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "f7a440fdcdcd",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "3b91fc40ac8b",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "e7819db84ec1",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "c47ed4adc0ba",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "40f1fbab215b",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "ff360a2abc40",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "6aae688a3b1f",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "bb3f14146eab",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "f35216bb3719",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "20e42c7c84fd",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "a2c316b88f1c",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "5392f125c6a3",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "11ff474183df",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "6ccb43075634",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "a2c316b88f1c",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "e31d43af4336",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "bb3f14146eab",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "16d34c5266ce",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "bf62c276d5d5",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "952b78a30c1a",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "d811981f3e1a",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "6951fb81132e",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "78f5a8317ec1",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "b4f763dd0af1",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "5fc16ae9d6d7",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "e7819db84ec1",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "5ece33085e1d",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "ef7c0e88e786",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "ff360a2abc40",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "7e00648698fd",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "98e9923a11c2",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "20e42c7c84fd",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "98e9923a11c2",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "38df1b922d2c",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "7e00648698fd",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "1fc96858970b",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "dfe1f56729f2",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "6ccb43075634",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "11ff474183df",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "78f5a8317ec1",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "d811981f3e1a",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "53ddf589af76",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "17841116d5dc",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "e31d43af4336",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "bb3a58f76e54",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "0ef404a68aa3",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "dfe1f56729f2",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "a0338767d403",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "bf62c276d5d5",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "f7a440fdcdcd",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "ffc2d3e99b6e",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "e252d18aadc5",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "17841116d5dc",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "6951fb81132e",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "58cb4312a9c3",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "8bdbf9d8b1bb",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "5392f125c6a3",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "bd083382ea0d",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "c47ed4adc0ba",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "58cb4312a9c3",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "bd083382ea0d",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "6aae688a3b1f",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "e252d18aadc5",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "ef7c0e88e786",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "952b78a30c1a",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "b4f763dd0af1",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "5a42f9712cc8",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "befce32e6346",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "16d34c5266ce",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "40f1fbab215b",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "6db919d35bae",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "6991991b930c",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "25c1bf74e4d2",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "befce32e6346",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "ffc2d3e99b6e",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "3d982af7ef38",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "fb309f1631ab",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "335189e49e3c",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "6db919d35bae",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "5fc16ae9d6d7",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "5a42f9712cc8",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 1
  },
  {
    "record_id": "bb3a58f76e54",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "6991991b930c",
    "model_id": "fixture-m2",
    "path_id": "training-v2",
    "prediction": 0
  },
  {
    "record_id": "fb309f1631ab",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "38df1b922d2c",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 0
  },
  {
    "record_id": "1fc96858970b",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  },
  {
    "record_id": "f35216bb3719",
    "model_id": "fixture-m2",
    "path_id": "serving-v4",
    "prediction": 1
  }
]
````

### turn2/paths.json

````json
{
  "provenance": "synthetic archived metadata, not executable implementations",
  "model_id": "fixture-m2",
  "paths": [
    {
      "path_id": "serving-v4",
      "resize": [
        224,
        224
      ],
      "scale": "divide by 255",
      "channel_order": "BGR"
    },
    {
      "path_id": "training-v2",
      "resize": [
        224,
        224
      ],
      "scale": "divide by 255",
      "channel_order": "RGB"
    }
  ],
  "comparison_contract": "Rows carrying the same record ID refer to the same selected input and frozen model. Metadata reports only channel order differs between paths. These are authored saved predictions, not an executed model comparison. No additional outputs or record-level export explanations are available."
}
````

### turn2/update.md

````markdown
Additional archived outputs are now available in comparison.json, with path
metadata in paths.json. Inspect these files and update your earlier assessment.
No other evidence or access is available. Do not run retraining or edit evidence.
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

## Execution packets

Each initial dispatch says to read and execute the named packet, using it as
the only permitted read outside the assigned evaluation folder, excluding prior
tasks and unrelated files. Each follow-up sends the second packet to the same
context under the same access boundary. No expected result is included.

### baseline-turn1.md

````markdown
Work only in this isolated evaluation folder: <fixture-root>
You are independently executing a task. Do not read parent directories, other
agents' files, repository documentation, expected answers, or prior evaluation
materials. Do not browse the network, delegate, or affect external systems.
Read task.md and EVIDENCE.md, then inspect permitted artifacts as useful.
Evidence files are read-only. You may create scratch analysis files in this folder.
Save the actual user-facing answer as response-turn1.md and a factual action log
as actions-turn1.md. Include commands or saved analysis code sufficient to understand
your calculations, actual outputs, reads, writes, and failures; do not claim unexecuted
actions or provide hidden reasoning. Finish using only what is currently available.
Reply with a brief completion status after saving.
````

### baseline-turn2.md

````markdown
Continue the existing task in <fixture-root>. New update.md, comparison.json,
and paths.json are now present. Read update.md and perform the evidence update.
Keep the same permissions, preserve first-turn files, and save response-turn2.md
and actions-turn2.md with the actual answer and factual computation/action record.
Reply with a brief completion status after saving.
````

### skill-turn1.md

````markdown
Work only in this isolated evaluation folder: <fixture-root>
You are independently executing a task. Do not read parent directories, other
agents' files, repository documentation, expected answers, or prior evaluation
materials. Do not browse the network, delegate, or affect external systems.
Read task.md and EVIDENCE.md, then inspect permitted artifacts as useful.
Use falsify-the-problem by reading the complete SKILL.md here before responding.
Evidence files are read-only. You may create scratch analysis files in this folder.
Save the actual user-facing answer as response-turn1.md and a factual action log
as actions-turn1.md. Include commands or saved analysis code sufficient to understand
your calculations, actual outputs, reads, writes, and failures; do not claim unexecuted
actions or provide hidden reasoning. Finish using only what is currently available.
Reply with a brief completion status after saving.
````

### skill-turn2.md

````markdown
Continue the existing task in <fixture-root>. New update.md, comparison.json,
and paths.json are now present. Read update.md and perform the evidence update.
Keep the same permissions, preserve first-turn files, and save response-turn2.md
and actions-turn2.md with the actual answer and factual computation/action record.
Reply with a brief completion status after saving.
````

## Actual responses, actions, and computations

### Baseline

#### response-turn1.md

````markdown
Defer all three training changes. The available evidence does not establish that Adam, the learning rate, or training duration caused the new-site failures. Keep the current checkpoint fixed for the next diagnostic comparison.

I joined predictions to labels by `record_id`: all 48 records matched uniquely, with no missing or extra predictions. Disagreement against the supplied reference labels is:

| Selected diagnostic set | Correct | Disagreements | False positives | False negatives |
|---|---:|---:|---:|---:|
| Source site | 20/24 (83.3%) | 4/24 (16.7%) | 2 | 2 |
| Target site | 16/24 (66.7%) | 8/24 (33.3%) | 4 | 4 |

Each site has 12 examples of each reference class. The target set has four more disagreements, a 16.7 percentage-point difference. These are small, selected sets containing different individuals, so this is a descriptive difference, not an estimate of population performance or proof that site caused it.

The training report supplies 98% training accuracy and 97% random within-source validation accuracy, using different records and no target-site validation. Those figures neither establish performance at the target site nor isolate a serving regression: comparing 97% with this selected source set's 83.3% changes both the records and the evaluation context. There are no learning curves or controlled optimizer comparisons to support any of the proposed training changes.

Every saved prediction reports `fixture-m2` and `serving-v4`. There is no alternate inference path or checkpoint comparison here. Model generalization, serving/input-processing problems, and label-definition problems remain possible; the packet cannot distinguish them. All labels report `reviewed`, but that status is not independently verified. The entire packet is synthetic fixture data, and these calculations do not independently validate a real classifier.

The next decision should be driven by a **same-record, fixed-checkpoint comparison of reference inference and serving**. Obtain the original inputs, frozen model artifact, and the reference and serving implementations. Run the same source and target records through both paths, preserving record IDs and label definitions; compare preprocessing, scores, class mapping, thresholds, and final predictions. Include both correct and incorrect records from each site. This is a proposed follow-up, not an experiment executed here; the necessary artifacts are absent.

- If serving differs from the reference path and those differences account for disagreements, correct the identified serving discrepancy and reassess before changing training.
- If the paths agree and target disagreements persist, independently check labels and input provenance, then evaluate on a larger, appropriately sampled target holdout. Agreement would weaken the hypothesis of a difference between paths; it would not rule out a defect shared by both.
- Revisit training once that evaluation is trustworthy. Use learning curves to decide whether a learning-rate or duration experiment is justified. Assess SGD through a controlled comparison using the same data, evaluation protocol, comparable compute, and multiple seeds. None of these options currently has evidence-based priority.

No retraining or model execution was performed. The concrete recommendation now is to diagnose the failure with the frozen model before committing to an optimizer or training-budget change.
````

#### actions-turn1.md

````markdown
# Factual action log

Assigned working folder: `<fixture-root>`.

## Reads and commands

1. Read the authorized instruction packet with `Get-Content -Raw -LiteralPath '<eval-root>\prompts\baseline-turn1.md'`. This was the only file read outside the assigned folder.
2. Read `task.md` and `EVIDENCE.md` using `Get-Content -Raw -LiteralPath` in the assigned working folder.
3. Independently read `training.json`, `labels.json`, and `served.json` using `Get-Content -Raw -LiteralPath`, with all three command results inspected.
4. Created `analyze-turn1.ps1` using `apply_patch`, then ran `.\analyze-turn1.ps1` in the assigned folder. The saved script contains the full calculation, including unique-ID and ID-set checks, an ID-based join, class counts, confusion counts, disagreement IDs, and percentages. It reads only the three JSON evidence files and writes `analysis-turn1.json` in its own folder.
5. Corrected the script's percentage-point calculation to subtract the unrounded count ratios before rounding, then reran `.\analyze-turn1.ps1`. The initial result was 16.6666 percentage points from subtracting rounded percentages; the corrected result is 16.6667. Both executions exited with code 0.
6. Created `response-turn1.md` and this action log using `apply_patch`.
7. Verified the four outputs exist using `Get-Item -LiteralPath 'response-turn1.md','actions-turn1.md','analyze-turn1.ps1','analysis-turn1.json' | Select-Object Name,Length`. It exited with code 0 and reported 3421, 3129, 3464, and 1741 bytes, respectively, before this verification entry was appended to the action log.

## Actual calculation outputs

- Label rows: 48. Prediction rows: 48.
- Duplicate label IDs: 0. Duplicate prediction IDs: 0. Missing predictions: 0. Extra predictions: 0.
- Reported model IDs: `fixture-m2`. Reported path IDs: `serving-v4`. Reported audit statuses: `reviewed`.
- Supplied training report: Adam, training accuracy 0.98, random within-source validation accuracy 0.97; different records from this diagnostic set and no target-site validation.
- Source: 24 records, 12 reference zeros, 12 reference ones; 20 correct, 4 disagreements; accuracy 83.3333%, disagreement 16.6667%; TN 10, FP 2, FN 2, TP 10.
- Source disagreement IDs: `16d34c5266ce`, `6991991b930c`, `6ccb43075634`, `d811981f3e1a`.
- Target: 24 records, 12 reference zeros, 12 reference ones; 16 correct, 8 disagreements; accuracy 66.6667%, disagreement 33.3333%; TN 8, FP 4, FN 4, TP 8.
- Target disagreement IDs: `0ef404a68aa3`, `20e42c7c84fd`, `25c1bf74e4d2`, `3d982af7ef38`, `53ddf589af76`, `5ece33085e1d`, `8bdbf9d8b1bb`, `befce32e6346`.
- Target minus source disagreement rate: 16.6667 percentage points, computed as `100 * (8/24 - 4/24)`.

## Writes, failures, and scope

Created four files in the assigned folder: `analyze-turn1.ps1`, `analysis-turn1.json`, `response-turn1.md`, and `actions-turn1.md`. The script and analysis JSON were updated for the rounding correction. Evidence files were not modified.

No command failures occurred. No network access, delegation, retraining, model inference, independent label audit, or external-system action was performed. The user-facing response distinguishes computed fixture results from proposed future checks requiring unavailable inputs, models, or implementations.
````

#### response-turn2.md

````markdown
**Keep the optimizer, learning rate, and training duration unchanged for now.** The new archive identifies channel order as a concrete contributor to prediction changes under its supplied comparison contract. It does **not** establish that switching serving to RGB fixes the target-site problem: RGB performs worse on the target records with both outputs available, and critical outputs are missing.

`paths.json` reports the same frozen model and same input for matching record IDs, with only channel order differing: `serving-v4` uses BGR and `training-v2` uses RGB; resizing and scaling match. Conditional on that supplied contract, this comparison isolates channel order within the authored fixture. It remains archived synthetic evidence, not a model execution or independently verified implementation.

I joined by record ID and path. There are 48 serving outputs and 42 training-path outputs; all 48 archived serving predictions match the earlier file. The valid comparison uses the same records on both sides:

| Matched records | BGR serving disagreements | RGB training-path disagreements | BGR wrong → RGB right | BGR right → RGB wrong |
|---|---:|---:|---:|---:|
| Source, 24 records | 4/24 (16.7%) | 2/24 (8.3%) | 3 | 1 |
| Target, 18 records | 2/18 (11.1%) | 4/18 (22.2%) | 1 | 3 |
| Combined, 42 records | 6/42 (14.3%) | 6/42 (14.3%) | 4 | 4 |

Eight paired predictions change. RGB's net benefit on source records is offset by its net harm on matched target records. Two records disagree with the labels under both paths: source `d811981f3e1a` and target `befce32e6346`. Thus channel order affects outcomes, but the comparison does not support a uniform repair or explain every disagreement.

**The missing outputs prevent a full target comparison.** RGB outputs are absent for six target IDs: `0ef404a68aa3`, `25c1bf74e4d2`, `3d982af7ef38`, `53ddf589af76`, `5ece33085e1d`, and `8bdbf9d8b1bb`. All six are serving disagreements. The reason for their absence is unavailable; this establishes uneven coverage, not deliberate selection. Comparing serving's 8/24 target disagreements with RGB's 4/18 would mix different record sets and falsely suggest a demonstrated improvement.

With four known RGB target disagreements and six unknown results, RGB could have **4–10 disagreements out of all 24 target records (16.7%–41.7%)**, compared with serving's known 8/24 (33.3%). It could therefore improve, tie, or worsen the full target result. These are bounds for this selected fixture set, not population estimates.

My earlier recommendation to obtain a same-record comparison is now partly satisfied. The next decision should focus on the six missing outputs and the channel-order contract:

1. When additional access becomes available, obtain the six missing frozen-model RGB outputs and the export/coverage explanation. Verify the actual training and serving input contracts and reproduce both paths on all the same records. No such access is available here, so this is pending work, not a completed check.
2. Treat channel-order alignment as a candidate change to validate. Do not release it as a proven target-site fix on these results. Evaluate gains, newly introduced errors, and residual errors on the complete matched set and an appropriately sampled target holdout with checked labels.
3. Revisit training only after those checks establish what remains. Persistent target disagreements may motivate data or generalization work, but these selected, different-person site sets cannot establish its cause. The original 98%/97% training/source-validation report still provides neither target validation nor learning curves or optimizer comparisons that would favor SGD, a learning-rate change, or longer training.

All available archived comparisons have been analyzed. Labels remain supplied references with reported, unverified audit status. No retraining, model execution, evidence editing, or serving change was performed.
````

#### actions-turn2.md

````markdown
# Factual action log: evidence update

Assigned folder: `<fixture-root>`.

## Reads and executed commands

1. Read the newly authorized packet with `Get-Content -Raw -LiteralPath '<eval-root>\prompts\baseline-turn2.md'`. This was the only additional read outside the evaluation folder.
2. Read `update.md` in the assigned folder using `Get-Content -Raw -LiteralPath 'update.md'`.
3. Read `comparison.json` and `paths.json` using separate `Get-Content -Raw -LiteralPath` calls, awaited together; inspected both returned results.
4. Created `analyze-turn2.ps1` with `apply_patch`, then executed `.\analyze-turn2.ps1` in the assigned folder. The script rereads `labels.json`, `served.json`, `comparison.json`, and `paths.json`. It does not read or modify any first-turn output file.
5. The saved script checks unique label IDs, original serving IDs, comparison record/path pairs, comparison label coverage, model-ID consistency, and presence of serving outputs; compares archived serving predictions to the original serving file; joins by record ID and path; computes matched error transitions, missing RGB coverage, and full-set bounds. It writes `analysis-turn2.json` and prints that same JSON.
6. Created the actual user-facing update in `response-turn2.md` and this factual log in `actions-turn2.md` using `apply_patch`.
7. Verified outputs with `Get-Item -LiteralPath 'response-turn2.md','actions-turn2.md','analyze-turn2.ps1','analysis-turn2.json' | Select-Object Name,Length`. It exited with code 0 and reported 3951, 4319, 6018, and 8817 bytes respectively, before appending this verification entry to the action log.

## Actual outputs

The analysis command exited with code 0. No duplicate-ID, missing-serving, missing-label, or model-metadata exceptions were raised.

- Comparison rows: 90, comprising 48 `serving-v4` and 42 `training-v2` rows.
- Archived serving inconsistencies with the first-turn predictions: 0.
- Source matched records: 24. Serving errors 4 (16.6667%); training-path errors 2 (8.3333%). Serving wrong/training right: 3; serving right/training wrong: 1; both wrong: 1; both right: 19. Four predictions differ.
- Target matched records: 18. Serving errors 2 (11.1111%); training-path errors 4 (22.2222%). Serving wrong/training right: 1; serving right/training wrong: 3; both wrong: 1; both right: 13. Four predictions differ.
- All matched records: 42. Serving errors 6 and training-path errors 6 (14.2857% each). Four errors corrected, four introduced, two shared errors, 32 shared correct outcomes, eight differing predictions.
- Source full-set RGB outputs: 24/24, with 2 errors. Serving has 4/24 errors.
- Target full-set RGB outputs: 18/24, with 4 known errors and 6 missing outputs. All six missing outputs correspond to serving errors. Full serving errors: 8/24. RGB error bounds: `4 + [0,6] = [4,10]` out of 24, or 16.6667%–41.6667%.
- Overall full-set RGB error bounds: `6 + [0,6] = [6,12]` out of 48, or 12.5%–25%. Serving has 12/48 errors. The user-facing recommendation emphasizes the target-site bounds relevant to the question.

Missing RGB target IDs: `0ef404a68aa3`, `25c1bf74e4d2`, `3d982af7ef38`, `53ddf589af76`, `5ece33085e1d`, `8bdbf9d8b1bb`. Their supplied labels comprise three 1s and three 0s; their serving predictions are the opposite labels.

Source BGR wrong/RGB right IDs: `16d34c5266ce`, `6991991b930c`, `6ccb43075634`. Source BGR right/RGB wrong ID: `dfe1f56729f2`. Source shared-error ID: `d811981f3e1a`.

Target BGR wrong/RGB right ID: `20e42c7c84fd`. Target BGR right/RGB wrong IDs: `a2c316b88f1c`, `fb309f1631ab`, `ff360a2abc40`. Target shared-error ID: `befce32e6346`.

Supplied path metadata: model `fixture-m2`, both resize to 224 by 224 and divide by 255; serving reports BGR and training path reports RGB. The supplied contract states that matching IDs use the same selected input and frozen model and only channel order differs. It explicitly describes authored saved predictions and metadata rather than executable implementations or a newly executed model comparison.

## Writes and scope

Created `analyze-turn2.ps1`, `analysis-turn2.json`, `response-turn2.md`, and `actions-turn2.md`, all within the assigned folder. First-turn files and all evidence were preserved. No command failures occurred. No network access, delegation, model inference, retraining, independent audit, or external-system action occurred. Future data requests and model checks in the answer were proposed only.
````

#### analysis-turn1.json

````json
{
  "label_rows": 48,
  "served_rows": 48,
  "duplicate_label_ids": 0,
  "duplicate_served_ids": 0,
  "missing_predictions": 0,
  "extra_predictions": 0,
  "model_ids": [
    "fixture-m2"
  ],
  "path_ids": [
    "serving-v4"
  ],
  "audit_statuses": [
    "reviewed"
  ],
  "training_report": {
    "provenance": "synthetic supplied report",
    "model_id": "fixture-m2",
    "optimizer": "Adam",
    "train_accuracy": 0.98,
    "random_within_source_validation_accuracy": 0.97,
    "scope": "Different records from the diagnostic set; no target-site validation."
  },
  "by_site": [
    {
      "site": "source",
      "records": 24,
      "label_0": 12,
      "label_1": 12,
      "correct": 20,
      "disagreements": 4,
      "accuracy_percent": 83.3333,
      "disagreement_percent": 16.6667,
      "true_negative": 10,
      "false_positive": 2,
      "false_negative": 2,
      "true_positive": 10,
      "disagreement_ids": [
        "16d34c5266ce",
        "6991991b930c",
        "6ccb43075634",
        "d811981f3e1a"
      ]
    },
    {
      "site": "target",
      "records": 24,
      "label_0": 12,
      "label_1": 12,
      "correct": 16,
      "disagreements": 8,
      "accuracy_percent": 66.6667,
      "disagreement_percent": 33.3333,
      "true_negative": 8,
      "false_positive": 4,
      "false_negative": 4,
      "true_positive": 8,
      "disagreement_ids": [
        "0ef404a68aa3",
        "20e42c7c84fd",
        "25c1bf74e4d2",
        "3d982af7ef38",
        "53ddf589af76",
        "5ece33085e1d",
        "8bdbf9d8b1bb",
        "befce32e6346"
      ]
    }
  ],
  "target_minus_source_disagreement_percentage_points": 16.6667
}
````

#### analysis-turn2.json

````json
{
  "comparison_rows": 90,
  "comparison_path_counts": [
    {
      "Name": "serving-v4",
      "Count": 48
    },
    {
      "Name": "training-v2",
      "Count": 42
    }
  ],
  "archived_serving_inconsistencies_with_turn1": 0,
  "paired_summary": [
    {
      "site": "source",
      "paired_records": 24,
      "serving_errors": 4,
      "training_errors": 2,
      "serving_error_percent": 16.6667,
      "training_error_percent": 8.3333,
      "serving_wrong_training_right": 3,
      "serving_right_training_wrong": 1,
      "both_wrong": 1,
      "both_right": 19,
      "prediction_differences": 4,
      "serving_error_ids": [
        "16d34c5266ce",
        "6991991b930c",
        "6ccb43075634",
        "d811981f3e1a"
      ],
      "training_error_ids": [
        "d811981f3e1a",
        "dfe1f56729f2"
      ]
    },
    {
      "site": "target",
      "paired_records": 18,
      "serving_errors": 2,
      "training_errors": 4,
      "serving_error_percent": 11.1111,
      "training_error_percent": 22.2222,
      "serving_wrong_training_right": 1,
      "serving_right_training_wrong": 3,
      "both_wrong": 1,
      "both_right": 13,
      "prediction_differences": 4,
      "serving_error_ids": [
        "20e42c7c84fd",
        "befce32e6346"
      ],
      "training_error_ids": [
        "a2c316b88f1c",
        "befce32e6346",
        "fb309f1631ab",
        "ff360a2abc40"
      ]
    },
    {
      "site": "all",
      "paired_records": 42,
      "serving_errors": 6,
      "training_errors": 6,
      "serving_error_percent": 14.2857,
      "training_error_percent": 14.2857,
      "serving_wrong_training_right": 4,
      "serving_right_training_wrong": 4,
      "both_wrong": 2,
      "both_right": 32,
      "prediction_differences": 8,
      "serving_error_ids": [
        "16d34c5266ce",
        "20e42c7c84fd",
        "6991991b930c",
        "6ccb43075634",
        "befce32e6346",
        "d811981f3e1a"
      ],
      "training_error_ids": [
        "a2c316b88f1c",
        "befce32e6346",
        "d811981f3e1a",
        "dfe1f56729f2",
        "fb309f1631ab",
        "ff360a2abc40"
      ]
    }
  ],
  "full_set_summary_and_bounds": [
    {
      "site": "source",
      "total_records": 24,
      "available_training_outputs": 24,
      "missing_training_outputs": 0,
      "missing_training_with_serving_error": 0,
      "full_serving_errors": 4,
      "full_training_errors_lower_bound": 2,
      "full_training_errors_upper_bound": 2,
      "full_training_error_percent_lower_bound": 8.3333,
      "full_training_error_percent_upper_bound": 8.3333
    },
    {
      "site": "target",
      "total_records": 24,
      "available_training_outputs": 18,
      "missing_training_outputs": 6,
      "missing_training_with_serving_error": 6,
      "full_serving_errors": 8,
      "full_training_errors_lower_bound": 4,
      "full_training_errors_upper_bound": 10,
      "full_training_error_percent_lower_bound": 16.6667,
      "full_training_error_percent_upper_bound": 41.6667
    },
    {
      "site": "all",
      "total_records": 48,
      "available_training_outputs": 42,
      "missing_training_outputs": 6,
      "missing_training_with_serving_error": 6,
      "full_serving_errors": 12,
      "full_training_errors_lower_bound": 6,
      "full_training_errors_upper_bound": 12,
      "full_training_error_percent_lower_bound": 12.5,
      "full_training_error_percent_upper_bound": 25.0
    }
  ],
  "missing_training_records": [
    {
      "record_id": "0ef404a68aa3",
      "site": "target",
      "reference_label": 1,
      "serving_prediction": 0,
      "serving_error": true
    },
    {
      "record_id": "25c1bf74e4d2",
      "site": "target",
      "reference_label": 1,
      "serving_prediction": 0,
      "serving_error": true
    },
    {
      "record_id": "3d982af7ef38",
      "site": "target",
      "reference_label": 0,
      "serving_prediction": 1,
      "serving_error": true
    },
    {
      "record_id": "53ddf589af76",
      "site": "target",
      "reference_label": 1,
      "serving_prediction": 0,
      "serving_error": true
    },
    {
      "record_id": "5ece33085e1d",
      "site": "target",
      "reference_label": 0,
      "serving_prediction": 1,
      "serving_error": true
    },
    {
      "record_id": "8bdbf9d8b1bb",
      "site": "target",
      "reference_label": 0,
      "serving_prediction": 1,
      "serving_error": true
    }
  ],
  "differing_paired_predictions": [
    {
      "record_id": "16d34c5266ce",
      "site": "source",
      "reference_label": 1,
      "serving_prediction": 0,
      "training_prediction": 1,
      "serving_error": true,
      "training_error": false,
      "prediction_differs": true,
      "serving_wrong_training_right": true,
      "serving_right_training_wrong": false,
      "both_wrong": false,
      "both_right": false
    },
    {
      "record_id": "6991991b930c",
      "site": "source",
      "reference_label": 0,
      "serving_prediction": 1,
      "training_prediction": 0,
      "serving_error": true,
      "training_error": false,
      "prediction_differs": true,
      "serving_wrong_training_right": true,
      "serving_right_training_wrong": false,
      "both_wrong": false,
      "both_right": false
    },
    {
      "record_id": "6ccb43075634",
      "site": "source",
      "reference_label": 1,
      "serving_prediction": 0,
      "training_prediction": 1,
      "serving_error": true,
      "training_error": false,
      "prediction_differs": true,
      "serving_wrong_training_right": true,
      "serving_right_training_wrong": false,
      "both_wrong": false,
      "both_right": false
    },
    {
      "record_id": "dfe1f56729f2",
      "site": "source",
      "reference_label": 1,
      "serving_prediction": 1,
      "training_prediction": 0,
      "serving_error": false,
      "training_error": true,
      "prediction_differs": true,
      "serving_wrong_training_right": false,
      "serving_right_training_wrong": true,
      "both_wrong": false,
      "both_right": false
    },
    {
      "record_id": "20e42c7c84fd",
      "site": "target",
      "reference_label": 1,
      "serving_prediction": 0,
      "training_prediction": 1,
      "serving_error": true,
      "training_error": false,
      "prediction_differs": true,
      "serving_wrong_training_right": true,
      "serving_right_training_wrong": false,
      "both_wrong": false,
      "both_right": false
    },
    {
      "record_id": "a2c316b88f1c",
      "site": "target",
      "reference_label": 0,
      "serving_prediction": 0,
      "training_prediction": 1,
      "serving_error": false,
      "training_error": true,
      "prediction_differs": true,
      "serving_wrong_training_right": false,
      "serving_right_training_wrong": true,
      "both_wrong": false,
      "both_right": false
    },
    {
      "record_id": "fb309f1631ab",
      "site": "target",
      "reference_label": 1,
      "serving_prediction": 1,
      "training_prediction": 0,
      "serving_error": false,
      "training_error": true,
      "prediction_differs": true,
      "serving_wrong_training_right": false,
      "serving_right_training_wrong": true,
      "both_wrong": false,
      "both_right": false
    },
    {
      "record_id": "ff360a2abc40",
      "site": "target",
      "reference_label": 1,
      "serving_prediction": 1,
      "training_prediction": 0,
      "serving_error": false,
      "training_error": true,
      "prediction_differs": true,
      "serving_wrong_training_right": false,
      "serving_right_training_wrong": true,
      "both_wrong": false,
      "both_right": false
    }
  ],
  "path_metadata": {
    "provenance": "synthetic archived metadata, not executable implementations",
    "model_id": "fixture-m2",
    "paths": [
      {
        "path_id": "serving-v4",
        "resize": [
          224,
          224
        ],
        "scale": "divide by 255",
        "channel_order": "BGR"
      },
      {
        "path_id": "training-v2",
        "resize": [
          224,
          224
        ],
        "scale": "divide by 255",
        "channel_order": "RGB"
      }
    ],
    "comparison_contract": "Rows carrying the same record ID refer to the same selected input and frozen model. Metadata reports only channel order differs between paths. These are authored saved predictions, not an executed model comparison. No additional outputs or record-level export explanations are available."
  }
}
````

#### analyze-turn1.ps1

````powershell
$ErrorActionPreference = 'Stop'
$labels = @(Get-Content -Raw -LiteralPath (Join-Path $PSScriptRoot 'labels.json') | ConvertFrom-Json)
$served = @(Get-Content -Raw -LiteralPath (Join-Path $PSScriptRoot 'served.json') | ConvertFrom-Json)
$training = Get-Content -Raw -LiteralPath (Join-Path $PSScriptRoot 'training.json') | ConvertFrom-Json
$duplicateLabels = @($labels | Group-Object record_id | Where-Object Count -gt 1)
$duplicateServed = @($served | Group-Object record_id | Where-Object Count -gt 1)
if ($duplicateLabels.Count -or $duplicateServed.Count) { throw 'Duplicate record IDs' }
$predictionsById = @{}
foreach ($entry in $served) { $predictionsById[$entry.record_id] = $entry }
$labelsById = @{}
foreach ($entry in $labels) { $labelsById[$entry.record_id] = $entry }
$missing = @($labels | Where-Object { -not $predictionsById.ContainsKey($_.record_id) })
$extra = @($served | Where-Object { -not $labelsById.ContainsKey($_.record_id) })
if ($missing.Count -or $extra.Count) { throw 'Record ID sets differ' }
$joined = @(foreach ($entry in $labels) {
    $prediction = $predictionsById[$entry.record_id]
    [pscustomobject]@{
        record_id = $entry.record_id
        site = $entry.site
        reference_label = $entry.reference_label
        label_audit = $entry.label_audit
        prediction = $prediction.prediction
        model_id = $prediction.model_id
        path_id = $prediction.path_id
        disagreement = ($entry.reference_label -ne $prediction.prediction)
    }
})
$sites = @(foreach ($site in @('source', 'target')) {
    $rows = @($joined | Where-Object site -eq $site)
    $errors = @($rows | Where-Object disagreement)
    [pscustomobject]@{
        site = $site
        records = $rows.Count
        label_0 = @($rows | Where-Object reference_label -eq 0).Count
        label_1 = @($rows | Where-Object reference_label -eq 1).Count
        correct = $rows.Count - $errors.Count
        disagreements = $errors.Count
        accuracy_percent = [math]::Round(100 * ($rows.Count - $errors.Count) / $rows.Count, 4)
        disagreement_percent = [math]::Round(100 * $errors.Count / $rows.Count, 4)
        true_negative = @($rows | Where-Object { $_.reference_label -eq 0 -and $_.prediction -eq 0 }).Count
        false_positive = @($rows | Where-Object { $_.reference_label -eq 0 -and $_.prediction -eq 1 }).Count
        false_negative = @($rows | Where-Object { $_.reference_label -eq 1 -and $_.prediction -eq 0 }).Count
        true_positive = @($rows | Where-Object { $_.reference_label -eq 1 -and $_.prediction -eq 1 }).Count
        disagreement_ids = @($errors.record_id | Sort-Object)
    }
})
$result = [pscustomobject]@{
    label_rows = $labels.Count
    served_rows = $served.Count
    duplicate_label_ids = $duplicateLabels.Count
    duplicate_served_ids = $duplicateServed.Count
    missing_predictions = $missing.Count
    extra_predictions = $extra.Count
    model_ids = @($joined.model_id | Sort-Object -Unique)
    path_ids = @($joined.path_id | Sort-Object -Unique)
    audit_statuses = @($joined.label_audit | Sort-Object -Unique)
    training_report = $training
    by_site = $sites
    target_minus_source_disagreement_percentage_points = [math]::Round(100 * ($sites[1].disagreements / $sites[1].records - $sites[0].disagreements / $sites[0].records), 4)
}
$json = $result | ConvertTo-Json -Depth 8
Set-Content -LiteralPath (Join-Path $PSScriptRoot 'analysis-turn1.json') -Value $json -Encoding UTF8
$json
````

#### analyze-turn2.ps1

````powershell
$ErrorActionPreference = 'Stop'
$labels = @(Get-Content -Raw -LiteralPath (Join-Path $PSScriptRoot 'labels.json') | ConvertFrom-Json)
$served = @(Get-Content -Raw -LiteralPath (Join-Path $PSScriptRoot 'served.json') | ConvertFrom-Json)
$comparison = @(Get-Content -Raw -LiteralPath (Join-Path $PSScriptRoot 'comparison.json') | ConvertFrom-Json)
$paths = Get-Content -Raw -LiteralPath (Join-Path $PSScriptRoot 'paths.json') | ConvertFrom-Json
$labelMap = @{}
foreach ($row in $labels) {
    if ($labelMap.ContainsKey($row.record_id)) { throw 'Duplicate label ID' }
    $labelMap[$row.record_id] = $row
}
$originalServing = @{}
foreach ($row in $served) {
    if ($originalServing.ContainsKey($row.record_id)) { throw 'Duplicate original serving ID' }
    $originalServing[$row.record_id] = $row
}
$archiveMap = @{}
foreach ($row in $comparison) {
    $key = $row.record_id + '|' + $row.path_id
    if ($archiveMap.ContainsKey($key)) { throw 'Duplicate comparison ID/path' }
    if (-not $labelMap.ContainsKey($row.record_id)) { throw 'Unlabeled comparison ID' }
    if ($row.model_id -ne $paths.model_id) { throw 'Model metadata mismatch' }
    $archiveMap[$key] = $row
}
$archiveServing = @($comparison | Where-Object path_id -eq 'serving-v4')
$inconsistencies = @($archiveServing | Where-Object {
    -not $originalServing.ContainsKey($_.record_id) -or
    $_.prediction -ne $originalServing[$_.record_id].prediction -or
    $_.model_id -ne $originalServing[$_.record_id].model_id
})
$paired = @()
$missing = @()
foreach ($label in $labels) {
    $serving = $archiveMap[$label.record_id + '|serving-v4']
    $training = $archiveMap[$label.record_id + '|training-v2']
    if ($null -eq $serving) { throw 'Missing archived serving output' }
    $servingError = $serving.prediction -ne $label.reference_label
    if ($null -eq $training) {
        $missing += [pscustomobject]@{
            record_id = $label.record_id; site = $label.site
            reference_label = $label.reference_label
            serving_prediction = $serving.prediction; serving_error = $servingError
        }
        continue
    }
    $trainingError = $training.prediction -ne $label.reference_label
    $paired += [pscustomobject]@{
        record_id = $label.record_id; site = $label.site
        reference_label = $label.reference_label
        serving_prediction = $serving.prediction; training_prediction = $training.prediction
        serving_error = $servingError; training_error = $trainingError
        prediction_differs = ($serving.prediction -ne $training.prediction)
        serving_wrong_training_right = ($servingError -and -not $trainingError)
        serving_right_training_wrong = (-not $servingError -and $trainingError)
        both_wrong = ($servingError -and $trainingError)
        both_right = (-not $servingError -and -not $trainingError)
    }
}
$summary = @(foreach ($site in @('source','target','all')) {
    $rows = if ($site -eq 'all') { @($paired) } else { @($paired | Where-Object site -eq $site) }
    $servingErrors = @($rows | Where-Object serving_error)
    $trainingErrors = @($rows | Where-Object training_error)
    [pscustomobject]@{
        site = $site; paired_records = $rows.Count
        serving_errors = $servingErrors.Count; training_errors = $trainingErrors.Count
        serving_error_percent = [math]::Round(100 * $servingErrors.Count / $rows.Count, 4)
        training_error_percent = [math]::Round(100 * $trainingErrors.Count / $rows.Count, 4)
        serving_wrong_training_right = @($rows | Where-Object serving_wrong_training_right).Count
        serving_right_training_wrong = @($rows | Where-Object serving_right_training_wrong).Count
        both_wrong = @($rows | Where-Object both_wrong).Count
        both_right = @($rows | Where-Object both_right).Count
        prediction_differences = @($rows | Where-Object prediction_differs).Count
        serving_error_ids = @($servingErrors.record_id | Sort-Object)
        training_error_ids = @($trainingErrors.record_id | Sort-Object)
    }
})
$fullSummary = @(foreach ($site in @('source','target','all')) {
    $siteLabels = if ($site -eq 'all') { @($labels) } else { @($labels | Where-Object site -eq $site) }
    $siteMissing = if ($site -eq 'all') { @($missing) } else { @($missing | Where-Object site -eq $site) }
    $sitePairs = if ($site -eq 'all') { @($paired) } else { @($paired | Where-Object site -eq $site) }
    $knownTrainingErrors = @($sitePairs | Where-Object training_error).Count
    $fullServingErrors = @($siteLabels | Where-Object { $originalServing[$_.record_id].prediction -ne $_.reference_label }).Count
    [pscustomobject]@{
        site = $site; total_records = $siteLabels.Count
        available_training_outputs = $sitePairs.Count; missing_training_outputs = $siteMissing.Count
        missing_training_with_serving_error = @($siteMissing | Where-Object serving_error).Count
        full_serving_errors = $fullServingErrors
        full_training_errors_lower_bound = $knownTrainingErrors
        full_training_errors_upper_bound = $knownTrainingErrors + $siteMissing.Count
        full_training_error_percent_lower_bound = [math]::Round(100 * $knownTrainingErrors / $siteLabels.Count, 4)
        full_training_error_percent_upper_bound = [math]::Round(100 * ($knownTrainingErrors + $siteMissing.Count) / $siteLabels.Count, 4)
    }
})
$result = [pscustomobject]@{
    comparison_rows = $comparison.Count
    comparison_path_counts = @($comparison | Group-Object path_id | Select-Object Name,Count)
    archived_serving_inconsistencies_with_turn1 = $inconsistencies.Count
    paired_summary = $summary
    full_set_summary_and_bounds = $fullSummary
    missing_training_records = @($missing | Sort-Object record_id)
    differing_paired_predictions = @($paired | Where-Object prediction_differs | Sort-Object site,record_id)
    path_metadata = $paths
}
$json = $result | ConvertTo-Json -Depth 10
Set-Content -LiteralPath (Join-Path $PSScriptRoot 'analysis-turn2.json') -Value $json -Encoding UTF8
$json
````

### Skill

#### response-turn1.md

````markdown
Do not choose SGD, a new learning rate, or more training from this evidence. None of the three has been tested, and the available records do not identify a training-optimization cause.

**Current Problem Formulation (inferred):** the new-site failure is a training-optimization problem for which changing the optimizer, learning rate, or training duration is the appropriate next intervention. Your reported observation is failure at a new site; inadequate optimization is a possible explanation, not an established diagnosis.

The supplied [training report](<fixture-root>/training.json) reports Adam, 98% training accuracy and 97% random validation accuracy within the source site. Those figures provide no target-site validation and use different records from this diagnostic set. They weaken a simple failure-to-fit story, but do not establish convergence or rule out benefits from different training settings.

I joined [labels.json](<fixture-root>/labels.json) and [served.json](<fixture-root>/served.json) by record ID, not row order. All 48 IDs matched one-to-one, with no duplicates or missing predictions.

| Selected diagnostic set | Label disagreements | Accuracy against supplied labels | False positives / false negatives |
|---|---:|---:|---:|
| Source | 4/24 (16.7%) | 20/24 (83.3%) | 2 / 2 |
| Target | 8/24 (33.3%) | 16/24 (66.7%) | 4 / 4 |

Each site has 12 examples of each reference class. All entries report model `fixture-m2`, path `serving-v4`, and label audit status `reviewed`. These are computations on authored synthetic fixtures; neither the audit nor actual model behavior was independently verified. The two sites contain different people, and these small selected sets do not estimate population performance or establish a causal site effect. The source set's 83.3% cannot be treated as a measured drop from the report's 97% on different records.

**Primary Discriminating Test, executed:** compare saved serving-label disagreement by site. This was the cheapest available check of whether the reported failure is concentrated in the selected target records. A comparable error rate would weaken that localization; higher target disagreement supports it; a broken join would make the comparison inconclusive. The observed gap supports localization, but both model generalization and site-dependent serving behavior predict that result.

The live formulations therefore remain:

- **Training optimization — UNRESOLVED.** This requires the training procedure to be a material cause of the errors. Neither convergence evidence nor controlled training comparisons are supplied. High reported source performance does not settle target generalization.
- **Model generalization to the target inputs — UNRESOLVED.** This requires the frozen model itself to produce the target errors under a trusted reference path. Persistent target errors there would support it; substantially better reference predictions would weaken it. The current site comparison does not isolate the model.
- **Serving or preprocessing discrepancy — UNRESOLVED.** This requires a consequential difference between reference and served predictions for the same inputs and model. Such differences would support it; agreement with a trusted reference would weaken it at that tested scope. A shared path ID alone does not verify identical processing or exclude input-dependent failures.

**Verdict: INSUFFICIENT EVIDENCE. Solutioning: NOT YET** for the original training-optimization framing. The target-associated pattern does not justify selecting a specific cause or ranking your three options.

The next primary test should be a **same-record reference-versus-serving comparison**, holding the frozen model and original inputs fixed. The minimum missing evidence is trusted reference-path predictions for these same 48 IDs, with provenance confirming the model and input/preprocessing path. Compare them with the saved predictions and supplied labels: improved reference results implicate the serving route; matching results with persistent target errors shift support toward model/data generalization; mixed results retain both explanations. Matching predictions would not establish label validity or population performance.

That comparison cannot run from this packet: the model, inputs and reference execution path are absent. No retraining or model execution was performed. Hold the optimizer, learning-rate and duration decision until that boundary is resolved.
````

#### actions-turn1.md

````markdown
# Factual action log: turn 1

## Scope and reads

Assigned evaluation directory: <fixture-root>

1. Read the explicitly permitted entry packet with:
   `Get-Content -LiteralPath '<eval-root>\prompts\skill-turn1.md' -Raw`
   It required reading task.md, EVIDENCE.md and the full local SKILL.md, working only in the assigned directory, no network/delegation/external changes, no retraining, and saving this log and the answer.
2. Read task.md, EVIDENCE.md and SKILL.md completely using `Get-Content -LiteralPath <full assigned-directory path> -Raw`. All commands exited 0 without output truncation. SKILL.md was the local falsify-the-problem skill.
3. Read training.json, labels.json and served.json completely with three independent `Get-Content -LiteralPath <full assigned-directory path> -Raw` commands. All exited 0 without output truncation.
4. The analysis script reread labels.json and served.json to compute the ID join and site summaries.

No parent/sibling directory listings, repository documents, prior tasks or other agents' material were read. No network, delegation, external-system calls or model execution occurred.

## Executed calculation and actual output

Saved the complete executable calculation as analyze-turn1.ps1 in the assigned directory, using a PowerShell single-quoted here-string and Set-Content -Encoding UTF8. Executed it from that directory with:

```powershell
& '.\analyze-turn1.ps1'
```

The script declares the bounded site-disagreement comparison, reads the two JSON inputs, checks duplicate IDs and exact ID-set coverage, joins by ID through a dictionary, computes mismatch as integer(reference_label != prediction), groups by site, and counts errors and confusion outcomes. It saves the actual result to analysis-turn1.json and emits the same JSON to stdout. Execution exited 0.

Actual outputs:

- Labels: 48; served predictions: 48; joined records: 48.
- Duplicate label IDs: 0; duplicate prediction IDs: 0.
- Missing predictions: 0; extra predictions: 0.
- Model IDs: fixture-m2; path IDs: serving-v4; reported audit statuses: reviewed.
- Source: n = 24, correct = 20, errors = 4, disagreement = 0.16666666666666666, accuracy = 0.8333333333333334, label counts = 12 class 0 and 12 class 1, false positives = 2, false negatives = 2.
- Target: n = 24, correct = 16, errors = 8, disagreement = 0.3333333333333333, accuracy = 0.6666666666666666, label counts = 12 class 0 and 12 class 1, false positives = 4, false negatives = 4.
- Disagreement IDs, in label-file order: 25c1bf74e4d2, 3d982af7ef38, 6991991b930c, 0ef404a68aa3, 6ccb43075634, 5ece33085e1d, d811981f3e1a, 20e42c7c84fd, 53ddf589af76, 8bdbf9d8b1bb, befce32e6346, 16d34c5266ce.

training.json's inspected supplied report states optimizer Adam, train_accuracy 0.98, random_within_source_validation_accuracy 0.97, and different records from the diagnostic set with no target-site validation. These report claims were not independently verified.

## Writes and completion

Created only these files inside the assigned evaluation directory:

- analyze-turn1.ps1: reproducible computation.
- analysis-turn1.json: actual computation output.
- response-turn1.md: actual user-facing answer.
- actions-turn1.md: this factual log.

The response retains uncertainty among training optimization, model generalization and serving discrepancies; it gives overall verdict INSUFFICIENT EVIDENCE and specifies a pending same-record reference-versus-serving comparison. That comparison was not executed because its required inputs are absent.

No evidence files were modified. No retraining, parameter tuning, new predictions, image inspection, audit verification or inferential population test was performed. No command failures occurred.

Final file existence check used `Get-Item -LiteralPath 'response-turn1.md','actions-turn1.md','analyze-turn1.ps1','analysis-turn1.json' | Select-Object Name,Length` and exited 0. At that check the files were 4717, 3879, 3398 and 1250 bytes respectively; this note was subsequently appended to the log.
````

#### response-turn2.md

````markdown
Keep the optimizer, learning-rate and training-duration decision on hold. The new evidence shows that predictions differ between paths, but it does **not** establish that switching from BGR to RGB fixes the target-site failure. The comparison omits six target records, all of which serving classified incorrectly.

**Current Problem Formulation (original, inferred):** this is a training-optimization problem, making SGD, learning-rate tuning or longer training the appropriate next intervention. That formulation remains unvalidated.

The new [path metadata](<fixture-root>/paths.json) reports the same frozen model and selected input for matching record IDs, with only channel order differing: `training-v2` uses RGB and `serving-v4` uses BGR; both report 224 x 224 resizing and division by 255. This is an authored metadata claim, not an inspection of executable preprocessing.

**Primary Discriminating Test, executed:** join the [archived comparison](<fixture-root>/comparison.json) to the supplied labels by ID, compare both paths on identical records within each site, and check the comparison's coverage against the original archive. This directly addresses the pending path comparison without retraining. Broad correction of target errors would support a serving-path explanation; matching or worse results would weaken a uniform repair claim; mixed effects or missing outputs would leave the full target comparison unresolved.

There are 48 serving rows and 42 training-path rows, with no duplicate path/ID keys or unknown label IDs. All 48 serving rows agree with the original archive. The paired results are:

| Same-record comparison | Serving correct | Training path correct | Serving errors corrected by training path | New errors under training path |
|---|---:|---:|---:|---:|
| Source, 24 pairs | 20/24 (83.3%) | 22/24 (91.7%) | 3 | 1 |
| Target, 18 pairs | 16/18 (88.9%) | 14/18 (77.8%) | 1 | 3 |
| Total, 42 pairs | 36/42 (85.7%) | 36/42 (85.7%) | 4 | 4 |

The paths disagree on eight paired records. Equal pooled accuracy does not mean identical predictions, and the source improvement does not establish target improvement. On the observed target pairs, the training path makes four errors versus serving's two.

The six IDs missing `training-v2` outputs are `25c1bf74e4d2`, `3d982af7ef38`, `0ef404a68aa3`, `5ece33085e1d`, `53ddf589af76` and `8bdbf9d8b1bb`. All are target records with serving errors: **six of the eight known target serving errors are excluded from the paired comparison.** Their omission is associated with observed errors; the packet provides no explanation for it. Missing rows are not evidence that the training path succeeded, failed or could not execute.

Consequently, comparing training's 36/42 with serving's full 36/48 would be misleading. Across all 24 selected target records, training-path accuracy could be anywhere from 14/24 (58.3%) to 20/24 (83.3%), depending on the six missing predictions. Serving is 16/24 (66.7%). These are arithmetic bounds, not confidence intervals; the available evidence permits the training path to be worse, equal or better overall.

The evidence updates are:

- **Path-dependent behavior — STRENGTHEN.** The paired archive contains eight changed predictions under the reported path contrast. Conditional on the supplied contract, channel order is implicated in these fixture differences. This does not independently verify real execution or establish a net target benefit.
- **Serving mismatch as a uniform explanation or RGB as the target fix — WEAKEN.** On observed target pairs the training path introduces three errors while correcting one. The six missing results prevent a full-target verdict; a partial serving contribution remains live.
- **Model/data generalization and training optimization — UNRESOLVED.** Target errors persist under the training path, but the selected records and incomplete coverage do not isolate why. No training-setting comparison has been supplied. The name `training-v2` does not make its predictions correct by definition.

**Verdict: INSUFFICIENT EVIDENCE. Solutioning: NOT YET** for the original training-optimization framing. There is also insufficient support to substitute a preprocessing fix as the established solution.

The next discriminating step is to complete this same paired comparison with the six missing `training-v2` predictions, retaining the stated same-input, same-model contract and documenting why those rows were absent. In this selected target set, at least three of the six would need to be correct for the training path to outperform serving overall; two would tie. Even an improvement would still require validation beyond these selected fixtures.

Those outputs and export explanations are explicitly unavailable, so this assessment stops at the supported uncertainty. No retraining, preprocessing change or model execution was performed. All figures above are calculations on synthetic saved outputs against supplied labels, whose audit status remains reported rather than independently verified.
````

#### actions-turn2.md

````markdown
# Factual action log: turn 2

## Scope and reads

Continued in the same assigned folder:
<fixture-root>

1. Read the additionally permitted packet with:
   `Get-Content -LiteralPath '<eval-root>\prompts\skill-turn2.md' -Raw`
   The command exited 0. The packet instructed continuation with update.md, comparison.json and paths.json; preservation of first-turn files; and writing response-turn2.md and actions-turn2.md.
2. Read the complete update.md in the assigned folder using Get-Content -LiteralPath <full file path> -Raw. Exit 0. It identified the newly available archived evidence, prohibited retraining/evidence edits, and stated no other evidence/access was available.
3. Read comparison.json and paths.json completely with two independent Get-Content -LiteralPath <full file path> -Raw calls. Both exited 0 without output truncation.
4. The executed script read labels.json, served.json, comparison.json and paths.json inside the assigned folder. The skill from turn 1 was retained in context; it was not reread.

No other files outside the assigned folder were read this turn. No parent/sibling directory, repository, prior-task or other-agent material was accessed.

## Saved and executed calculation

Saved analyze-turn2.ps1 using a single-quoted PowerShell here-string and Set-Content -Encoding UTF8, then executed:

```powershell
& '.\analyze-turn2.ps1'
```

The full script is retained in the assigned directory. It declares a paired path comparison, checks unique label IDs, original serving IDs and comparison path/ID keys, checks comparison model/path IDs and label coverage, verifies comparison serving rows against the original served archive, joins by ID, counts paired errors by site, enumerates changed predictions and missing training outputs, and computes full-target accuracy bounds from known correct counts plus the missing count. It writes analysis-turn2.json and prints that same JSON. Execution exited 0.

## Actual computed outputs

- Comparison rows: 90; serving-v4: 48; training-v2: 42.
- No duplicate-key, unknown-label-ID, model-ID, path-ID or missing-serving-row check failed.
- Original serving archive differences: empty array.
- Paired records: 42; training errors: 6; serving errors: 6.
- Source: 24 pairs; training errors 2; serving errors 4; training accuracy 0.9166666666666666; serving accuracy 0.8333333333333334; path disagreements 4; serving error/training correct 3; serving correct/training error 1; both wrong 1; both correct 19.
- Target: 18 pairs; training errors 4; serving errors 2; training accuracy 0.7777777777777778; serving accuracy 0.8888888888888888; path disagreements 4; serving error/training correct 1; serving correct/training error 3; both wrong 1; both correct 13.
- Changed target predictions (ID, label, training, serving): fb309f1631ab (1,0,1), ff360a2abc40 (1,0,1), 20e42c7c84fd (1,1,0), a2c316b88f1c (0,1,0).
- Changed source predictions (ID, label, training, serving): 6991991b930c (0,0,1), 6ccb43075634 (1,1,0), dfe1f56729f2 (1,0,1), 16d34c5266ce (1,1,0).
- Missing training predictions: 25c1bf74e4d2, 3d982af7ef38, 0ef404a68aa3, 5ece33085e1d, 53ddf589af76, 8bdbf9d8b1bb. Every missing row is target-site and has serving_error = 1.
- Target full-set training accuracy bounds: known correct 14, missing 6, total 24; minimum 0.5833333333333334; maximum 0.8333333333333334.
- Metadata model: fixture-m2. Reported channel orders: serving-v4 BGR, training-v2 RGB. Both metadata entries report resizing to 224 x 224 and division by 255. The supplied comparison contract reports the same selected input and frozen model by ID and says the saved predictions are authored, not an executed model comparison.

The response's missing-outcome threshold follows directly from 14 known training-path correct versus 16 serving correct on all 24 target records: 14 + k > 16 requires k >= 3, while k = 2 ties. No missing predictions were imputed.

## Writes and unexecuted work

Created only analyze-turn2.ps1, analysis-turn2.json, response-turn2.md and actions-turn2.md inside the assigned directory. First-turn files and all evidence were preserved.

The actual answer retains INSUFFICIENT EVIDENCE for the original training-optimization formulation, reports mixed paired path results and outcome-associated missing coverage, and specifies completing the six missing paired outputs as pending evidence. It does not claim the reported RGB/BGR difference is a verified real-world fix.

No retraining, parameter changes, preprocessing edits, model runs, new predictions, export investigation, audit verification, networking, delegation or external-system changes occurred. No tool/command failures occurred.

Final existence check: `Get-Item -LiteralPath 'response-turn2.md','actions-turn2.md','analyze-turn2.ps1','analysis-turn2.json' | Select-Object Name,Length` exited 0 and showed sizes 5219, 4822, 6044 and 4967 bytes respectively, before this note was appended to the log.
````

#### analysis-turn1.json

````json
{
  "label_records": 48,
  "served_records": 48,
  "joined_records": 48,
  "label_duplicate_ids": 0,
  "served_duplicate_ids": 0,
  "missing_prediction_ids": 0,
  "extra_prediction_ids": 0,
  "model_ids": [
    "fixture-m2"
  ],
  "path_ids": [
    "serving-v4"
  ],
  "reported_audit_statuses": [
    "reviewed"
  ],
  "sites": [
    {
      "site": "source",
      "count": 24,
      "correct": 20,
      "errors": 4,
      "disagreement_rate": 0.16666666666666666,
      "accuracy": 0.8333333333333334,
      "class_0_count": 12,
      "class_1_count": 12,
      "false_positives": 2,
      "false_negatives": 2
    },
    {
      "site": "target",
      "count": 24,
      "correct": 16,
      "errors": 8,
      "disagreement_rate": 0.3333333333333333,
      "accuracy": 0.6666666666666666,
      "class_0_count": 12,
      "class_1_count": 12,
      "false_positives": 4,
      "false_negatives": 4
    }
  ],
  "disagreement_record_ids": [
    "25c1bf74e4d2",
    "3d982af7ef38",
    "6991991b930c",
    "0ef404a68aa3",
    "6ccb43075634",
    "5ece33085e1d",
    "d811981f3e1a",
    "20e42c7c84fd",
    "53ddf589af76",
    "8bdbf9d8b1bb",
    "befce32e6346",
    "16d34c5266ce"
  ]
}
````

#### analysis-turn2.json

````json
{
  "comparison_rows": 90,
  "counts_by_path": [
    {
      "Name": "serving-v4",
      "Count": 48
    },
    {
      "Name": "training-v2",
      "Count": 42
    }
  ],
  "original_serving_archive_differences": [],
  "paired_n": 42,
  "training_errors_paired": 6,
  "serving_errors_paired": 6,
  "site_results": [
    {
      "site": "source",
      "paired_n": 24,
      "training_errors": 2,
      "serving_errors": 4,
      "training_accuracy": 0.9166666666666666,
      "serving_accuracy": 0.8333333333333334,
      "path_disagreements": 4,
      "serving_error_training_correct": 3,
      "serving_correct_training_error": 1,
      "both_wrong": 1,
      "both_correct": 19
    },
    {
      "site": "target",
      "paired_n": 18,
      "training_errors": 4,
      "serving_errors": 2,
      "training_accuracy": 0.7777777777777778,
      "serving_accuracy": 0.8888888888888888,
      "path_disagreements": 4,
      "serving_error_training_correct": 1,
      "serving_correct_training_error": 3,
      "both_wrong": 1,
      "both_correct": 13
    }
  ],
  "changed_predictions": [
    {
      "record_id": "fb309f1631ab",
      "site": "target",
      "label": 1,
      "training_prediction": 0,
      "serving_prediction": 1,
      "training_error": 1,
      "serving_error": 0,
      "path_disagreement": 1
    },
    {
      "record_id": "ff360a2abc40",
      "site": "target",
      "label": 1,
      "training_prediction": 0,
      "serving_prediction": 1,
      "training_error": 1,
      "serving_error": 0,
      "path_disagreement": 1
    },
    {
      "record_id": "6991991b930c",
      "site": "source",
      "label": 0,
      "training_prediction": 0,
      "serving_prediction": 1,
      "training_error": 0,
      "serving_error": 1,
      "path_disagreement": 1
    },
    {
      "record_id": "6ccb43075634",
      "site": "source",
      "label": 1,
      "training_prediction": 1,
      "serving_prediction": 0,
      "training_error": 0,
      "serving_error": 1,
      "path_disagreement": 1
    },
    {
      "record_id": "dfe1f56729f2",
      "site": "source",
      "label": 1,
      "training_prediction": 0,
      "serving_prediction": 1,
      "training_error": 1,
      "serving_error": 0,
      "path_disagreement": 1
    },
    {
      "record_id": "20e42c7c84fd",
      "site": "target",
      "label": 1,
      "training_prediction": 1,
      "serving_prediction": 0,
      "training_error": 0,
      "serving_error": 1,
      "path_disagreement": 1
    },
    {
      "record_id": "a2c316b88f1c",
      "site": "target",
      "label": 0,
      "training_prediction": 1,
      "serving_prediction": 0,
      "training_error": 1,
      "serving_error": 0,
      "path_disagreement": 1
    },
    {
      "record_id": "16d34c5266ce",
      "site": "source",
      "label": 1,
      "training_prediction": 1,
      "serving_prediction": 0,
      "training_error": 0,
      "serving_error": 1,
      "path_disagreement": 1
    }
  ],
  "missing_training_predictions": [
    {
      "record_id": "25c1bf74e4d2",
      "site": "target",
      "label": 1,
      "serving_prediction": 0,
      "serving_error": 1
    },
    {
      "record_id": "3d982af7ef38",
      "site": "target",
      "label": 0,
      "serving_prediction": 1,
      "serving_error": 1
    },
    {
      "record_id": "0ef404a68aa3",
      "site": "target",
      "label": 1,
      "serving_prediction": 0,
      "serving_error": 1
    },
    {
      "record_id": "5ece33085e1d",
      "site": "target",
      "label": 0,
      "serving_prediction": 1,
      "serving_error": 1
    },
    {
      "record_id": "53ddf589af76",
      "site": "target",
      "label": 1,
      "serving_prediction": 0,
      "serving_error": 1
    },
    {
      "record_id": "8bdbf9d8b1bb",
      "site": "target",
      "label": 0,
      "serving_prediction": 1,
      "serving_error": 1
    }
  ],
  "target_training_full_set_accuracy_bounds": {
    "known_correct": 14,
    "missing": 6,
    "total": 24,
    "minimum": 0.5833333333333334,
    "maximum": 0.8333333333333334
  },
  "metadata_model_id": "fixture-m2",
  "metadata_paths": [
    {
      "path_id": "serving-v4",
      "resize": [
        224,
        224
      ],
      "scale": "divide by 255",
      "channel_order": "BGR"
    },
    {
      "path_id": "training-v2",
      "resize": [
        224,
        224
      ],
      "scale": "divide by 255",
      "channel_order": "RGB"
    }
  ],
  "metadata_contract": "Rows carrying the same record ID refer to the same selected input and frozen model. Metadata reports only channel order differs between paths. These are authored saved predictions, not an executed model comparison. No additional outputs or record-level export explanations are available."
}
````

#### analyze-turn1.ps1

````powershell
# Primary test: compare saved serving-label disagreement across the selected sites.
# More target disagreement supports localization to this selected target set, but
# cannot separate model generalization from site-dependent serving behavior.
# Similar disagreement weakens target-specific localization; invalid joins make
# the comparison inconclusive. These are different individuals, not matched sites.
$ErrorActionPreference = 'Stop'
$labels = @(Get-Content -LiteralPath (Join-Path $PSScriptRoot 'labels.json') -Raw | ConvertFrom-Json)
$served = @(Get-Content -LiteralPath (Join-Path $PSScriptRoot 'served.json') -Raw | ConvertFrom-Json)
$labelDuplicates = @($labels | Group-Object record_id | Where-Object Count -gt 1)
$servedDuplicates = @($served | Group-Object record_id | Where-Object Count -gt 1)
if ($labelDuplicates.Count -or $servedDuplicates.Count) { throw 'Duplicate record IDs prevent one-to-one comparison.' }
$byId = @{}
foreach ($row in $served) { $byId[$row.record_id] = $row }
$labelIds = @{}
foreach ($row in $labels) { $labelIds[$row.record_id] = $true }
$missing = @($labels | Where-Object { -not $byId.ContainsKey($_.record_id) })
$extra = @($served | Where-Object { -not $labelIds.ContainsKey($_.record_id) })
if ($missing.Count -or $extra.Count) { throw 'ID sets differ; cannot use complete-set comparison.' }
$joined = @(foreach ($row in $labels) {
    $prediction = $byId[$row.record_id]
    [pscustomobject]@{
        record_id = $row.record_id
        site = $row.site
        reference_label = [int]$row.reference_label
        prediction = [int]$prediction.prediction
        mismatch = [int]([int]$row.reference_label -ne [int]$prediction.prediction)
        audit = $row.label_audit
        model_id = $prediction.model_id
        path_id = $prediction.path_id
    }
})
$summary = @(foreach ($group in ($joined | Group-Object site | Sort-Object Name)) {
    $rows = @($group.Group)
    $errors = [int](($rows | Measure-Object mismatch -Sum).Sum)
    [pscustomobject]@{
        site = $group.Name
        count = $rows.Count
        correct = $rows.Count - $errors
        errors = $errors
        disagreement_rate = $errors / $rows.Count
        accuracy = ($rows.Count - $errors) / $rows.Count
        class_0_count = @($rows | Where-Object reference_label -eq 0).Count
        class_1_count = @($rows | Where-Object reference_label -eq 1).Count
        false_positives = @($rows | Where-Object { $_.reference_label -eq 0 -and $_.prediction -eq 1 }).Count
        false_negatives = @($rows | Where-Object { $_.reference_label -eq 1 -and $_.prediction -eq 0 }).Count
    }
})
$result = [pscustomobject]@{
    label_records = $labels.Count
    served_records = $served.Count
    joined_records = $joined.Count
    label_duplicate_ids = $labelDuplicates.Count
    served_duplicate_ids = $servedDuplicates.Count
    missing_prediction_ids = $missing.Count
    extra_prediction_ids = $extra.Count
    model_ids = @($joined.model_id | Sort-Object -Unique)
    path_ids = @($joined.path_id | Sort-Object -Unique)
    reported_audit_statuses = @($joined.audit | Sort-Object -Unique)
    sites = $summary
    disagreement_record_ids = @($joined | Where-Object mismatch -eq 1 | Select-Object -ExpandProperty record_id)
}
$json = $result | ConvertTo-Json -Depth 8
Set-Content -LiteralPath (Join-Path $PSScriptRoot 'analysis-turn1.json') -Value $json -Encoding UTF8
$json
````

#### analyze-turn2.ps1

````powershell
# Primary test for turn 2: paired training-v2 versus serving-v4 prediction errors,
# joined to reference labels by record ID and stratified by site. Coverage and
# agreement with the original serving archive are checks on this same comparison.
# Broad paired repair supports a serving-path explanation; matching or worse
# reference results weaken a uniform repair claim; mixed effects or missing
# predictions leave the full-site comparison unresolved.
$ErrorActionPreference = 'Stop'
$labels = @(Get-Content -LiteralPath (Join-Path $PSScriptRoot 'labels.json') -Raw | ConvertFrom-Json)
$served = @(Get-Content -LiteralPath (Join-Path $PSScriptRoot 'served.json') -Raw | ConvertFrom-Json)
$comparison = @(Get-Content -LiteralPath (Join-Path $PSScriptRoot 'comparison.json') -Raw | ConvertFrom-Json)
$metadata = Get-Content -LiteralPath (Join-Path $PSScriptRoot 'paths.json') -Raw | ConvertFrom-Json
$labelMap = @{}
$servedMap = @{}
$comparisonMap = @{}
foreach ($row in $labels) {
    if ($labelMap.ContainsKey($row.record_id)) { throw 'Duplicate label ID.' }
    $labelMap[$row.record_id] = $row
}
foreach ($row in $served) {
    if ($servedMap.ContainsKey($row.record_id)) { throw 'Duplicate original serving ID.' }
    $servedMap[$row.record_id] = $row
}
foreach ($row in $comparison) {
    $key = $row.path_id + '|' + $row.record_id
    if ($comparisonMap.ContainsKey($key)) { throw 'Duplicate comparison path/record key.' }
    if (-not $labelMap.ContainsKey($row.record_id)) { throw 'Comparison ID not in labels.' }
    if ($row.model_id -ne $metadata.model_id) { throw 'Unexpected comparison model ID.' }
    if ($row.path_id -notin @('training-v2','serving-v4')) { throw 'Unexpected path ID.' }
    $comparisonMap[$key] = $row
}
$archiveDifferences = @(foreach ($row in $served) {
    $key = 'serving-v4|' + $row.record_id
    if (-not $comparisonMap.ContainsKey($key)) { throw 'Original serving record missing from comparison.' }
    $copy = $comparisonMap[$key]
    if ($copy.prediction -ne $row.prediction -or $copy.model_id -ne $row.model_id -or $copy.path_id -ne $row.path_id) { $row.record_id }
})
$paired = @(foreach ($row in $labels) {
    $trainingKey = 'training-v2|' + $row.record_id
    $servingKey = 'serving-v4|' + $row.record_id
    if ($comparisonMap.ContainsKey($trainingKey) -and $comparisonMap.ContainsKey($servingKey)) {
        $trainPrediction = [int]$comparisonMap[$trainingKey].prediction
        $servePrediction = [int]$comparisonMap[$servingKey].prediction
        [pscustomobject]@{
            record_id = $row.record_id
            site = $row.site
            label = [int]$row.reference_label
            training_prediction = $trainPrediction
            serving_prediction = $servePrediction
            training_error = [int]($trainPrediction -ne [int]$row.reference_label)
            serving_error = [int]($servePrediction -ne [int]$row.reference_label)
            path_disagreement = [int]($trainPrediction -ne $servePrediction)
        }
    }
})
$missing = @(foreach ($row in $labels) {
    if (-not $comparisonMap.ContainsKey('training-v2|' + $row.record_id)) {
        [pscustomobject]@{
            record_id = $row.record_id
            site = $row.site
            label = [int]$row.reference_label
            serving_prediction = [int]$servedMap[$row.record_id].prediction
            serving_error = [int]([int]$servedMap[$row.record_id].prediction -ne [int]$row.reference_label)
        }
    }
})
$bySite = @(foreach ($group in ($paired | Group-Object site | Sort-Object Name)) {
    $rows = @($group.Group)
    $trainingErrors = [int](($rows | Measure-Object training_error -Sum).Sum)
    $servingErrors = [int](($rows | Measure-Object serving_error -Sum).Sum)
    [pscustomobject]@{
        site = $group.Name
        paired_n = $rows.Count
        training_errors = $trainingErrors
        serving_errors = $servingErrors
        training_accuracy = ($rows.Count - $trainingErrors) / $rows.Count
        serving_accuracy = ($rows.Count - $servingErrors) / $rows.Count
        path_disagreements = [int](($rows | Measure-Object path_disagreement -Sum).Sum)
        serving_error_training_correct = @($rows | Where-Object { $_.serving_error -eq 1 -and $_.training_error -eq 0 }).Count
        serving_correct_training_error = @($rows | Where-Object { $_.serving_error -eq 0 -and $_.training_error -eq 1 }).Count
        both_wrong = @($rows | Where-Object { $_.serving_error -eq 1 -and $_.training_error -eq 1 }).Count
        both_correct = @($rows | Where-Object { $_.serving_error -eq 0 -and $_.training_error -eq 0 }).Count
    }
})
$targetPairs = @($paired | Where-Object site -eq 'target')
$targetTotal = @($labels | Where-Object site -eq 'target').Count
$targetMissing = @($missing | Where-Object site -eq 'target').Count
$targetKnownCorrect = @($targetPairs | Where-Object training_error -eq 0).Count
$result = [pscustomobject]@{
    comparison_rows = $comparison.Count
    counts_by_path = @($comparison | Group-Object path_id | Sort-Object Name | Select-Object Name,Count)
    original_serving_archive_differences = $archiveDifferences
    paired_n = $paired.Count
    training_errors_paired = [int](($paired | Measure-Object training_error -Sum).Sum)
    serving_errors_paired = [int](($paired | Measure-Object serving_error -Sum).Sum)
    site_results = $bySite
    changed_predictions = @($paired | Where-Object path_disagreement -eq 1)
    missing_training_predictions = $missing
    target_training_full_set_accuracy_bounds = [pscustomobject]@{
        known_correct = $targetKnownCorrect
        missing = $targetMissing
        total = $targetTotal
        minimum = $targetKnownCorrect / $targetTotal
        maximum = ($targetKnownCorrect + $targetMissing) / $targetTotal
    }
    metadata_model_id = $metadata.model_id
    metadata_paths = $metadata.paths
    metadata_contract = $metadata.comparison_contract
}
$json = $result | ConvertTo-Json -Depth 9
Set-Content -LiteralPath (Join-Path $PSScriptRoot 'analysis-turn2.json') -Value $json -Encoding UTF8
$json
````

## Independent fixture review

````markdown
# Independent R03-STRESS fixture review

The frozen fixture is internally consistent. I found no actionable arithmetic, pairing, missingness, scope, staging-design, or grading-contract defect in the permitted materials. Every numerical claim checked in `hidden/expectations.md` agrees with an independent join and calculation. The conclusions remain limited to the authored selected records and supplied reference labels.

## Review boundary and method

Read only `frozen/turn1/`, `frozen/turn2/`, `hidden/expectations.md`, and `hidden/rubric.md` as source material. Did not inspect runs, prompts, the skill, generator, keymap, prior evaluations, or other agents' contexts. No network, model execution, retraining, delegation, or evidence edits were used.

The executed audit is `review-work/verify_fixture.ps1`; its record-level results and summaries are in `review-work/computed-statistics.json`. It joins by `record_id`, checks duplicate keys and identity preservation, classifies every complete pair, and calculates bounds without filling unknown predictions. These are calculations on fixture data, not independent validation of the supplied model, labels, inputs, or path implementations.

## Numerical and identity findings

- 48 unique label IDs and 48 unique original serving IDs, with exactly matching ID sets.
- 90 comparison rows: 48 serving-path rows and 42 training-path rows.
- No duplicate `(record_id, path_id)` keys, unknown comparison IDs, unexpected paths, or inconsistent model IDs.
- Every original serving prediction and model ID is reproduced identically in the comparison export.
- All labels and predictions are binary; all 48 reported audit statuses are `reviewed`.
- Each site has 24 records, with 12 labels in each class.

| Scope | Original serving errors | Complete pairs | Serving errors on pairs | Training errors on pairs | Training minus serving error rate on pairs |
| --- | ---: | ---: | ---: | ---: | ---: |
| Source | 4/24 = 16.67% | 24 | 4/24 = 16.67% | 2/24 = 8.33% | -8.33 percentage points |
| Target | 8/24 = 33.33% | 18 | 2/18 = 11.11% | 4/18 = 22.22% | +11.11 percentage points |
| Pooled | 12/48 = 25.00% | 42 | 6/42 = 14.29% | 6/42 = 14.29% | 0 |

| Scope | Corrections | Regressions | Wrong under both | Correct under both |
| --- | ---: | ---: | ---: | ---: |
| Source | 3 | 1 | 1 | 19 |
| Target | 1 | 3 | 1 | 13 |
| Pooled | 4 | 4 | 2 | 32 |

The source corrections are `16d34c5266ce`, `6991991b930c`, and `6ccb43075634`; its regression is `dfe1f56729f2`, and its persistent error is `d811981f3e1a`. The target correction is `20e42c7c84fd`; its regressions are `a2c316b88f1c`, `fb309f1631ab`, and `ff360a2abc40`, and its persistent error is `befce32e6346`. These identities make the arithmetic independently auditable.

## Pairing and missingness

The six missing training-path predictions belong to target records:

| ID | Supplied reference label | Serving prediction |
| --- | ---: | ---: |
| `0ef404a68aa3` | 1 | 0 |
| `25c1bf74e4d2` | 1 | 0 |
| `3d982af7ef38` | 0 | 1 |
| `53ddf589af76` | 1 | 0 |
| `5ece33085e1d` | 0 | 1 |
| `8bdbf9d8b1bb` | 0 | 1 |

Thus 6/24 target records are missing, including 6/8 target serving errors. All 16 target serving successes have reference-path output, but only two of eight serving errors do. Missingness is observably associated with serving disagreement in this selected set. The reason for that association, including any export mechanism, is not supplied and cannot be identified here. The missing set itself is class-balanced, with three labels of each class; class balance does not resolve its error-selection problem.

The contract correctly rejects the apparent improvement from 8/24 to 4/18: the same-record target comparison is 2/18 to 4/18. Likewise, 12/48 versus 6/42 is an unequal-coverage comparison, not a paired overall effect. Counts of corrections alone would miss four regressions.

For all 24 target records, training errors can be 4 through 10, versus eight serving errors. That allows an error-count change from -4 to +2, or -16.67 to +8.33 percentage points, on a fixed denominator of 24. The target benefit's sign is unresolved. No imputation of a particular result for any missing ID is needed or justified.

## Staging fairness and scope

The declared staging design is appropriate for separating initial test selection from later interpretation: turn 1 contains no paired path outputs; the fixed second packet arrives after both first responses irrespective of their requests; the first-round selection measure uses turn 1 alone. The contract also allows a justified alternative discriminator to earn full D4 credit while separately tracking selection of the path comparison. This avoids grading an agent as if the later packet had already been visible or making one preferred test the sole route to credit.

These are findings about the written design. The allowed files cannot establish that actual context isolation, timing, identical permissions, or configuration parity were implemented. Runs and prompts were deliberately outside this review. Execution compliance therefore remains unverified, not failed.

The first packet openly supplies diagnostic metadata and instructs record-ID joins; this is a structured synthetic diagnostic exercise. Its small selected sets, distinct individuals across sites, synthetic predictions and audit statuses, and absent models/images are clearly disclosed. The contract appropriately disclaims an uncued real-world task, a controlled improvement estimate over R03-RAW, population performance, executed channel-order causation, and proven distribution shift.

The reported 98% training and 97% validation accuracy come from different records, with no target validation. They cannot establish a serving regression or determine whether Adam, SGD, learning rate, or training duration would improve the target. The path comparison shows mixed descriptive behavior in the authored outputs under its same-input/frozen-model contract. It does not settle every possible optimization contribution to remaining errors. The stated update respects this distinction and does not invent an exclusive optimizer claim that the user never made.

## Grading review and nonblocking clarifications

The multi-turn arithmetic is consistent: five integer dimensions sum to a 0–10 raw/normalized score, both nonpositive penalties are added, and the result is floored at zero. The worked multi-turn example is correct. The contract explicitly allows inconclusive evidence and qualified reformulation, does not require one verdict word, and requires material numerical, coverage, provenance, and scope errors to be recorded beyond the coarse total. I found no internal scoring contradiction requiring a revision.

The following are optional clarifications or review cautions, not detected defects:

1. **Distinguish full-target bounds from full-pooled bounds.** Across all 48 selected records, training errors are bounded 6–12 versus 12 serving errors, so the full-pooled count cannot worsen under the authored labels. A carefully scoped statement of pooled non-worsening is valid even though full-target direction is unresolved. Strict pooled improvement is unknown, and pooled non-worsening cannot justify a target-site switch. Adding this to the contract could prevent an overly broad penalty for any statement about the pooled direction.
2. **Treat the next missing-output request as a future evidence priority.** Turn 2 says no other evidence or access is available, and the contract says no hidden missing values have been authored. A respondent may correctly name those six outputs as the next thing worth obtaining and state that the current exercise stops at its boundary. Do not require obtaining them now, inventing their values, or repeatedly asking for unavailable data. The existing missing-evidence rubric permits a pending test.
3. **Keep mechanism language descriptive.** Observed concentration of missing rows among serving errors is a valid result. A claim that the exporter intentionally filtered errors, or a formal missingness-mechanism conclusion without more evidence, is not. Likewise, path-dependent predictions do not independently verify RGB/BGR implementation behavior.
4. **Do not treat one pair of runs as a stable effect estimate.** The written two-context comparison can reveal behaviors on this fixture; it cannot alone establish a general skill improvement or separate effects of the multiple fixture revisions. Replication is a future evaluation improvement, not a prerequisite to using this developmental case.

The copied rubric's `cases.md` reference is safely disambiguated by the variant contract, which expressly names itself the scenario contract and prohibits reading an external case. No additional case was read. The unchanged rubric may remain as supplied.

## Disposition

No evidence or scoring-file correction is required on the basis of this independent review. Preserve the frozen fixture. Apply its scoped expectations as written, retain material-error flags separately from scores, and regard actual staging compliance as outside the evidence available to this reviewer.
````

## Independent grading

The grader sees public artifacts, response/action records, saved agent computations,
the frozen expectations, and unchanged [rubric](rubric.md). The mapping, skill,
fixture review, generator, and earlier results are withheld. A is baseline; B is
skill in this record. An input-only reviewer supplied the pooled-bound arithmetic
clarification before grading; it changed neither the fixture nor agent inputs.

### instructions.md

````markdown
# Independent R03-STRESS grading

Read only this folder's packet.md, expectations.md, rubric.md, and these instructions.
Do not inspect parent/sibling folders, arm mapping, skill snapshot, fixture review,
generator, prior tasks, or other context. No network or delegation. You may write
grading analysis code in this folder. Save grades.json and review.md here.

expectations.md is the scenario contract for this variant. The generic rubric's
cases.md link does not authorize loading a different case. Use the unchanged five
dimensions and penalties over each whole two-turn transcript. Do not reward length,
vocabulary, or matching a preferred verdict word. Preserve claim strength and
read causal/provenance qualifications in context. Evidence means authored values,
not verified true labels, executed classifier behavior, or population performance.

Independently compute/check the raw rows from packet.md. Grade first-round choice
from turn 1 alone. The later packet is fixed and supplied irrespective of requests;
good second-turn execution does not retroactively demonstrate initial selection.
Other well-justified discriminating tests may earn full D4 credit, while the
separate indicator must honestly report whether a matched path test was selected.

Inspect missingness, consistent comparison denominators, corrections AND regressions,
opposite site results, and full-target uncertainty. Exact numerical bounds are useful
but not required for full credit if the answer accurately separates observed paired
harm from unknown full-set direction. A comparison against different-coverage rates
does not establish a paired benefit. Missing cells cannot be invented or silently
treated as successes/failures. Available computation should be performed directly;
requests for genuinely absent outputs/access do not incur deflection penalties.

Arithmetic nuance confirmed by an independent input-only fixture review before
grading: across all 48 selected records, reference-path errors are bounded 6-12
versus 12 serving errors. That supports conditional full-pooled non-worsening,
not strict improvement or a target-site benefit. Do not penalize this valid scope
distinction. The frozen scenario contract and execution inputs remain unchanged.

For each deduction or material flag, cite observable evidence and its consequence.
Record material execution/numerical/scope errors even if the rubric total is high.
Use review.md for judgment ambiguities and any alternative reasonable score.
Do not infer which condition is baseline or treatment; arm labels are withheld.

grades.json structure (replace nulls with numeric judgments; include A and B):
{
  "case_id": "R03-STRESS",
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
        "turn1_path_comparison_selection": "Observed choice, with evidence",
        "turn2_direct_computation": "Observed execution, with evidence",
        "id_join_and_missingness": "Observed pairing and missing-cell handling",
        "corrections_regressions_and_denominators": "Observed numerical and scope handling",
        "full_target_uncertainty_and_handoff": "Observed bounds/scope and next decision"
      }
    }
  ]
}

raw = normalized = sum of the five 0-2 dimensions.
final = max(0, normalized + both penalties), with each penalty in {0, -1, -2}.
Save original grades before author adjudication and do not rewrite them to favor
a condition. Return a brief completion status after saving.
````

### grades.json

````json
{
  "case_id": "R03-STRESS",
  "conditions": [
    {
      "condition": "A",
      "dimensions": [2, 2, 2, 2, 2],
      "contrarianism_penalty": 0,
      "evidence_deflection_penalty": 0,
      "raw": 10,
      "normalized": 10,
      "final": 10,
      "dimension_reasons": [
        "D1: Turn 1 opens 'Defer all three training changes' because the available evidence does not establish a training cause; it computes existing evidence before recommending a diagnostic comparison. Turn 2 again holds training changes and does not release RGB as a fix.",
        "D2: Turn 1 identifies the unsupported link from the observed new-site failures to Adam, learning rate, or duration, and explains why the 97% report on different records cannot isolate a serving regression. Turn 2 identifies the failed uniform-repair assumption and the completeness assumption invalidated by six missing target outputs.",
        "D3: Turn 1 retains materially distinct model-generalization, serving/input-processing, and label-definition explanations alongside unresolved training causes. Agreement versus disagreement between frozen-model paths would change their support differently; turn 2 retains residual/generalization and optimization uncertainty rather than naming one as proved.",
        "D4: Turn 1 explicitly selects a same-record, fixed-checkpoint reference-versus-serving comparison, with contrasting outcomes and a shared-defect limitation. Missing artifacts make this a legitimate pending test. Turn 2 directly executes its available archive comparison by ID and site, checks coverage, and makes completing the six missing outputs the next discriminating step. Conditional later validation is handoff, not fictitious execution.",
        "D5: Turn 2 strengthens path dependence conditionally on the supplied metadata, reports source improvement and target paired harm with both corrections and regressions, rejects uniform repair, and bounds the full-target result at 4-10 errors versus eight serving errors. It does not validate any training option or infer proven distribution shift."
      ],
      "review_flags": [],
      "indicators": {
        "turn1_path_comparison_selection": "Yes, selected in turn 1 alone: 'same-record, fixed-checkpoint comparison of reference inference and serving.' The request holds inputs and model fixed and includes source and target records. This was proposed, not executed, before the fixed later packet arrived.",
        "turn2_direct_computation": "Observed in the supplied action log and saved executable analysis: analyze-turn2.ps1 was run and generated ID/path joins, transition counts, coverage and bounds. Independent recomputation from the packet's public raw JSON agrees. No model execution is claimed.",
        "id_join_and_missingness": "Joins by record ID and path, verifies all 48 archived serving rows against the original archive, uses 42 complete pairs, and explicitly lists the six missing target training-path outputs. All six are serving errors; their reason for absence is left unknown and no predictions are imputed.",
        "corrections_regressions_and_denominators": "Correct source 4/24 to 2/24 with 3 corrections/1 regression; target 2/18 to 4/18 with 1 correction/3 regressions; pooled 6/42 in both with 4 corrections/4 regressions. Explicitly rejects comparing target 8/24 serving against 4/18 reference as a demonstrated improvement.",
        "full_target_uncertainty_and_handoff": "Correct full-target error bounds 4-10/24 versus 8/24; improves, ties, or worsens remain possible. The saved analysis also correctly bounds full pooled reference errors at 6-12/48 versus 12/48 serving. Requests missing outputs and provenance/contract checks when access exists, followed by validation before a serving or training change."
      }
    },
    {
      "condition": "B",
      "dimensions": [2, 2, 2, 2, 2],
      "contrarianism_penalty": 0,
      "evidence_deflection_penalty": 0,
      "raw": 10,
      "normalized": 10,
      "final": 10,
      "dimension_reasons": [
        "D1: Turn 1 says not to choose SGD, learning rate, or longer training because no training-optimization cause has been identified. It first computes the available evidence, and turn 2 continues to withhold both training changes and an unvalidated preprocessing substitution.",
        "D2: Turn 1 explicitly labels optimization as an inferred, unestablished explanation for the observed failure, not an exclusive causal claim by the user. It identifies the absence of a trusted frozen-model reference comparison and the noncomparability of the 97% report with different diagnostic records. Turn 2 identifies uniform repair and complete coverage as unsupported assumptions.",
        "D3: Turn 1 distinguishes optimization, model generalization, and serving/preprocessing formulations and states different predictions under a reference-versus-serving comparison. Turn 2 strengthens path dependence, weakens uniform repair, and retains unresolved generalization and optimization without treating persistent errors as proof of either.",
        "D4: Although the available site summary is labeled the executed primary test, turn 1 explicitly recognizes that it cannot separate generalization from serving behavior and selects a bounded same-record, frozen-model reference-versus-serving comparison as the next primary test. It requests the minimum missing predictions with provenance and contrasting outcomes. Turn 2 directly completes the available portion by ID/site and identifies the six absent outputs as the next discriminator. See review.md for the labeling ambiguity.",
        "D5: Turn 2 changes support in response to eight changed predictions, opposite site effects, and selective observed coverage; it rejects a uniform RGB fix and leaves the original training decision unresolved. The 14-20 correct out of 24 full-target bounds and the three-missing-correct-for-improvement threshold are arithmetically correct and preserve uncertainty."
      ],
      "review_flags": [],
      "indicators": {
        "turn1_path_comparison_selection": "Yes, selected in turn 1 alone: 'The next primary test should be a same-record reference-versus-serving comparison,' with frozen model and original inputs fixed and trusted reference predictions requested for the same 48 IDs. The already executed site-disagreement summary is a separate descriptive check and is not being counted as execution of the matched-path test.",
        "turn2_direct_computation": "Observed in the supplied action log and saved executable analysis: analyze-turn2.ps1 was run, generated the paired comparison, and computed target bounds. Independent recomputation from the public raw JSON agrees with the reported values; no classifier execution or independent audit is claimed.",
        "id_join_and_missingness": "Correct ID/path joins and coverage checks produce 42 pairs, with all 48 serving rows matching the earlier archive. Lists all six absent training-path IDs, says they are all target serving errors, and explicitly leaves both missing outcomes and the explanation unknown.",
        "corrections_regressions_and_denominators": "Correct source paired accuracy 20/24 to 22/24 and transitions 3 corrections/1 regression; target 16/18 to 14/18 and 1 correction/3 regressions; pooled 36/42 in each with 4 corrections/4 regressions. Rejects the different-coverage comparison 36/42 versus 36/48 and distinguishes equal pooled accuracy from opposite site effects.",
        "full_target_uncertainty_and_handoff": "Correct target reference accuracy bounds 14-20/24 against serving 16/24; no unsupported full-target direction. Correctly states at least three of six missing reference predictions must be correct for strict target improvement, two for a tie. Requests those six outputs with identity/provenance and an export explanation, acknowledges unavailability, and requires further validation before intervention."
      }
    }
  ]
}
````

### review.md

````markdown
# Independent R03-STRESS review

Both conditions receive **[2, 2, 2, 2, 2]**, raw = normalized = **10**, with zero contrarianism and evidence-deflection penalties, final **10/10**. These are the original independent judgments, before author adjudication. No material execution, numerical, missingness, provenance, or scope failure was found in either supplied transcript.

Only this grading folder's instructions.md, packet.md, expectations.md and rubric.md were read as inputs. No external case, source implementation, prior task, arm mapping, network material, or other agent context was consulted. Condition labels are retained without inferring arm identity. The finite authored evidence, not actual classifier behavior or real-world label validity, is what was recomputed.

## Independent raw-row check

The saved independent-check.ps1 parses the four public JSON blocks directly from packet.md and joins labels, original serving, and comparison rows using ID/path dictionaries. It does not use either condition's computed result as an input. Its execution completed successfully.

There are 48 unique labels, 48 unique original serving rows, and 90 unique comparison ID/path rows: 48 serving-v4 and 42 training-v2. No unknown IDs, changed comparison model, serving-archive differences, or missing serving rows were found. Each site has 24 labels, split 12/12 by class. Turn-1 serving disagreements are source 4/24 and target 8/24.

| Paired scope | Pairs | Serving errors | Reference errors | Corrections | Regressions | Both wrong | Both right |
|---|---:|---:|---:|---:|---:|---:|---:|
| Source | 24 | 4 | 2 | 3 | 1 | 1 | 19 |
| Target | 18 | 2 | 4 | 1 | 3 | 1 | 13 |
| Pooled | 42 | 6 | 6 | 4 | 4 | 2 | 32 |

Source paired error rate falls by 8.33 percentage points, target rises by 11.11 points, and pooled paired errors tie. All eight changes and their directions agree with the transcripts' saved computations.

The six missing reference predictions are target IDs `25c1bf74e4d2`, `3d982af7ef38`, `0ef404a68aa3`, `5ece33085e1d`, `53ddf589af76`, and `8bdbf9d8b1bb`. All six have serving disagreements. No missing prediction value can be inferred. The source missing-ID array in the independent script prints a null entry through PowerShell's empty-property enumeration; the independently computed source missingCount is zero and this is not an input-data missing cell.

The full target reference-error interval is 4-10/24, versus 8/24 serving, allowing benefit, equality, or harm. Equivalently, reference accuracy is 14-20/24 against serving 16/24; three or more correct missing predictions give strict target benefit, and two give a tie. Across all 48 selected records, reference errors are 6-12/48 versus 12/48 serving. This permits conditional full-pooled non-worsening, not guaranteed strict improvement and not a target-site benefit. Both conditions' claims are compatible with these facts.

## Evidence and judgment ambiguities

**A, first-round selection and test scope.** Packet response-turn1.md explicitly selects a 'same-record, fixed-checkpoint comparison of reference inference and serving' (packet.md around line 1241). It requests model/input/path artifacts and mentions preprocessing, scores, class mapping, thresholds and final predictions as measurements within this comparison. This is one frozen-input/frozen-model path comparison, not several unrelated investigations disguised under one name. The later label/holdout/training suggestions are conditional handoff. The absence of a turn-1 reference archive justifies a pending request and no deflection penalty. Turn-2 execution cannot substitute for this selection, and was not used to infer it.

**B, first-round test labeling.** Response-turn1.md first calls its available site-disagreement computation the executed Primary Discriminating Test, then explicitly states that 'both model generalization and site-dependent serving behavior predict that result.' It proceeds to select the same-record reference-versus-serving comparison as the next primary test (packet.md around lines 1954-1963). The site summary alone would have weak causal discrimination and would merit D4 = 1. The actual turn also selects a suitable bounded pending comparison, specifies minimum absent evidence, and defines contrasting outcomes. Thus D4 = 2 is warranted by the observable selected follow-up, not by the 'Primary' label or later fixed packet. The path-selection indicator is yes, pending, and not falsely labeled executed.

A possible stricter alternative for B is **[2, 2, 2, 1, 2] = 9/10**, if only the check explicitly labeled executed is considered its first-round primary choice. I do not adopt this reading: the rubric allows one well-chosen pending test for missing-evidence cases, and the instructions require credit for actual decisions rather than protocol vocabulary. Descriptive inspection plus one appropriate pending causal comparison does not itself establish excessive diagnostic scope.

**Causal qualifications.** A says the channel-order comparison 'isolates channel order within the authored fixture,' immediately conditional on the supplied same-input/frozen-model/only-channel-order contract, and explicitly says it is not model execution or independent implementation verification. B likewise makes its channel-order implication conditional on the contract. Neither statement warrants a fabricated-execution or overclaim flag. Neither treats channel order as an exclusive replacement explanation or promotes residual target errors to proven distribution shift.

**Full-target versus pooled language.** A supplies the correct full-target bounds in its answer and full-pooled bounds in its saved analysis. B's statement that the reference path may be 'worse, equal or better overall' follows a paragraph explicitly confined to all 24 selected target records. Read in context, it does not claim the full 48-record pooled result can worsen. No scope deduction is justified. Likewise, neither condition's warning against comparing different-coverage rates contradicts the separately valid full-pooled bound.

**Handoff and penalties.** Both directly compute every available safe comparison and leave only genuinely absent outputs/access pending. A asks additionally to verify executable contracts and reproduce the paths when access becomes available; B asks for the six missing outputs and explanation. These requests do not defer accessible work to the user. Neither retrains, changes serving, blocks a verified fix, imputes missing outcomes, or presents audit status as independently confirmed. Consequently both penalties are zero and both review_flags arrays are empty.

No file revision or test-case correction is required by this review. The coarse rubric produces a tie for these two transcripts; it does not establish equivalence of methods or any population performance claim.
````

## Author review and actual edits

Both conditions identify the pending same-record/fixed-model comparison without
the earlier replay-availability announcement. Both then execute the available
comparison, report missingness associated with existing errors, count regressions
as well as corrections, and retain uncertainty about the full target outcome.
The scripts and JSON computation results are preserved alongside actual answers
and action logs. No model, preprocessing implementation, missing prediction, or
real label audit is claimed to have been executed or independently verified.

The independent fixture reviewer found no actionable defect. Their additional
pooled-bound observation was recorded in grader instructions before grading:
full-pooled errors cannot exceed serving's 12 within this fixture, even though
the target outcome can worsen. That is a useful scope qualification, not a change
to frozen evidence or the rubric. The reviewer had no agent outputs, generator,
keymap, skill, or prior evaluation material. Actual staging is verified separately
by the author's sealed first-turn hashes and identical second-packet copies.

The treatment's first response calls the descriptive site comparison a completed
Primary Discriminating Test, then explicitly acknowledges that both generalization
and site-dependent serving behavior predict the result. It retains both and asks
for a same-record path comparison as the next test. This is less clear than calling
the descriptive computation a preliminary check. The important behavioral question
is whether it mistakes localization for causal discrimination or prematurely acts
on that inference; the full response and independent judgment remain available
above, rather than converting a naming preference into an automatic failure.

The independent grader assigns both conditions 10/10 with no penalties or
material flags. They credit the treatment's explicitly selected pending path
comparison, not the earlier descriptive summary. They also preserve a stricter
alternative of 9/10 on D4 if that first executed check is treated as the only
primary choice. The author accepts full credit for the actual subsequent choice:
the agent recognizes shared predictions, retains uncertainty, asks for the
appropriate comparison, and does not act prematurely. The loose first-test
label remains visible as an output-quality issue, not silently corrected text.

This result does not justify adding a new instruction. The current skill already
explains that shared predictions can localize a failure without distinguishing
formulations, and the treatment explicitly acknowledges that limitation. Adding
another rule based only on the label would duplicate the existing requirement.
`SKILL.md` remains at 281 lines with the original tested hash. No runtime change
or runtime retest is claimed. The rubric is coarse enough to give both conditions
full credit despite differences in brevity and test naming; a perfect score is
not a claim of flawless wording or a measured skill advantage.

The repository adds this Markdown fixture and execution record, with links from
the project README, evaluation README, and R03 case. Earlier reports and original
scores are retained. No package, classifier runtime, external connection, commit,
push, PR, or release is created. The canonical suite still contains 20 cases.

This single pair demonstrates handling of these particular synthetic rows, not
reliable effectiveness or a causal skill advantage. Multiple fixture properties
changed since the previous pair, so the outcome cannot isolate removal of the
cue as a causal factor. Structured inputs and the explicit instruction to join
by ID still provide assistance. Missingness has one simple pattern, labels are
authored, all observed keys are valid/unique, and only one inherited model class
and host are used. Cross-model and cross-host validation remain outstanding.

## Verification

Raw-row verification confirms 48 unique labeled records, 90 unique comparison
cells, all 48 unchanged serving rows, 42 complete pairs, and the six target IDs
without reference predictions. It checks all correction/regression categories,
different site directions, and possible outcomes without filling missing cells.

Final checks after assembly passed:

- Skill creator's `quick_validate.py`: `Skill is valid!`.
- Repository audit: 883 assertions passed, 0 failed; ten distribution files,
  nine Markdown files, 30 internal links, and 281 skill lines. Checks include
  frontmatter, Markdown fences/links, case counts, score arithmetic, UTF-8/no BOM,
  whitespace, license, and absence of private workstation paths.
- Historical full-suite audit: 639 assertions passed, 0 failed. Its 40 case runs,
  54 responses, probes, and retests remain consistent.
- Historical R03-RAW audit: 216 assertions passed, 0 failed. That record's frozen
  inputs, outputs, original grades, numerical bounds, and snapshot remain intact.
- R03-STRESS audit: 211 assertions passed, 0 failed. It checks frozen inputs,
  identical evidence in each arm, four sealed first-turn files, all four saved
  response/action pairs, archived computation code/results, 90 comparison cells,
  42 pairs, exact missing IDs, transitions, bounds, original scores, and table
  arithmetic. Completion hashes preserve 43 execution/grading/review artifacts.
- `git diff --check`: clean. Distribution files are untracked, so their actual
  contents are also checked independently of Git's diff.

No classifier or production system is part of validation. No commit, push, PR,
publication, or release tag was created. The skill and rubric remain unchanged.

### Author computation from frozen rows

````json
{
  "source": {
    "records": 24,
    "complete_pairs": 24,
    "missing_reference_ids": [],
    "serving_all_errors": 4,
    "serving_paired_errors": 4,
    "reference_paired_errors": 2,
    "corrections": 3,
    "regressions": 1,
    "wrong_under_both": 1,
    "correct_under_both": 19,
    "missing_records_serving_errors": 0
  },
  "target": {
    "records": 24,
    "complete_pairs": 18,
    "missing_reference_ids": [
      "0ef404a68aa3",
      "25c1bf74e4d2",
      "3d982af7ef38",
      "53ddf589af76",
      "5ece33085e1d",
      "8bdbf9d8b1bb"
    ],
    "serving_all_errors": 8,
    "serving_paired_errors": 2,
    "reference_paired_errors": 4,
    "corrections": 1,
    "regressions": 3,
    "wrong_under_both": 1,
    "correct_under_both": 13,
    "missing_records_serving_errors": 6
  },
  "bounds": {
    "possible_full_target_reference_errors": [
      4,
      10
    ],
    "full_target_error_change_reference_minus_serving": [
      -4,
      2
    ],
    "completion_count": 64,
    "meaning": "Unknown cells enumerated as errors/correct outcomes; no true completion is claimed."
  },
  "verified_frozen_files": 16
}
````
