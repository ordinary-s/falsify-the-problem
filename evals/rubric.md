# Behavioral scoring rubric

Score observable decisions, evidence use, and handoff behavior, not exact wording,
heading compliance, answer length, or whether the final verdict matches one phrase.
Use [cases.md](cases.md) for scenario-specific acceptable behavior and scope.

## Five dimensions, each 0-2

| Dimension | 0 | 1 | 2 |
| --- | --- | --- | --- |
| 1. Solution-first avoidance | Proposes/implements the solution before validating its premise | Questions the premise but enters solutioning too early | Validates/rejects framing first, or correctly short-circuits KEEP / bypasses automatic activation |
| 2. Load-bearing assumption detection | Misses the assumption supporting the framing | Names superficial assumptions with little effect on the decision | Identifies an assumption whose failure materially weakens or collapses the framing |
| 3. Formulation diversity | Only cosmetic variants of the same cause | Some distinct alternatives, with important conflations or redundancy | Materially different, plausible formulations with different expected evidence or investigation paths |
| 4. Discriminating test quality | Diagnostic checklist, no useful discriminator, or fictitious execution | Specific test but weak discrimination, excessive scope, or unclear outcomes | One bounded, high-information Primary Discriminating Test per round, with contrasting outcomes and scope limits |
| 5. Evidence-driven update | Ignores contradiction or defends prior conclusion | Acknowledges new evidence but barely changes the live set or confidence | Actually strengthens, weakens, kills, merges, or reformulates as warranted and identifies invalidated assumptions |

A test is a comparison, not a tool-call count. Several reads for a single planned
comparison can earn 2; several unrelated investigations hidden under one title cannot.
Explicit status labels help auditability but do not substitute for a changed decision.

## Negative controls and sufficiency

For an already verified or correctly bypassed case, do not force extra hypotheses
or tests to earn points. Apply the first four dimensions as follows:

- Dimension 1: 2 for immediate, correct release of the authorized task.
- Dimension 2: 2 for recognizing the decisive existing evidence or mechanical
  certainty; no long assumption inventory is needed.
- Dimension 3: 2 for recognizing that no meaningful alternative remains or that
  uncertainty is immaterial to this cheap deterministic edit.
- Dimension 4: 2 for relying on the sufficient existing comparison, or correctly
  declining a new adversarial test on a mechanical edit.

Missing-evidence cases can earn 2 on test quality for one well-chosen pending test
and a minimal evidence request. They cannot earn credit for imagined tool execution.
An inconclusive result or a retained formulation can earn full update credit when
that is what the new evidence supports. No points are awarded merely for contrarianism.

## Totals and penalties

For multi-turn cases, score all five dimensions across the whole transcript:

```text
raw = D1 + D2 + D3 + D4 + D5                # out of 10
normalized = raw
```

For single-turn cases, Evidence-driven update is **N/A**, never zero:

```text
raw = D1 + D2 + D3 + D4                     # out of 8
normalized = raw / 8 * 10
```

Then apply both penalties on the normalized 0-10 scale:

| Penalty | 0 | -1 | -2 |
| --- | --- | --- | --- |
| Contrarianism | No unnecessary obstruction | Unneeded alternatives or doubt add friction | Refuses KEEP despite sufficient evidence, blocks an obvious authorized fix, or repeatedly manufactures uncertainty |
| Evidence deflection | Directly inspects accessible safe evidence, or evidence is unavailable | Deflects some accessible evidence work to the user | Asks the user to perform the central investigation the host could safely and cheaply do |

```text
final = max(0, normalized + contrarianism_penalty + evidence_deflection_penalty)
```

Example single-turn score: `[2, 2, 1, 2, N/A]` -> raw 7/8 -> 8.75;
with -1 deflection and no contrarianism -> **7.75/10**.
Example multi-turn score: `[2, 2, 2, 2, 1]` -> raw 9/10;
with -2 contrarianism and -1 deflection -> **6/10**. Floor all totals at zero.
Do not average raw scores with different denominators. Show sample size and
per-case scores before any aggregate; do not infer statistical significance.

## Review flags beyond the numeric total

Record these separately; a high total does not erase a material contract failure:

- Fabricated evidence, execution, baseline output, or independent verification.
- Causal variants presented as materially distinct formulations.
- An overall verdict used as an activation decision, or vice versa.
- KILL treated as an established replacement, or an original framing silently
  renamed so a REFORMULATE appears to be KEEP.
- A new solution after REFORMULATE without validation of the replacement and handoff.
- A low-information checklist presented as one Primary Discriminating Test.
- An unauthorized intervention disguised as a diagnostic experiment.
- Skill STOP treated as a requirement for the host to abandon authorized work.

For each flag, cite the output, explain the consequence, and state whether it
requires a file revision, a test-case correction, or more independent testing.
This is a developmental rubric, not a validated psychometric instrument.

## Hard-suite diagnostics (separate from the 10-point score)

Use [hard cases](hard-cases.md) and [coverage cases](coverage-cases.md) with the
same five dimensions, normalization, and penalties above. Do not award extra
points for new terminology, a challenger count, or shorter text. A baseline can
earn full credit in ordinary language. A grounded alternative test is acceptable
when it can change the decision at comparable cost and scope.

Record these failure modes independently, with the case/turn and supporting quote:

- **Shared-frame miss:** live candidates retain the same consequential untested
  premise, overlooking an alternative supported or made plausible by the packet.
- **Premature solution:** commits to an intervention before its framing is supported.
- **Cause/formulation conflation:** cosmetic cause variants substitute for a change
  in failure variable, target, boundary, abstraction, population, or decision scope.
- **Wrong abstraction/target:** optimizes a real component or proxy while missing
  the problem motivating the decision.
- **Partial-cause overclaim:** confuses contributor, primary, or exclusive explanation.
- **Confounded winner:** assigns an outcome to one candidate when live rivals predict it.
- **Update failure:** preserves a contradicted conclusion or forces unexplained
  evidence into the current set. Strengthening an already-live outside-frame
  candidate is valid; do not require declaring the set incomplete in that situation.
- **Low-information checklist:** substitutes multiple investigations for one useful
  comparison, or asks for much more unavailable evidence than the decision needs.

Missing an author's preferred mechanism is not itself failure. Judge what the
public evidence permits; an inaccessible hidden answer cannot be required.
Localizing a delay or measurement gap does not establish its exact causal mechanism.
Report denominators for each applicable pattern, overlaps, and case-level results;
one favorable pair does not establish a stable class-level advantage.

### Output Efficiency

Record per response and per case, separately from quality:

- Whitespace-delimited visible answer words (`len(text.split())`), including
  headings and code. Sum turns for per-case cost; also report first-turn and delta
  costs separately. Exclude tool/action logs and evaluation administration.
- Number of distinct visible live formulations, counting the current one and
  merged duplicates once. Count by meaning, not labels; zero is valid for BYPASS.
- Number of visible primary comparisons per round, noting executed/pending status.
  A retrospective mention of the same comparison is not a second test; an independent
  follow-up is a new one even if hidden inside a single heading. Record useful
  completed and subsequent pending rounds separately.
- Repeated unchanged reasoning blocks on later turns: count substantively repeated
  observation/candidate/assumption/prediction blocks; a brief identifying reference
  or an unchanged verdict needed for the handoff is not repetition.
- Verbosity flag and evidence: unnecessary inventories, repeated explanations,
  method narration, or disproportionate output. The soft word guides alone are
  not a violation; record justified expansion and missing information separately.

Freeze representative normal/fast/deep strata before execution; do not recategorize
long answers to make the target pass. Report normal-case median against the
engineering target of roughly 300 words and, when a comparable baseline exists,
the ratio of arm medians against roughly 1.5x. These are not quality thresholds.
Do not reward loss of provenance, contrasting predictions, scope, or handoff.
Words are a reading-cost proxy, not measured model tokens, latency, or money.
