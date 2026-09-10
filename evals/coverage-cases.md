# Shared-frame coverage micro-suite

Six cases span coding, debugging, architecture, research, and product. Each supplies a
reasonable candidate set sharing one consequential premise. V06 additionally stages an
unexplained residual. See [execution record](coverage-eval.md).

All inputs and numerical results are authored synthetic fixtures. Public packets below
may be given to executors; reviewer notes, tags, output-path classifications, and future
turns must be withheld. A reasonable alternative test can earn full credit; there is no
secret unique answer. Unavailable evidence warrants uncertainty, not guessing the author’s answer.

| ID | Domain | Structures | Turns | Predeclared output stratum |
| --- | --- | --- | --- | --- |
| V01 | coding | shared-frame | 1 | normal |
| V02 | debugging | shared-frame | 1 | normal |
| V03 | architecture | shared-frame | 1 | normal |
| V04 | research | shared-frame | 1 | normal |
| V05 | product | shared-frame | 1 | normal |
| V06 | debugging | shared-frame, unexplained-residual, multi-turn | 2 | normal |

Output strata describe task complexity for cost analysis; they are not executor instructions
or grading quotas. They were fixed before execution. See [rubric](rubric.md) for unchanged
quality scoring and independent efficiency diagnostics. Full credit does not require Skill vocabulary.

## V01 — CPU candidates and request admission

**Public task / Turn 1**

Export requests are slow. The profiler shortlist is JSON encoding, compression, or template rendering. Pick the optimization with the largest end-to-end payoff. Read report.txt.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
Existing profiler covers only worker execution. In a sampled slow request, CPU time is 80 ms: JSON 40, compression 25, template 15. The same request has accepted_at=0 ms, worker_started_at=920 ms, response_sent_at=1000 ms. Twenty matched slow requests have the same stage proportions. Typical requests wait 5 ms before the worker and execute for 80 ms. Timestamp clocks are reconciled. Admission policy implementation is not supplied.
```

**Reviewer-only: why this tests problem formulation**

Expands execution boundary from the profiler to accepted-request latency; ranking CPU causes cannot address most elapsed time.

**Reviewer-only: shared premise**

All shortlisted candidates assume profiled worker CPU covers the end-to-end delay.

**Reviewer-only: behavior and acceptable scope**

Identify omitted admission boundary with a bounded same-ID timestamp comparison; preserve CPU contribution. One concrete queue/admission challenger suffices; do not invent the policy cause.

## V02 — Successful traces and absent failed operations

**Public task / Turn 1**

The incident team ruled out storage and is debating DNS, TLS, or response serialization for upload timeouts. Their traces look clean. Read report.txt and recommend the next investigation.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
Trace export contains 200 HTTP 2xx uploads, all under one second. The same window has 80 client timeout IDs; none is in the export. Export policy: retain spans only after successful response completion. DNS/TLS/client deadline durations for timed-out IDs are absent. An existing client log may supply one timed-out request timeline, but no such log is currently accessible. The successful traces themselves are accurate.
```

**Reviewer-only: why this tests problem formulation**

Changes inferential population and instrumentation boundary; does not merely add storage as a fourth cause.

**Reviewer-only: shared premise**

All candidates and the storage exclusion assume successful exported traces represent timed-out operations.

**Reviewer-only: behavior and acceptable scope**

Recognize common sample-coverage assumption, reopen exclusion of storage without asserting storage caused failure. Request one representative failed-ID stage/deadline timeline; no winner from successful traces.

## V03 — Deployment topology and decision ownership

**Public task / Turn 1**

Our release planning discussion narrowed delivery delays to monolith size, shared release trains, or cross-service test duration. Choose the target. Read report.txt.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
Six matched feature pairs cross small services/large monolith and independent/shared deploy schedules. Median pre-code wait is 14 days in every group; code-to-release time is 2 days. Change records show pre-code tickets awaiting the same commercial-policy decision owner. A deploy-process improvement saves 6 hours but leaves pre-code wait unchanged. This sample does not establish why decisions take 14 days.
```

**Reviewer-only: why this tests problem formulation**

Changes organizational/system boundary and elapsed delivery target; the right response is not another deployment cause.

**Reviewer-only: shared premise**

Every option assumes technical release execution dominates total delivery lead time.

**Reviewer-only: behavior and acceptable scope**

Compare ticket stages and topology strata, add decision-ownership challenger, scope attribution to observed wait without designing governance.

## V04 — Biological candidates and specimen handling

**Public task / Turn 1**

Study sites disagree on marker concentration. We shortlisted ancestry, diet, and disease severity. Which biology should the next study target? Read report.txt.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
Sites A and B differ in measured marker concentration after matching age and disease category. Site A freezes specimens within 10 minutes; B stores them at room temperature for four hours. Instrument calibration standards agree. A small archive contains aliquots from the same donor IDs assayed after both handling protocols at both sites, but results have not been retrieved. No new recruitment or wet-lab experiments are permitted.
```

**Reviewer-only: why this tests problem formulation**

Tests the shared biological/data-generating premise via the pre-measurement path; a calibrated instrument alone does not establish specimen equivalence.

**Reviewer-only: shared premise**

All shortlisted biology assumes specimen handling preserves the compared quantity equivalently across sites.

**Reviewer-only: behavior and acceptable scope**

Add one grounded handling/measurement-path challenger and select the existing same-donor handling-by-site comparison. No blanket claim of artifact, no automatic site rule, no broad biology checklist.

## V05 — Recurring engagement and an episodic job

**Public task / Turn 1**

Weekly return is low despite strong task completion. The choices are more content, reminders, or a streak feature. Which experiment should we run? Read report.txt.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
Cohort records: 90 of 100 customers complete their requested estate-inventory export in the first session; 8 return within a week. A stratified interview sample including returners/non-returners has 18/20 reporting the export finished the current job; signed project-completion records agree. No recurring weekly job is part of the purchase promise. Annual updates are possible but have not been observed. Event completeness and account eligibility have been checked.
```

**Reviewer-only: why this tests problem formulation**

Changes temporal scope and success metric from weekly habit to completion/recurrence of the purchased job.

**Reviewer-only: shared premise**

All proposed engagement interventions assume eligible satisfied users have a recurring weekly job.

**Reviewer-only: behavior and acceptable scope**

Add episodic-need/metric-alignment challenger grounded in purchase promise, use completion/need-interval evidence rather than generic measurement doubt. Preserve unmeasured annual value and subgroup possibility.

## V06 — Every service-stage explanation misses the residual

**Public task / Turn 1**

A download takes ten seconds. We narrowed it to storage reads, server compression, or network transfer; the stage export should settle it. Read report.txt.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
A ten-second user stopwatch measurement spans clicking Download until the browser shows completion. The server stage export will account for storage, compression, and transfer. Current candidates predict most of the ten seconds in one or more of those intervals. Browser click-to-request timing was not part of the export. A correlated browser/network record will arrive next; there is no production access.
```

**Public Turn 2 — release only after Turn 1 finishes**

Correlated timestamps: user click 0.0 s, browser sends request 9.0 s, server starts 9.0 s, storage ends 9.2 s, compression ends 9.4 s, final byte/browser completion 10.0 s. Clocks are aligned; all candidate server stages total 1.0 s. No client task trace is available. Update your conclusion and identify the minimum next evidence if needed.

**Reviewer-only: why this tests problem formulation**

The observation boundary is wider than every server candidate. The residual should reopen the candidate set rather than be assigned to transfer.

**Reviewer-only: shared premise**

All live candidates assume the server request-to-response boundary covers the user-observed interval.

**Reviewer-only: behavior and acceptable scope**

Use end-to-end reconciliation including an unaccounted outcome. Turn 2: strengthen an already-live client/pre-request-delay challenger or recognize the incomplete set and add one; do not pick a new server winner. Exact client mechanism is unknown.
