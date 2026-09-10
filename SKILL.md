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
quota. Let evidence and the pending decision determine the live set; more
candidates are not evidence of better reasoning. Presentation limits in section 9
do not justify dropping a materially different, decision-relevant candidate.

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

Before choosing the test, make one lightweight **Shared-Frame / Coverage Check**:
do the live formulations all rely on one consequential, untested premise about
the relevant boundary, measurement path, causal layer, population, time scope,
or optimization target? Select what matters here; do not audit a category checklist.
If that premise failing would undermine the whole set, and a plausible alternative
would change the decision and predict different evidence, add at most **ONE
Outside-Frame Challenger**. Name the shared premise and its contrasting prediction
briefly when decision-relevant. Generic "measurement could be wrong" is insufficient;
ground the challenger in this task. If none is warranted, proceed without one.
Do not chain coverage audits or expand the set merely to satisfy a quota.

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
Include an unaccounted or outside-boundary outcome when the observation method
could omit relevant stages; an artifact's label does not define its boundaries.
Handle such a result through the evidence update below, not a forced winner.
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
2. If a consequential result fits no live formulation, mark it **OUTSIDE CURRENT
   FRAME**: the set may be incomplete. This is an evidence diagnostic, not a sixth
   verdict. Preserve the unexplained residual; do not award it to the closest
   candidate. Repeat the lightweight coverage check once for this new evidence,
   adding at most one grounded challenger if warranted. Otherwise leave it unresolved.
3. Update affected candidates using the labels below with a short evidence reason,
   and re-check load-bearing assumptions invalidated by the test.
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

## 9. Default to compact output; disclose detail as needed

Complete the relevant checks, but show only decision-relevant evidence and
rationale, not an exhaustive reasoning transcript or hidden chain of thought.
Choose the shortest path that preserves the decision, discrimination, and scope:

| Path | When | Visible output |
| --- | --- | --- |
| Fast | BYPASS, strong KEEP, verified deterministic diagnosis, or simple low uncertainty | Usually 2-5 sentences: source-backed observation, framing, verdict/release if entered, then host continuation. No invented alternative or new test. BYPASS needs no adversarial report. |
| Normal (default) | Ordinary unresolved coding, debugging, architecture, research, or product framing | Usually 120-220 English words: observation/provenance, current framing, live alternatives, one Primary Test with contrasting outcomes, result or pending evidence, verdict and handoff. Fold each key assumption into its prediction. |
| Deep | Stakes or complexity require more detail, including when 5+ live formulations materially affect the decision | Usually 250-450 English words: expand assumptions, predictions, candidate updates, and scope limits only where needed. Domain alone does not require this path. |

These are soft presentation guides, not word quotas or correctness gates; use
equivalent brevity in other languages. Normal output usually shows 2-4 live
formulations including the current one, at most 3-4 by default. Do not conceal a
consequential challenger to fit that range: merge genuine redundancies, or expand
the output when needed. A supported single formulation needs no padding.

Keep provenance compact (for example, "report.txt, supplied summary"), never omit
it or upgrade it. State whether the one primary comparison ran or is pending;
preliminary localization is not a discriminating test when all candidates predict
it. Give one clear verdict and release status, plus **Reformulated Problem:** when
required. Headings are optional; do not mechanically reproduce all workflow steps.

On later turns, use **delta output**: new evidence/source, what changed, affected
candidate updates and scope, a new Primary Test only if useful, then verdict/handoff.
Do not repeat unchanged observations, formulations, assumptions, or predictions.
Reference prior candidates briefly so the update remains intelligible.

Do not repeat the user prompt, narrate internal exploration, stage a debate,
explain the methodology unless asked, or list discarded/merged candidates unless
their change matters now. Stop once the framing decision is supported; mark any
authorized downstream work separately and let the host continue.
