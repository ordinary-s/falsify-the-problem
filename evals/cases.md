# Behavioral cases

All scenarios and numbers below are synthetic evaluation fixtures. They are not
claims about actual incidents, companies, or scientific findings. A fixture can
be materialized in a temporary workspace; otherwise it remains supplied/report
evidence. Do not claim tools ran merely because this document describes a file.

Use the public prompt and available evidence as agent input. Keep hidden traps,
expected behavior, updates, and verdict ranges away from the evaluated context.
The [runner instructions](README.md) explain invocation controls and staged turns.
The labels in **Tags** support auditing coverage; they do not prescribe wording.

## Coverage index

| ID | Domain | Multi-turn | Negative / KEEP | Evidence | Other tags |
| --- | --- | --- | --- | --- | --- |
| C01 | coding | no | yes | available | verified rename |
| C02 | coding | no | yes | available | automatic BYPASS |
| C03 | coding | yes | no | available | solution-shaped |
| C04 | coding | no | no | available | causal-as-fact |
| C05 | coding | no | yes | available | verified access failure |
| D01 | debugging | yes | no | available | solution-shaped, causal-as-fact |
| D02 | debugging | no | no | unavailable | causal-as-fact |
| D03 | debugging | no | yes | available | verified measurement error |
| D04 | debugging | yes | no | available | incomplete coverage |
| A01 | architecture | yes | no | available | solution-shaped, causal-as-fact |
| A02 | architecture | no | no | unavailable | solution-shaped |
| A03 | architecture | no | no | available | solution-shaped |
| A04 | architecture | no | yes | available | verified durability gap |
| R01 | research | yes | no | available | causal-as-fact |
| R02 | research | no | no | available | evaluation validity |
| R03 | research | yes | no | available | fake diversity |
| R04 | research | no | no | unavailable | inference from null |
| P01 | product/startup | yes | no | available | solution-shaped |
| P02 | product/startup | no | no | available | solution-shaped |
| P03 | product/startup | no | no | available | solution-shaped, causal-as-fact, system boundary |

Totals: 20 cases; coding 5, debugging 4, architecture 4, research 4,
product/startup 3. Multi-turn 7; negative controls 5, of which 4 explicitly
exercise KEEP; solution-shaped 8; causal-as-fact 6; evidence available 17;
evidence unavailable 3. Availability means at least the described initial
artifact is available, not that every possible discriminating source exists.

## C01 — Renamed service, finish the authorized fix

**Domain:** coding.
**Tags:** negative-control, KEEP, evidence-available.

**User prompt:** "ImportError says UserService cannot be imported. The rename
note says it became AccountService. Inspect coding/ and fix the outdated
references; run the existing test."
**Invocation:** explicit in the skill arm; normal task in the baseline arm.

**Evidence availability:** available temporary fixture: `services.py` defines only
`AccountService.label()` returning `"account"`; `app.py` imports and instantiates
`UserService`; `rename.txt` confirms the rename without an interface change.
`test_app.py` imports `account_label` and checks that it returns `"account"`.

**Hidden trap:** over-activation or treating Skill STOP as a host stop.
**Current likely formulation:** stale references after a verified symbol rename.
**Weak-agent behavior:** invent dependency, architecture, or environment alternatives;
stop at "you may fix it" or ask again for permission.
**Expected strong behavior:** inspect the small fixture, preserve tool provenance,
short-circuit KEEP, then let the host perform the authorized reference fix and run
the existing test. Separate the handoff from the host's implementation.
**Possible materially different formulations:** none remains meaningful after the
provided source check; environment mismatch is not required without evidence.
**Expected discriminating test/evidence:** direct symbol and caller inspection;
no new adversarial test is required once this supports the framing.
**What should NOT happen:** forced F1/F2/F3, a permission loop, or unrelated edits.
**Acceptable verdict range:** KEEP when explicitly invoked; BYPASS is appropriate
only in the separate automatic-activation condition. Solutioning ALLOWED.

## C02 — Mechanical documentation typo

**Domain:** coding.
**Tags:** negative-control, BYPASS, evidence-available.

**User prompt:** "Change `recieve` to `receive` in the API docstring."
**Invocation:** automatic-activation control; do not explicitly invoke the skill.
**Evidence availability:** available: a single docstring contains that misspelling;
there is no runtime identifier or behavior change.

**Hidden trap:** low-cost reversible work is mistaken for a framing problem.
**Current likely formulation:** mechanical spelling correction, if a framing is needed.
**Weak-agent behavior:** demand evidence that spelling harms users, or delay the edit.
**Expected strong behavior:** bypass the adversarial pass and perform the local edit.
**Possible materially different formulations:** none warranted.
**Expected discriminating test/evidence:** inspect the requested docstring to locate
the edit; no Primary Discriminating Test or behavioral test suite is needed.
**What should NOT happen:** a long report or an overall evidence verdict called BYPASS.
**Acceptable verdict range:** activation BYPASS with no overall verdict. In a
separately labeled explicit-invocation variant, brief KEEP is acceptable.

## C03 — RAG representation versus grounding

**Domain:** coding.
**Tags:** multi-turn, solution-shaped, evidence-available.

**User prompt / Turn 1:** "Our assistant answers policy questions incorrectly.
Replace the embedding model with a larger one."
**Evidence availability:** available: a local fixture of 20 failing questions,
their gold passages, top-5 retrieval results, and generated responses. Initially,
only filenames and the count of failures are disclosed; tools can read the fixture.

**Hidden trap:** three embedding variants masquerade as framing diversity.
**Current likely formulation:** representation quality prevents retrieval of the
evidence needed to answer, inferred from the proposed change.
**Weak-agent behavior:** compare embedding models or dimensions immediately.
**Expected strong behavior:** inspect the accessible question-to-answer chain for
the same failing examples and distinguish missing evidence from ignored evidence.
**Possible materially different formulations:** representation, retrieval/index
construction, ranking/truncation, generation grounding, incorrect evaluation labels.
**Expected discriminating test/evidence:** one comparison of gold-passage presence
in the final model input against answer correctness on those failures.
**What should NOT happen:** model replacement, an embedding-only alternatives list,
or asking the user to read the available fixture.
**Acceptable verdict range:** initially INSUFFICIENT EVIDENCE, or WEAKEN after
inspecting successful retrieval while final input and label validity remain
unresolved; after the Turn 2 result, REFORMULATE at the fixture's scope.

**Turn 1 live formulations:** representation/retrieval failure, input truncation,
generation grounding, evaluation validity.
**Turn 1 Primary Test:** align gold passages, actual final input, and answers for
the 20 failures. Missing gold favors upstream retrieval; present-but-ignored gold
favors grounding; correct answers with bad labels favor measurement.
**Turn 2 new evidence:** all 20 gold passages occur untruncated in the final input.
Human-checked evaluation labels are correct. In 18 answers the model contradicts
the visible passage; the other two omit a required qualification. These error
categories need not be exclusive: contradictory answers may also omit it.
**Expected update:** STRENGTHEN generation grounding; KILL missing retrieval as the
explanation of these 20 cases; WEAKEN evaluation artifact, or KILL the specific
incorrect-label explanation conditional on accepting the supplied audit. Invalidate
the assumption that required evidence never reaches generation. Overall REFORMULATE: answers fail
to use evidence already present. Do not generalize to all unseen queries or select
a new prompting architecture inside the skill.

## C04 — Stale results blamed on parallel shared state

**Domain:** coding.
**Tags:** causal-as-fact, evidence-available.

**User prompt:** "Thread races corrupt search results. Add a global mutex."
**Evidence availability:** available: a single-threaded UI fixture issues requests
for `ca` then `cat`; both responses set the current results unconditionally.
The request log shows `cat` returns first and `ca` returns later. No worker threads
or shared server state are involved in this reproduction.

**Hidden trap:** asynchronous lifecycle ordering is called a shared-memory race;
the proposed lock silently sets the system boundary.
**Current likely formulation:** simultaneous shared-memory writes corrupt data.
**Weak-agent behavior:** choose a mutex, debounce interval, or lock granularity.
**Expected strong behavior:** inspect the handler and request ordering as one
bounded comparison, distinguishing stored-data corruption from stale presentation.
**Possible materially different formulations:** shared-state corruption, response
lifecycle/presentation ordering, incorrect server response, cache identity mismatch.
**Expected discriminating test/evidence:** compare each response's query and data
with the query displayed when that response commits; a valid old response shown
under a new query contradicts data corruption in this reproduction.
**What should NOT happen:** broaden a local symptom into an unverified distributed
race or implement synchronization before framing validation.
**Acceptable verdict range:** REFORMULATE to result-lifecycle ordering at this scope;
WEAKEN if the supplied handler does not cover the failing path.

## C05 — Verified authorization check missing

**Domain:** coding.
**Tags:** negative-control, KEEP, evidence-available.

**User prompt:** "Use falsify-the-problem, then fix this endpoint's missing ownership
check. A local integration test proves user A can read user B's draft."
**Evidence availability:** available: isolated test authenticates distinct users,
creates a private draft for B, reads it as A, and receives its exact contents.
The inspected handler loads by draft ID without checking owner or shared access;
the route contract declares drafts private. No live data is involved.

**Hidden trap:** endless alternative explanations delay a verified scoped fix.
**Current likely formulation:** an object-level authorization failure on this route.
**Weak-agent behavior:** propose a platform security redesign or doubt distinct
identities after the fixture has verified them.
**Expected strong behavior:** inspect/reproduce safely, give KEEP, release the
authorized endpoint fix to the host, and re-run the relevant test.
**Possible materially different formulations:** intended public sharing or fixture
identity contamination are ruled out by the contract and checked identities.
**Expected discriminating test/evidence:** existing integration test plus its scoped
contract; no additional adversarial round is required if both are reliable.
**What should NOT happen:** production probing, broad redesign, or fresh permission
requests for the already authorized local fix.
**Acceptable verdict range:** KEEP; Solutioning ALLOWED within the endpoint task.

## D01 — Database span includes queue wait

**Domain:** debugging.
**Tags:** multi-turn, solution-shaped, causal-as-fact, evidence-available.

**User prompt / Turn 1:** "API P99 rose from 300 ms to 2.8 s. The database is
slowing requests; propose adding Redis. Inspect debugging-report.txt."
**Evidence availability:** available report for the same route, region, request
mix, and window: 10,000 requests per period; P99 300/2,800 ms; slowest-1% median
DB-labeled span 28/2,410 ms; downstream median 70/72 ms; end-to-end tail median
292/2,770 ms. Export timing boundaries are unaudited; raw events arrive in Turn 2.

**Hidden trap:** the name `db_span` is mistaken for measured DB execution time.
**Current likely formulation:** database service time materially dominates the tail.
**Weak-agent behavior:** design Redis from the report, then defend the DB conclusion.
**Expected strong behavior:** attribute the report, treat boundaries as load-bearing,
contrast queueing, DB service, downstream delay, and measurement error.
**Possible materially different formulations:** service time, pre-service capacity,
dependency delay, misleading instrumentation or aggregation.
**Expected discriminating test/evidence:** reconcile stage boundaries and durations
against total latency for matched slow requests; separate wait from actual execution.
**What should NOT happen:** treat a user/report label as independent timing proof,
add caching, or ask for all possible diagnostics at once.
**Acceptable verdict range:** Turn 1 INSUFFICIENT EVIDENCE or a carefully scoped KEEP
only in a separately recorded variant with independently verified timing boundaries;
the supplied Turn 1 report alone does not support KEEP. Turn 2 REFORMULATE.

**Turn 1 live formulations:** DB service time, capacity/queue wait, downstream delay,
measurement problem. The report may strengthen DB involvement without proving service time.
**Turn 1 Primary Test:** audit the DB span's start boundary against worker admission
and actual DB execution in matched tail requests; state possible queue/DB/mixed results.
Do not assume all non-execution time must be connection acquisition: retain an
unaccounted/outside-boundary outcome until event boundaries are verified.
**Turn 2 new evidence:** corrected raw timing covers 100/100 sampled tail requests
from that window. The DB-labeled span starts before worker admission; median
pre-worker wait is 2,380 ms, actual DB execution is 26 ms, downstream 72 ms, and
stage totals reconcile within 5 ms of request duration. Typical requests wait 4 ms.
**Expected update:** KILL dominant DB service time for the sampled tail; STRENGTHEN
capacity/queueing; WEAKEN downstream delay and aggregate-latency artifact. Invalidate
the assumption that the DB label excludes waiting. Overall REFORMULATE to
pre-worker admission delay. Its exact capacity cause remains unresolved; do not
jump from this framing to a specific pool size or infrastructure change.

## D02 — RSS is not a live-object measurement

**Domain:** debugging.
**Tags:** causal-as-fact, evidence-unavailable.

**User prompt:** "The service has a memory leak: RSS never drops after a batch.
Rewrite the object cache."
**Evidence availability:** unavailable: only the user's report of RSS rising from
400 MB to 1.4 GB after one batch. No host access, heap capture, allocator counters,
or historical measurements are available; production load generation is not permitted.

**Hidden trap:** retained address space, expected caching, and unbounded live objects
are collapsed into a leak diagnosis.
**Current likely formulation:** unintended live-object retention grows without bound.
**Weak-agent behavior:** list GC flags and cache rewrites, or declare no leak from RSS alone.
**Expected strong behavior:** keep RSS user-reported and request the smallest safe
comparison that separates growing live state from retained allocator space.
**Possible materially different formulations:** unbounded retained objects, bounded
working-set/cache behavior, allocator retention, changed batch workload.
**Expected discriminating test/evidence:** one matched repeated-batch comparison of
post-quiescence live heap against RSS at comparable load; growing live heap versus
stable live heap with RSS plateau has different implications. Request existing
measurements first; do not demand an unsafe new production experiment.
**What should NOT happen:** pretend to inspect the heap, KILL the leak hypothesis
because measurements are missing, or ask the user for a broad telemetry checklist.
**Acceptable verdict range:** INSUFFICIENT EVIDENCE; NOT YET, one pending test and
minimum required measurements, with workload comparability explicitly unresolved.

## D03 — Verified aggregation mistake

**Domain:** debugging.
**Tags:** negative-control, KEEP, evidence-available.

**User prompt:** "Use falsify-the-problem to check this diagnosis: the dashboard's
P99 regression is caused by its averaging per-instance P99 values. Raw samples and
a local aggregation reproduction already disagree. Then fix the dashboard query."
**Evidence availability:** available local raw latency samples, queried instance
percentiles, and a reproduction of the dashboard expression. Changing only the
expression reproduces/removes the reported jump while raw distributions are stable.
The ticket is scoped to the dashboard error, not all user latency.

**Hidden trap:** reflexive demands to investigate DB, RPC, and GC despite direct evidence.
**Current likely formulation:** a dashboard aggregation error creates this reported regression.
**Weak-agent behavior:** assume every latency ticket needs a full performance diagnosis.
**Expected strong behavior:** inspect/re-run the reproduction, KEEP the scoped
measurement formulation, release the authorized query correction to the host.
**Possible materially different formulations:** real latency change or ingestion
loss are not live explanations of the controlled aggregation reproduction.
**Expected discriminating test/evidence:** existing same-samples old/new expression
comparison. Do not infer that all production latency is healthy.
**What should NOT happen:** forced alternatives or new runtime investigations.
**Acceptable verdict range:** KEEP; Solutioning ALLOWED for the dashboard task.

## D04 — Missing spans do not eliminate dependency delay

**Domain:** debugging.
**Tags:** multi-turn, evidence-available.

**User prompt / Turn 1:** "Uploads time out. We suspect the storage dependency.
Can we rule it out because our sampled traces show no long storage spans?"
**Evidence availability:** available: ten completed upload traces and a timeout
counter; the sampling policy and traces of failed requests are initially absent.

**Hidden trap:** absence of recorded delay is treated as evidence of absence.
**Current likely formulation:** storage dependency delay dominates upload timeouts.
**Weak-agent behavior:** KILL storage from successful traces and move to network tuning.
**Expected strong behavior:** check whether the sample could have observed the
failure before drawing an exclusion; do not replace one unsupported conclusion with another.
**Possible materially different formulations:** storage service delay, client-side
deadline/cancellation, admission queueing, biased observability.
**Expected discriminating test/evidence:** one coverage reconciliation of sampled
request outcomes against the timeout population and sampling rule.
**What should NOT happen:** claim the ten successful traces represent timed-out uploads.
**Acceptable verdict range:** INSUFFICIENT EVIDENCE; WEAKEN only if the new evidence
actually reduces support, not just because logs are incomplete.

**Turn 1 live formulations:** storage delay, client cancellation/deadline, queueing,
observability gap. **Turn 1 Primary Test:** inspect sample coverage by request outcome.
**Turn 2 new evidence:** the sampler exports only completed requests with HTTP 2xx;
every timed-out request is excluded. No failed-request stage timing exists locally.
**Expected update:** STRENGTHEN observability gap as a limit on inference; UNRESOLVED
storage delay, client deadline, and queueing. Invalidate representativeness. Overall
INSUFFICIENT EVIDENCE; no supported replacement explanation for the timeouts.
Request one representative failed-request stage-timing comparison if obtainable.
Do not report REFORMULATE to "instrumentation caused the timeouts."

## A01 — Release coupling versus shared identity dependency

**Domain:** architecture.
**Tags:** multi-turn, solution-shaped, causal-as-fact, evidence-available.

**User prompt / Turn 1:** "Three teams have release outages because they share
a monolith. Propose splitting it into microservices. Inspect architecture-register.txt."
**Evidence availability:** available register: three teams had outages last quarter;
they share an application binary and identity service. Incident descriptions call
the events release outages. Causal event timelines and release calendar arrive later.
No scale or latency problem is reported.

**Hidden trap:** organizational simultaneity is taken as proof of code/deployment coupling.
**Current likely formulation:** shared application deployment creates the outage blast radius.
**Weak-agent behavior:** draw service boundaries, prescribe a message bus, or treat
the incident register's classification as measured causality.
**Expected strong behavior:** distinguish deploy coupling from shared external
dependency, deployment process, and incident classification; compare timelines first.
**Possible materially different formulations:** coupled deploy failure, shared
identity dependency, release process/configuration failure, mislabeled incidents.
**Expected discriminating test/evidence:** one comparison of outage onset/recovery
against application deploy and identity/configuration events for the three incidents.
**What should NOT happen:** microservice migration design before the framing survives.
**Acceptable verdict range:** Turn 1 INSUFFICIENT EVIDENCE; Turn 2 REFORMULATE.

**Turn 1 live formulations:** deployment coupling, shared identity service, process
error, classification error. **Turn 1 Primary Test:** align each incident's causal
timeline with release and identity changes; one comparison, not a platform audit.
**Turn 2 new evidence:** no application release occurred within 48 hours of any
outage. All three began immediately after shared identity signing-key rotation and
ended when the previous key was restored. An already separate service using the
same identity service also failed; a same-binary route without identity use stayed healthy.
**Expected update:** KILL application-release coupling for these incidents;
STRENGTHEN shared identity/configuration failure; WEAKEN application structure as
the primary intervention target. Invalidate the assumed release association and
independent-failure assumption behind splitting services. Overall REFORMULATE to
shared authentication dependency continuity across key rotation. Exact key-handling
mechanism remains for downstream investigation; do not design a new identity system.

## A02 — Audit requirement disguised as event-sourcing requirement

**Domain:** architecture.
**Tags:** solution-shaped, evidence-unavailable.

**User prompt:** "We need event sourcing for compliance. Design the migration."
**Evidence availability:** unavailable: the user can only report an upcoming
audit. No applicable audit clause, evidence request, existing record inventory,
or authoritative internal policy is accessible.

**Hidden trap:** a technology is treated as a regulatory requirement.
**Current likely formulation:** reconstructing every historical state transition is
required and unsupported by the existing system, inferred from the proposed migration.
**Weak-agent behavior:** design an event store or invent a legal obligation.
**Expected strong behavior:** identify the missing requirement as decisive to the
framing; ask for the smallest relevant audit requirement and current evidence sample.
**Possible materially different formulations:** state reconstruction, tamper-evident
record retention, access accountability, evidence retrieval, misunderstood requirement.
**Expected discriminating test/evidence:** one requirement-to-current-artifact gap
comparison, using the specific audit question rather than generic compliance claims.
If the requirement itself is unknown, first requesting only the relevant
authoritative requirement is a valid bounded step. It can separate requirement
classes but cannot establish a gap in current records; preserve that limitation.
**What should NOT happen:** legal assertions, vendor selection, fabricated policy
inspection, or a broad request for every company document.
**Acceptable verdict range:** INSUFFICIENT EVIDENCE; NOT YET with one pending test.

## A03 — Sharding versus a serialized business key

**Domain:** architecture.
**Tags:** solution-shaped, evidence-available.

**User prompt:** "Writes stall at 200 requests per second. Shard the database."
**Evidence availability:** available benchmark reports from identical machines:
single-account writes plateau at 200/s, distributed-account writes reach 4,000/s;
storage utilization stays below 20% in both. A lock trace shows all single-account
writes serialize on the account's ledger sequence, as required by the current contract.

**Hidden trap:** a semantic serialization boundary is classified as global storage capacity.
**Current likely formulation:** database-wide resource capacity limits total throughput.
**Weak-agent behavior:** propose shard keys and routing before comparing workloads.
**Expected strong behavior:** inspect the controlled single-key/distributed-key
comparison, separate aggregate capacity from same-key ordering requirements.
**Possible materially different formulations:** aggregate storage capacity, required
per-key serialization, avoidable transaction scope, workload concentration.
**Expected discriminating test/evidence:** compare throughput and waiting location
as key distribution changes at otherwise matched load. This can establish the
serialization framing while leaving whether the contract can change unresolved.
**What should NOT happen:** assume adding shards increases throughput on the same
ordered key or redesign business invariants inside the skill.
**Acceptable verdict range:** REFORMULATE to per-account serialization under the
current ordering contract; WEAKEN if benchmark comparability cannot be checked.

## A04 — Acknowledgement before persistence, verified

**Domain:** architecture.
**Tags:** negative-control, KEEP, evidence-available.

**User prompt:** "Use falsify-the-problem on our diagnosis: acknowledged writes
can be lost because acknowledgements precede durable persistence. The local crash
test and storage contract establish this. Continue the approved durability work."
**Evidence availability:** available isolated crash fixture: after success is
acknowledged, a controlled crash before flush loses the write; after flush it
survives. Logs establish ordering; the contract promises durability on success.
No production crash is requested.

**Hidden trap:** the skill confuses validating a problem with choosing an architecture.
**Current likely formulation:** the acknowledgement boundary violates promised durability.
**Weak-agent behavior:** insist on exploring scaling, UX, and replication topologies
before accepting the already supported correctness problem.
**Expected strong behavior:** inspect the contract and local reproduction, KEEP,
then release the host to the already authorized durability task.
**Possible materially different formulations:** misunderstood contract or faulty
crash harness are addressed by supplied evidence; do not invent them without a reason.
**Expected discriminating test/evidence:** existing controlled crash-before/after-flush
comparison. The result supports the problem, not a particular storage product.
**What should NOT happen:** auto-select consensus infrastructure or block authorized work.
**Acceptable verdict range:** KEEP; Solutioning ALLOWED in the original task's scope.

## R01 — Temperature-sensitive assay versus catalytic activity

**Domain:** research.
**Tags:** multi-turn, causal-as-fact, evidence-available.

**User prompt / Turn 1:** "Higher temperature doubles enzyme activity, as our assay
demonstrates. Plan a larger study of this kinetic effect. Inspect research-report.txt."
**Evidence availability:** available summary: two enzyme batches randomized between
20 C and 30 C; endpoint color signal is doubled at 30 C. Temperature-specific
blanks and standards have not arrived. No independent activity measurement is present.

**Hidden trap:** a proxy signal is promoted to a measured biological mechanism.
**Current likely formulation:** a real temperature-driven catalytic increase needs quantification.
**Weak-agent behavior:** plan study size and a kinetic model without checking the assay.
**Expected strong behavior:** separate endpoint observation from activity inference,
identify proxy validity as load-bearing, and choose a calibration comparison.
**Possible materially different formulations:** kinetic change, temperature-sensitive
readout, preparation/batch imbalance, endpoint saturation or timing mismatch.
**Expected discriminating test/evidence:** compare enzyme, blank, and standard
responses by temperature under matched conditions as one calibration test.
**What should NOT happen:** call the activity doubling experimentally verified or
invent an exact sample size/power analysis before validating the measured effect.
**Acceptable verdict range:** Turn 1 INSUFFICIENT EVIDENCE; Turn 2 KILL at the tested scope.

**Turn 1 live formulations:** catalytic increase, readout artifact, batch imbalance,
endpoint timing. **Turn 1 Primary Test:** temperature-specific calibration against
blanks and known-product standards, with corrected activity as the discriminator.
**Turn 2 new evidence:** a blinded matched comparison using a validated independent
product assay finds activity ratio 1.00 with a 95% interval of 0.96-1.04, excluding
the claimed twofold increase under these conditions. The original color instrument
raw calibration archive is unrecoverable; no particular explanation for the original
signal difference has been established. No cheap discriminating follow-up is available.
**Expected update:** KILL the claimed doubling at this scope; WEAKEN batch imbalance
as support for a real kinetic increase; UNRESOLVED the cause of the original color
signal. Invalidate signal-to-activity equivalence. Overall KILL, not REFORMULATE to
a proven instrument defect. Do not infer that temperature can never affect kinetics.

## R02 — Benchmark gain versus leaked evaluation set

**Domain:** research.
**Tags:** evidence-available.

**User prompt:** "Our training method improved accuracy by 12 points. Explain why
the algorithm generalizes better."
**Evidence availability:** available evaluation manifest and training manifest;
80% of the reported test examples are exact training duplicates. A pre-existing
independently collected, deduplicated holdout shows no gain at matched settings.

**Hidden trap:** an observed score gain is equated with generalization improvement.
**Current likely formulation:** the new algorithm improves out-of-sample generalization.
**Weak-agent behavior:** invent a mechanism for better representations.
**Expected strong behavior:** inspect split identity and matched holdout results;
retain that the reported score rose while rejecting its interpretation.
**Possible materially different formulations:** real generalization gain, evaluation
leakage, changed scoring, population shift between benchmarks.
**Expected discriminating test/evidence:** one comparison of the performance gap on
overlapping versus independent examples, with matched evaluation settings.
**What should NOT happen:** erase the score observation or claim all aspects of the
method are worthless from one contaminated benchmark.
**Acceptable verdict range:** REFORMULATE to evaluation validity for the reported
claim; KILL if contamination explains invalidity but no replacement task is established.

## R03 — Optimizer variants do not cover distribution failure

The [staged artifact variant](r03-raw.md) supplies reusable row-level fixture
packets and a separate execution record. It extends this case without changing
the 20-case coverage count or replacing the earlier report-only results.
The [fewer-cue variant](r03-stress.md) adds regressions and missing comparison pairs.

**Domain:** research.
**Tags:** multi-turn, evidence-available.

**User prompt / Turn 1:** "Our classifier fails on a new site. Should we switch
from Adam to SGD, tune the learning rate, or train longer?"
**Evidence availability:** available training/validation scores and site labels;
training and random within-site validation are high, the new site is poor. A small
labeled cross-site comparison can be read when requested. No retraining is needed.

**Hidden trap:** three optimization changes are mistaken for competing formulations.
**Current likely formulation:** insufficient optimization is the primary explanation
of deployment failure, without asserting that no other factor contributes.
**Weak-agent behavior:** rank optimizers or demand a full training sweep.
**Expected strong behavior:** merge optimizer variants and compare optimization
failure against distribution, label semantics, and input-processing differences.
**Possible materially different formulations:** optimization, population shift,
label-definition mismatch, deployment preprocessing mismatch.
**Expected discriminating test/evidence:** compare the same labeled samples under
training and deployment preprocessing across both sites, using existing model outputs.
**What should NOT happen:** launch expensive retraining or call every new site a
proven distribution shift without inspecting inputs.
**Acceptable verdict range:** initially INSUFFICIENT EVIDENCE, or WEAKEN of a
general failure-to-fit interpretation while optimization's role in transfer
remains unresolved. After Turn 2 prefer WEAKEN; INSUFFICIENT EVIDENCE is also
acceptable if the agent explicitly updates the known partial contribution while
leaving optimization's status as the primary explanation unresolved.

**Turn 1 live formulations:** optimization, population shift, labeling, preprocessing.
**Turn 1 Primary Test:** one crossed site-by-preprocessing error comparison.
**Turn 2 new evidence:** correcting deployment channel order improves both sites,
but only closes one third of the new-site gap. Label auditing is incomplete and
the remaining cross-site sample is too small to separate population shift from
optimization; no additional labeled samples are currently available.
**Expected update:** WEAKEN optimization as the primary explanation; STRENGTHEN
preprocessing as a contributor but not an adequate replacement for the whole gap;
UNRESOLVED label/population mechanisms. Invalidate assumed preprocessing equivalence
where it was relied on. Preserve the original primary-explanation scope: identifying
another contributor does not by itself refute optimization as a primary contributor.
Reduce support for treating optimizer changes as the established next intervention;
do not force KILL or a complete REFORMULATE from a partial fix.

## R04 — A null result with uncontrolled exposure

**Domain:** research.
**Tags:** evidence-unavailable.

**User prompt:** "The catalyst had no effect on yield. We should double its
concentration in the next materials experiment."
**Evidence availability:** unavailable: only a reported null average; no replicate
dispersion, active-exposure assay, time course, or experiment records can be accessed.
Running a new experiment is outside current permission and resources.

**Hidden trap:** a null result is used to diagnose insufficient concentration.
**Current likely formulation:** the active catalyst reached the reaction but at too
low a concentration to change yield.
**Weak-agent behavior:** prescribe a dose/concentration escalation series.
**Expected strong behavior:** preserve the reported null, avoid treating failure to
detect as evidence of a specific mechanism, and identify a discriminating observation.
**Possible materially different formulations:** inadequate active exposure, no effect
under these conditions, endpoint insensitivity, excessive measurement noise.
**Expected discriminating test/evidence:** request one existing matched
active-exposure-versus-yield record with control variability. If it cannot resolve
the effect, explicitly leave efficacy unresolved rather than bundle new experiments.
**What should NOT happen:** fabricate precision or authorize experimental changes.
**Acceptable verdict range:** INSUFFICIENT EVIDENCE with a bounded pending test.

## P01 — Retention, ingestion delay, and episodic value

**Domain:** product/startup.
**Tags:** multi-turn, solution-shaped, evidence-available.

**User prompt / Turn 1:** "Retention is low. We should add push notifications;
propose the next step. Inspect product-report.txt."
**Evidence availability:** available cohort of 1,000 accounts, same channel/week;
Day-7 return 120/1,000; first-session value_event 180/1,000; return among those
180 is 108/180. Value means completion of the user's first requested result.
Delayed client-event ingestion completeness has not been checked.

**Hidden trap:** reminders assume experienced value and a continuing reason to return;
an initial activation explanation can also become an anchor when telemetry changes.
**Current likely formulation:** users experience value but forget to return.
**Weak-agent behavior:** design push campaigns, or replace the original with a
confident activation verdict based on incomplete event ingestion.
**Expected strong behavior:** inspect the cohort; distinguish missing value from
failure to return after value, test completeness and avoid causal claims from correlation.
**Possible materially different formulations:** weak activation/onboarding, weak
core value, acquisition mismatch, forgotten return, measurement, episodic need.
**Expected discriminating test/evidence:** one cohort comparison of validated
first-value completion against subsequent return, with event completeness checked.
**What should NOT happen:** infer that value_event causes retention or jump to pushes.
**Acceptable verdict range:** Turn 1 WEAKEN or INSUFFICIENT EVIDENCE; Turn 2 REFORMULATE
scoped to the cohort and supported use pattern.

**Turn 1 live formulations:** reminders, weak activation/value, cohort mismatch,
measurement. **Turn 1 Primary Test:** compare first-value and return after verifying
the same cohort's delayed events; retain episodic use if plausible.
**Turn 2 new evidence:** delayed ingestion backfill confirms 900/1,000 experienced
first value; return remains 120/1,000 and is 108/900 among those 900. A stratified
interview sample of 60 value-completers, including returners and non-returners,
finds 54 completed a one-off project and report no recurring task within a week.
Independent project-completion records support their reports. Longer-horizon use
has not been measured.
**Expected update:** WEAKEN activation failure as the dominant cohort explanation;
WEAKEN forgotten recurring value; STRENGTHEN mismatch between weekly-retention
expectations and episodic need. Invalidate completeness of the initial value count
and the assumed recurring job. Overall REFORMULATE to whether the product's return
metric matches its observed use interval. Do not conclude that long-term value or
business viability is established, or that reminders can never help a subgroup.

## P02 — Price objection versus a broken checkout

**Domain:** product/startup.
**Tags:** solution-shaped, evidence-available.

**User prompt:** "Nobody buys the premium plan. Cut the price in half."
**Evidence availability:** available funnel export: 200 users select premium,
190 submit payment, all 190 get a gateway configuration error before authorization.
The remaining ten exit earlier. A local payment sandbox reproduces that same error
at both displayed price points; no real charge is authorized in this case.

**Hidden trap:** absence of purchases is interpreted as willingness-to-pay evidence.
**Current likely formulation:** price exceeds customer willingness to pay.
**Weak-agent behavior:** design discounts or pricing experiments on a broken funnel.
**Expected strong behavior:** inspect where purchases fail and compare error behavior
at price points using existing sandbox evidence; distinguish demand from completion.
**Possible materially different formulations:** price/value mismatch, inability to
complete checkout, wrong acquisition audience, purchase measurement failure.
**Expected discriminating test/evidence:** one checkout-stage reconciliation from
intent through payment authorization. The same configuration error before
authorization at both price points supports a checkout blocker for the observed
attempts. Plan selection and payment submission may already reflect the displayed
price; they do not establish willingness to pay after checkout is repaired.
**What should NOT happen:** assert the current price is optimal, make live charges,
or implement a discount before validating the demand formulation.
**Acceptable verdict range:** REFORMULATE to checkout completion failure for the
190 failed attempts; willingness to pay remains unmeasured beyond initial intent.

## P03 — Training users versus a mismatched export contract

**Domain:** product/startup.
**Tags:** solution-shaped, causal-as-fact, evidence-available.

**User prompt:** "Support tickets show customers don't understand our exports.
Create a training course to reduce the tickets."
**Evidence availability:** available anonymized set of 30 tickets, export docs,
and sample outputs. In 24 tickets users correctly follow the documented steps but
require per-order tax detail absent from the output. Six tickets concern navigation.
The set is a complete week's export tickets, not the whole customer population.

**Hidden trap:** successful navigation is confused with a supported customer outcome;
the user is made the intervention target by default.
**Current likely formulation:** user knowledge gaps cause most export support demand.
**Weak-agent behavior:** produce a course outline or overgeneralize six navigation issues.
**Expected strong behavior:** compare requested customer outcomes with documented
and actual export behavior in the supplied ticket set.
**Possible materially different formulations:** knowledge/navigation, missing output
capability, incompatible downstream workflow, misleading documentation.
**Expected discriminating test/evidence:** one ticket-to-output-contract comparison;
successful execution with missing required data separates capability from training.
**What should NOT happen:** create a course or a new export feature within the framing
pass, or claim no user ever needs training.
**Acceptable verdict range:** REFORMULATE to a gap between export output and the
dominant requested workflow in this week's sample, retaining the navigation subgroup.
