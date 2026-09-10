# Evaluating falsify-the-problem

Evaluate whether an agent attacks the current **problem formulation**, gathers
discriminating evidence, updates honestly, and stops at the right boundary.
Do not reward a longer answer, more alternatives, or automatic rejection.

- [Cases](cases.md): 20 synthetic cases and an auditable coverage index.
- [Rubric](rubric.md): five 0-2 dimensions, single-turn normalization, two penalties.
- [Smoke-test record](smoke-tests.md): actual development runs, limitations, and revisions.
- [Full-suite record](full-suite.md): paired execution of all 20 case variants,
  independent grading with arm labels withheld, and recorded limitations.
- [R03 artifact follow-up](r03-raw.md): a staged synthetic row-level variant,
  with a fixed skill snapshot, separate contexts, and auditable numerical checks.
- [R03 missing-pair test](r03-stress.md): fewer initial cues, mixed corrections and
  regressions, and incomplete comparison coverage with an unchanged skill.
- [Harder cases](hard-cases.md) and [hard-suite record](hard-suite.md): 12 cases
  probing partial truth, shared premises, targets, confounding, and reversals;
  paired quality/efficiency results and seven selected historical regressions.
- [Coverage cases](coverage-cases.md) and [coverage record](coverage-eval.md): six
  focused shared-frame cases across five domains, including a staged residual.

## Minimal manual procedure

1. Choose the case and decide the invocation condition before running it. Explicit
   invocation always enters the skill; C02 specifically tests automatic non-activation.
2. Materialize any described artifacts in an isolated temporary directory, or
   explicitly label them as supplied reports. Do not imply a fixture exists if it
   has not been created. Keep production systems outside the test.
3. Give the agent only the public task and currently available raw evidence. Do
   not give it hidden traps, expected behavior, verdict ranges, scoring, or future turns.
4. For the skill arm, load the complete `SKILL.md`. For a genuine baseline, use
   the same case, model/context class, tools, permissions, and evidence without
   these skill instructions. Use separate contexts and separate fixture copies.
5. Save the actual response and record reads, commands, edits, failures, and handoff.
6. For multi-turn cases, let the first response finish. Then deliver the next
   evidence packet. If it directly answers a requested test, make that available;
   do not adapt evidence to force a desired verdict. Save the second response.
7. Score using the rubric, identifying the observed behavior behind every non-full
   score and penalty. Prefer an independent grader when resources permit.
   Withhold arm labels using a per-case mapping saved separately. Disclose that
   response vocabulary can reveal the treatment; do not call this full blinding.
   Freeze original scores before the author reviews them. Record case defects and
   disputed grading separately rather than silently changing scores or answers.
8. Review failure modes, revise actual files where warranted, and re-run affected
   cases when possible. Distinguish a runtime retest from a desk review.

The case text sometimes uses an explicit invocation phrase. When building a paired
run, move that phrase to the skill-arm instruction so the actual task content is
identical; record this treatment difference. Keep C02 separate as an automatic
activation probe with the skill discoverable but not explicitly invoked.

For accessible evidence, observe whether the agent reads it directly rather than
asking the user to do so. For inaccessible evidence, observe whether it asks for
only the smallest discriminating input. Tool failure must remain a recorded failure,
not be reclassified as successful inspection.

## Running without an independent baseline

If separate baseline execution is unavailable, use the exact heading
**Counterfactual Baseline Risk Analysis**. Label it **qualitative, non-empirical,
not actual model output**. Describe risks without fabricating a transcript or
baseline scores. Do not claim percentage improvement, significance, or superiority.

An author applying the skill to a case in the same context is a manual dry-run,
not independent forward-testing. Label it accordingly. A baseline that already
has the skill or case answers in context is contaminated and cannot support a
clean comparison. Do not conceal contamination, failed runs, or mixed results.

## Harder-suite controls

Freeze the skill, public packets, reviewer expectations, and output strata before
execution. Only the skill arm loads the skill; do not send either executor the
case titles, tags, rubric, hidden premise, expected answer, or future evidence.
Both arms receive identical tasks and report contents in separate fixture copies.
Deliver later evidence after the first response finishes, without adapting it to
the answer. Record whether isolation is per case or per batch: batch execution
shares context across its cases and is a weaker independence claim.

Use the existing 10-point rubric. Record the additional failure-mode and
[Output Efficiency diagnostics](rubric.md#output-efficiency) independently, with
denominators and verbatim responses. Distinguish test selection from preliminary
localization and from later supplied results. Treat correct baseline answers and
null or mixed differences as findings; do not tune the baseline to fail. If a
case expectation is defective, preserve original grades and report adjudication
separately. If execution is unavailable, label that entry **NOT EXECUTED**;
structural checks are **desk-reviewed only**.

Make the isolated grader packet self-contained: include the referenced case
definitions as well as the rubric, or explicitly resolve their relevant criteria
inside the packet. Record missing references as a grading limitation; do not
silently invent their contents or rewrite an already returned grade.

## What to record

- Date, skill snapshot or hash, model/configuration information actually exposed,
  context isolation, tool availability, evidence packets, and invocation mode.
- Case IDs, exact outputs or clearly labeled excerpts, actual actions, and whether
  later turns used the same context as their first turn.
- Per-case dimension scores, N/A fields, normalization, penalties, and review flags.
- Baseline type; missing or unexecuted cases; who judged the outputs.
- Observed failures, resulting edits, and what was actually re-tested afterward.

## Coverage and interpretation

Required minimums and current counts are recorded in the cases' coverage index:
5 coding, 4 debugging, 4 architecture, 4 research, and 3 product/startup cases.
Cross-cutting categories overlap. A negative control is not automatically a KEEP
test: C02 instead tests BYPASS; the other four explicitly test KEEP.

The representative smoke set is C01, D01, A01, R01, and P01. It covers five domains,
a verified authorized fix, evidence access, proxy uncertainty, revised evidence,
KILL without a replacement, and downstream handoff. It is only a subset of the
suite; writing 20 cases does not mean executing all 20.

The follow-up full-suite record identifies each executed fixture variant. Concrete
local reproductions and supplied report summaries test different evidence-access
behaviors; a report-only run is not execution of the underlying raw-data case.

**This is a behavioral smoke test, not a statistically valid benchmark.** Small
development samples, a single model class, shared authorship, and qualitative
grading limit inference. Strong baseline behavior and weak skill behavior are
valid findings; record them rather than selecting only favorable examples.
