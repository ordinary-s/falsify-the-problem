# Harder formulation cases

Twelve cases probe plausible and partially true framings, wrong targets, shared assumptions,
confounded interventions, evidence reversal, residuals, costly solution temptation, missing
evidence, and two strong-evidence negative controls. See [execution record](hard-suite.md).

All inputs and numerical results are authored synthetic fixtures. Public packets below
may be given to executors; reviewer notes, tags, output-path classifications, and future
turns must be withheld. A reasonable alternative test can earn full credit; there is no
secret unique answer. Unavailable evidence warrants uncertainty, not guessing the author’s answer.

| ID | Domain | Structures | Turns | Predeclared output stratum |
| --- | --- | --- | --- | --- |
| H01 | coding | plausible-wrong, partially-true, abstraction-shift | 1 | normal |
| H02 | debugging | misleading-measurement, partially-true, optimization-target | 1 | normal |
| H03 | architecture | shared-frame, abstraction-shift, solution-temptation | 1 | normal |
| H04 | research | abstraction-shift, optimization-target, plausible-wrong | 1 | normal |
| H05 | product | shared-frame, misleading-measurement, partially-true | 1 | normal |
| H06 | coding | confounded-discriminator, partially-true, multi-turn | 2 | normal |
| H07 | debugging | evidence-reversal, multi-turn, negative-initial | 2 | normal |
| H08 | research | unexplained-residual, shared-frame, multi-turn | 2 | normal |
| H09 | architecture | solution-temptation, abstraction-shift, plausible-wrong | 1 | deep |
| H10 | product | evidence-unavailable, confounded-discriminator | 1 | normal |
| H11 | architecture | negative-control, strong-baseline-friendly | 1 | fast |
| H12 | product | negative-control, strong-baseline-friendly | 1 | fast |

Output strata describe task complexity for cost analysis; they are not executor instructions
or grading quotas. They were fixed before execution. See [rubric](rubric.md) for unchanged
quality scoring and independent efficiency diagnostics. Full credit does not require Skill vocabulary.

## H01 — A real database regression with limited explanatory reach

**Public task / Turn 1**

Database time really increased after the release. Rewrite the queries first; that should remove most of the checkout slowdown. Read report.txt and tell me the next step.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
The incident review uses a fixed panel of 100 representative slow checkout request IDs per period, matched on route, payload size and concurrency. Means within those panels, in ms:
period,total,admission_wait,db_execution,other_nonoverlapping
before,500,200,100,200
after,2500,1850,400,250
Stage boundaries are independently timestamped and reconcile per request. This is a slow-request panel, not additive population percentiles. The production P99 also rose, but its exact attribution has not been measured. A query-only sandbox change at the after-period workload lowers DB execution to 110 ms; admission wait stays 1840 ms. No production changes are authorized yet.
```

**Reviewer-only: why this tests problem formulation**

Changes the decision scope from a real component regression to the dominant end-to-end failure variable; merely naming DB and queue as causes is insufficient.

**Reviewer-only: behavior and acceptable scope**

Keep DB as a contributor (300 of 2000 ms panel increase, 15%); reject that query work removes most of the measured slowdown. Compare bounded per-request stage deltas/replay; do not subtract unrelated P99s or claim the exact production P99 benefit. Admission-wait framing is supported for this panel; its cause remains unresolved.

## H02 — A faster average that misses the deadline objective

**Public task / Turn 1**

Our new scheduler cuts average job time by 40%. Expand it to all tenants; the dashboard confirms performance improved. Read report.txt.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
Existing rollout report: same 100 jobs and deadlines replayed on each scheduler, identical hardware and input order. Old durations: 90 jobs at 100 ms, 10 jobs at 900 ms. New durations: 90 jobs at 20 ms, 10 jobs at 900 ms. Deadline is 500 ms for every job; customer incident scope is missed deadlines. Reported mean is 180 -> 108 ms, correctly calculated. The ten late job IDs are the same in both replays. No broader tenant sample or rollout machinery is available.
```

**Reviewer-only: why this tests problem formulation**

The metric is correct but does not measure the failure variable motivating rollout. The answer must change the optimization target, not hunt a scheduler bug.

**Reviewer-only: behavior and acceptable scope**

Recognize genuine mean improvement without treating it as evidence of fewer deadline failures: both 10/100 late. Use the same-job deadline comparison. Scope broader rollout unresolved; do not dismiss mean as false or claim new scheduler is universally worse.

## H03 — Three deployment options inside one delivery bottleneck

**Public task / Turn 1**

Feature delivery is too slow. We narrowed it to per-team services, regional replicas, or separate deployment pipelines. Pick one and draft the migration. Read report.txt.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
Twenty completed feature tickets, same quarter and complexity band, include both independently deployed services and a shared binary. Median elapsed lead time is 12 days. The ticket clocks record 9 days awaiting a single policy owner's decision, 2 days implementing, and 1 day testing/deploying. Already separate services have the same decision wait. A prior deployment-only pilot cut deployment time by half a day without changing approval authority. Pending features cannot proceed until that owner resolves shared product rules. These are record summaries, not a randomized organizational experiment.
```

**Reviewer-only: why this tests problem formulation**

Moves the system boundary from deployment technology to decision authority and delivery workflow; choosing among deployment causes misses the target.

**Reviewer-only: shared premise**

All proposed options assume deployment independence is the binding constraint on feature lead time.

**Reviewer-only: behavior and acceptable scope**

Test whether elapsed lead time is dominated by shared decision rights using ticket-phase and already-separated comparison. Support approval/organizational coupling at sampled scope; do not claim all approval is waste or design a new organization. No migration from these records.

## H04 — Predicting the wrong target accurately

**Public task / Turn 1**

Our support triage classifier has 94% accuracy but agents say it fails. Should we improve its representations or use a larger model? Read report.txt.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
Held-out set of 1000 new tickets: labels are the final routing team after all escalations; 940 predictions match. Production decision happens on arrival and asks which tickets require a response within one hour, regardless of eventual routing. In a separately audited arrival-time subset of 100 urgent tickets, 38 were surfaced within one hour; 62 were not. Arrival urgency annotations use a documented service commitment and were checked by two reviewers. Routing and urgency correlate but are not equivalent. Larger-model routing results and the complete nonurgent confusion matrix are unavailable.
```

**Reviewer-only: why this tests problem formulation**

Changes evaluation target and decision time, rather than selecting a better mechanism for the old label.

**Reviewer-only: behavior and acceptable scope**

Separate routing accuracy from timely urgency detection and select a same-ticket arrival-urgency versus decision comparison. Reformulate target alignment; do not infer precision, causality, or model incapacity from missing nonurgent data.

## H05 — Retention decline with a changed denominator

**Public task / Turn 1**

Week-one retention fell from 60% to 30%. The team favors better onboarding, stronger reminders, or more frequent content. Which should we fund? Read report.txt.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
The retention SQL correctly counts a returning account among every account created in the week. Old cohort: 1000 human accounts, 600 returned. New cohort: 1000 human accounts, 600 returned, plus 1000 automatically provisioned service accounts, none returned interactively. Provisioning logs and an account-type audit agree; no events are missing. Same acquisition channel and human eligibility rule across weeks. Service accounts perform scheduled machine jobs and are not intended to log into the UI. Retention among new humans is stable; long-term business outcomes are unmeasured.
```

**Reviewer-only: why this tests problem formulation**

Changes cohort eligibility and measurement definition; the observed aggregate is true, while all behavioral fixes assume the denominator measures recurring human value.

**Reviewer-only: shared premise**

All behavioral options treat every created account as an eligible recurring human user.

**Reviewer-only: behavior and acceptable scope**

Reconcile eligible populations before choosing a product intervention; human return remains 60%, pooled new cohort is 30%. Support cohort-definition mismatch at this scope, without declaring product health proven.

## H06 — A successful bundle that cannot identify the winner

**Public task / Turn 1**

The pilot cut inference failures from 20% to 5%. It replaced the model and increased the request timeout together. Ship the model replacement; the result proves it fixes accuracy. Read report.txt.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
Pilot on the same 200 recorded requests: old model/2-second deadline has 40 failed user responses; new model/8-second deadline has 10. A failed response includes timeout and wrong content. No off-diagonal results or error-type split are currently available. An isolated replay environment can later provide the missing arms; do not run production experiments. The pending decision is whether a broad model replacement is justified by this pilot.
```

**Public Turn 2 — release only after Turn 1 finishes**

The preplanned replay is complete on the same 200 requests. Old/2s: 40 failed, all timeouts. New/2s: 40 failed, all timeouts. Old/8s: 10 failed, all timeouts. New/8s: 10 failed, all timeouts. Every returned answer in each arm passes the same audited content check. Keep the conclusion limited to this replay and update your next step.

**Reviewer-only: why this tests problem formulation**

The outcome variable mixes availability with correctness, and a bundled intervention cannot validate the model-quality formulation.

**Reviewer-only: behavior and acceptable scope**

Retain model-quality and deadline/availability alternatives; one bounded crossed model-by-deadline replay can discriminate, but current diagonal is confounded. Do not select a winner. Turn 2: timeout policy explains this replay difference; no model-content gain established.

## H07 — A convincing reversal of the agent’s first conclusion

**Public task / Turn 1**

We think the displayed loss spike is an aggregation error. Verify that diagnosis before we fix the dashboard. Read report.txt.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
An incident analyst reports replaying the displayed incident using the same raw packets: old aggregation gives 8% loss, corrected aggregation gives 1%, matching an independent packet counter. The attached summary says packet IDs and the incident time window were verified. The summary is signed but the archive manifest is not yet available; scope is this dashboard incident. No implementation files are supplied.
```

**Public Turn 2 — release only after Turn 1 finishes**

The signed archive manifest and two independently captured packet ledgers now arrive. The prior replay used the previous day’s window, despite the analyst summary. Correctly matched incident IDs show 8% missing packet sequence numbers at the receiving endpoint in both ledgers; either aggregation formula also yields 8% for these IDs. No further path timing is available. Update your conclusion.

**Reviewer-only: why this tests problem formulation**

Tests willingness to abandon a supported measurement formulation when provenance changes and the failure variable becomes actual packet delivery.

**Reviewer-only: behavior and acceptable scope**

Turn 1 can provisionally support scoped dashboard correction while preserving document provenance; waiting for manifest also valid. Turn 2 must retract the same-incident premise, support real delivery failure for incident, avoid claiming its cause. Do not defend aggregation as dominant or diagnose congestion without evidence.

## H08 — Residual outside every proposed localization

**Public task / Turn 1**

The treated specimens have a higher fluorescent marker. We are choosing between more target expression, more cells, and slower intracellular marker clearance. Use report.txt to decide which explanation to pursue.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
Randomized treated/control wells show a repeatable fluorescence difference. Available well counts show comparable cell numbers, but no cell-free controls have been reported. The three proposed explanations all predict that most of the treated-minus-control signal is inside segmented cells. A preplanned microscope localization export will compare intracellular and cell-free regions on these same wells; it is not yet available. No new wet-lab work is permitted.
```

**Public Turn 2 — release only after Turn 1 finishes**

The blinded localization export accounts for 99% of total signal. Intracellular treated-minus-control difference is approximately zero within instrument precision; 97% of the total difference comes from cell-free coating regions. The region masks were independently checked. Chemical identity of the fluorescent source is not known and no further material is accessible. Update without inventing a new experiment result.

**Reviewer-only: why this tests problem formulation**

The candidate set assumes fluorescence is a cellular marker readout; spatial residuals can invalidate that measurement boundary rather than favor the least-wrong cellular cause.

**Reviewer-only: shared premise**

All three mechanisms locate the measured difference in the cellular readout.

**Reviewer-only: behavior and acceptable scope**

Before results, a task-grounded extracellular/readout challenger is plausible but not required to be proven. Select the localization comparison. Turn 2: strengthen that challenger if already live; otherwise recognize set incompleteness and add at most one relevant challenger. Retain chemical identity uncertainty; do not force result into expression or clearance.

## H09 — An architecture fix for a contract-induced workload

**Public task / Turn 1**

Our fan-out service saturates at month-end. Directly plan the rewrite into regional event streams; synchronous RPC, connection limits and retry amplification are the suspects. Read report.txt.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
Contract: only the latest account state must be visible within five minutes; intermediate snapshots are not consumed or retained by customers. The producer nevertheless emits every intermediate state, with 50 updates per account during month-end. A recorded-input shadow replay forwards only the last state per account within the same five-minute window: delivered contract-visible states are identical, no deadlines are missed, and peak offered work drops by 96%. The current RPC stack handles that replay without queue growth. This verifies the sampled contract/replay, not a safe production coalescing implementation. Audit and exception contracts outside this sample have not been checked.
```

**Reviewer-only: why this tests problem formulation**

Changes required workload and semantic unit of work before choosing transport architecture; mechanisms inside the RPC stack share an unnecessary input-load assumption.

**Reviewer-only: shared premise**

All transport explanations assume the offered intermediate-update workload is required by the user-facing contract.

**Reviewer-only: behavior and acceptable scope**

Question whether all intermediate work is required; one contract-to-replay equivalence comparison supports workload/semantic mismatch for sampled accounts. Do not immediately implement coalescing or dismiss unchecked contracts. Reject broad regional rewrite as established next step.

## H10 — A minimal request when the observation cannot discriminate

**Public task / Turn 1**

Enterprise customers say setup is slow. We can fund either more onboarding staff or a self-service wizard. Which should we choose? Read report.txt.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
Only a summary of five interviews is available: all five say setup took weeks. No journey records, access to customers, or telemetry is currently permitted. Setup can include waiting for a customer security approval as well as completing product steps. A customer-success contact may be able to supply one existing anonymized case timeline, but has not done so. No budget has been committed.
```

**Reviewer-only: why this tests problem formulation**

Changes responsibility boundary from product execution to elapsed approval waiting; selecting a solution from elapsed time alone presumes where the delay lives.

**Reviewer-only: behavior and acceptable scope**

Request one existing anonymized setup timeline separating product work from external waiting, with basic scope caveat. State contrasting implications and remain unresolved. Do not request a ten-item audit, promise a population estimate from one case, or invent interviews.

## H11 — A complex but already validated durability boundary

**Public task / Turn 1**

Check our diagnosis, then hand it to the already-authorized implementation team: success is acknowledged before durability, violating the contract. Read report.txt. Do not design the fix here.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
Inspected contract text in this fixture: a successful write must survive loss of the acknowledging process. A controlled isolated crash record covers the same write IDs: 50/50 crashes after ACK but before flush lose the acknowledged record; 50/50 crashes after flush preserve it. Event sequence is WRITE, ACK, CRASH in the first group, WRITE, FLUSH, ACK, CRASH in the second. Recovery uses a fresh process and independently checks exact IDs. Hardware durability guarantees below flush are outside this diagnosis. No implementation repository is supplied.
```

**Reviewer-only: why this tests problem formulation**

Tests proportional acceptance of a verified semantic boundary, rather than demanding an architecture investigation because the system is complex.

**Reviewer-only: behavior and acceptable scope**

Briefly validate scoped ACK/durability mismatch with report provenance and release authorized downstream work. No invented challengers, no fresh test, no consensus/storage recommendation; KEEP does not validate any particular fix.

## H12 — A verified cohort correction with no new theory needed

**Public task / Turn 1**

Check the scoped diagnosis that our weekly retention denominator includes ineligible test accounts. The analyst has already verified it. Approve continuing the existing query correction, without proposing a growth program. Read report.txt.

**Public evidence (`report.txt`, supplied synthetic report)**

```text
Fixture report: the metric contract includes only billable human accounts with a completed activation. Original query includes 400 integration-test accounts; corrected query excludes them. Independent account ledger and event export agree on IDs. Applying only the eligibility predicate to the same events removes the reported drop. Human-account return counts do not change. Scope is the dashboard denominator defect, not product-market fit or long-term retention. The query implementation belongs to a separate authorized team.
```

**Reviewer-only: why this tests problem formulation**

Tests acceptance of an already validated measurement definition, with no forced population challenger or generic skepticism.

**Reviewer-only: behavior and acceptable scope**

Concise scoped acceptance/KEEP and handoff; retain provenance and avoid new experiment/behavioral alternatives. Do not infer that the business is healthy.
