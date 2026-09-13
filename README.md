# falsify-the-problem — An Agent Skill for Problem Framing

English | [简体中文](README.zh-CN.md)

> Stop solving the wrong problem faster.

An open-source Agent Skill for problem framing and assumption testing across
coding, debugging, architecture, scientific research, and product decisions.
It asks **Are we solving the right problem?** before proposing solutions.
Start with [installation](#installation) and a [first invocation](#first-invocation-in-codex-cli-or-the-ide-extension).

**Illustrative scenarios, not production incidents or measured results:**

| Before | After |
| --- | --- |
| "API P99 rose from 300 ms to 2.8 s. Add Redis." -> design a cache | Attribute the reported latency, test whether database time actually dominates the slow tail, then keep or replace that framing |
| "The experiment underperformed. We need a stronger model." -> increase model capacity | Compare the same saved inputs through training and evaluation preprocessing, holding the model and scoring fixed; test whether an input-path mismatch contributes before attributing the result to model capability |
| "Retention is low. Add push notifications." -> build reminders | Test whether users experienced value and forgot to return, or never experienced value in the first place |

One Markdown file. No dependency, API key, server, or database. The distinctive
focus is a falsifiable framing, materially different alternatives, one primary
discriminating test per investigation round, evidence updates, and an explicit
handoff before solution design. `KEEP` is a successful result.

## Installation

The complete runtime artifact is [SKILL.md](SKILL.md). Evaluation files are
development materials, not dependencies. The skill itself needs no package,
API key, or service; your host agent has its own setup requirements.

### Codex: choose an installation scope

Codex is one way to use this cross-domain skill. According to the
[official skills documentation](https://learn.chatgpt.com/docs/build-skills),
local skills can live in either of these locations:

| Scope | Folder containing `SKILL.md` | Available to |
| --- | --- | --- |
| Project | `<project>/.agents/skills/falsify-the-problem/` | Codex sessions in that project |
| User | `~/.agents/skills/falsify-the-problem/` | Codex sessions across your projects |

Choose one scope. Run the commands below in a **terminal**, not in the Codex
prompt. Git must be installed. Project commands start in the root of the project
where you want to use the skill; user commands can start in any directory.
These commands clone into a new folder and will fail if the destination is
already populated. Keep an existing installation instead of overwriting it.

**Windows PowerShell, project scope:**

```powershell
New-Item -ItemType Directory -Force -Path .agents/skills | Out-Null
git clone https://github.com/ordinary-s/falsify-the-problem.git .agents/skills/falsify-the-problem
```

**Windows PowerShell, user scope:**

```powershell
$skillRoot = Join-Path $env:USERPROFILE '.agents/skills'
New-Item -ItemType Directory -Force -Path $skillRoot | Out-Null
git clone https://github.com/ordinary-s/falsify-the-problem.git (Join-Path $skillRoot 'falsify-the-problem')
```

**macOS / Linux, Bash or Zsh, project scope:**

```bash
mkdir -p .agents/skills
git clone https://github.com/ordinary-s/falsify-the-problem.git .agents/skills/falsify-the-problem
```

**macOS / Linux, Bash or Zsh, user scope:**

```bash
mkdir -p "$HOME/.agents/skills"
git clone https://github.com/ordinary-s/falsify-the-problem.git "$HOME/.agents/skills/falsify-the-problem"
```

Alternatively, download or clone this repository elsewhere and copy only
`SKILL.md` into the chosen `falsify-the-problem` folder. Codex detects skill
changes automatically; restart it if the skill does not appear. In Codex CLI
or the IDE extension, use `/skills` or type `$` to select the skill.

### First invocation in Codex CLI or the IDE extension

Paste this into the **Codex prompt**, not PowerShell or a shell:

```text
$falsify-the-problem
Our API has become slower and we are considering a cache.
Inspect the available evidence, distinguish observations from assumptions,
and test the problem framing before proposing a solution.
```

The local setup commands do not establish skill activation or model behavior.
macOS and Linux installation and cross-host behavior have not been verified in
this documentation change. See [Usage](#usage) for ordinary-language examples.

### Other hosts

1. Download or clone this repository into a local `falsify-the-problem` folder.
2. For a host with skill-folder support, place the folder containing `SKILL.md` in
   that host's documented skill location and use its normal reload/discovery procedure.
   You can copy just `SKILL.md` into a folder of the same name.
3. For a host that accepts reusable Markdown instructions, attach or load the
   complete `SKILL.md` and explicitly request its use before solving the task.

Paths, discovery, invocation syntax, and tool permissions are host-specific. The
skill is designed to be portable across agents that support reusable Markdown
instructions or skill-like workflows; identical behavior across hosts is not guaranteed.

## Why

A requested solution often contains an untested definition of the problem.
Optimizing that solution can make the wrong investigation expensive.
This skill exposes the definition and seeks cheap evidence that could overturn it.
It is useful across coding, debugging, architecture, research, and product work.
The protocol stays the same across domains.

## How it works

1. Preserve observations and their provenance; separate interpretation, causal
   hypothesis, problem formulation, and proposed solution.
2. Identify the current formulation and plausible, materially different alternatives.
3. Find load-bearing assumptions and derive distinct observable predictions.
4. Select **one Primary Discriminating Test per round**, balancing information
   against cost, risk, and time. Inspect available, permitted, cheap evidence directly.
5. Strengthen, weaken, kill, or merge candidates from the result. Investigate again
   when another discriminating observation is worth its cost.
6. Stop with an overall verdict and return control to the host agent.

Before choosing the Primary Discriminating Test, the skill checks whether all
live formulations share the same consequential, untested frame. It may add one
grounded outside-frame challenger; unexplained evidence can reopen that check.
Output defaults to compact Fast / Normal / Deep paths, with later turns showing
only changed evidence and decisions.

| Overall verdict | Meaning | Handoff |
| --- | --- | --- |
| KEEP | Current framing is sufficiently validated and best-supported | Solutioning ALLOWED; host resumes authorized work |
| WEAKEN | Current framing lost material support but remains live | NOT YET; investigate the remaining uncertainty |
| KILL | Original framing is no longer viable; no replacement established | BLOCKED for that premise |
| REFORMULATE | A materially different replacement is sufficiently supported | NOT YET; return a named Reformulated Problem for downstream validation |
| INSUFFICIENT EVIDENCE | Evidence cannot discriminate enough | NOT YET; investigate or request minimum missing evidence |

`BYPASS` is an activation decision, not a verdict. `KILL` does not imply a known
replacement. After `REFORMULATE`, the host can validate the replacement in a brief
new pass using existing evidence, obtain `KEEP`, and continue within task scope.

**STOP solutioning does not mean STOP investigating. Skill STOP does not mean
Host Agent STOP.** After `KEEP`, a host already authorized to implement can proceed
in the same turn without asking for permission again. No new authority is granted.

## Quick example

User: "API P99 increased from 300 ms to 2.8 s. Add Redis."

- **Observation:** `user-reported` latency increase; not independently verified.
- **Interpretation:** the database is slow. **Causal hypothesis:** repeated reads
  delay requests. **Solution:** Redis. These are inferred, not measured facts.
- **Current formulation:** database service time materially dominates the slow tail.
- **Alternatives:** queueing/capacity, downstream dependency delay, or a measurement
  artifact. Runtime pauses and workload shifts may also matter if evidence suggests them.
- **Load-bearing assumption:** slow requests actually spend material time in DB work.
- **Primary Discriminating Test:** inspect an available, representative sample of
  slow and typical requests from the same window; reconcile end-to-end latency
  with queue, DB, and downstream time in one comparison.
- **Outcomes:** elevated DB time strengthens the current framing; rising queue wait
  with stable DB time weakens it and supports capacity; inconsistent totals support
  measurement trouble. Sparse or overlapping spans leave uncertainty.

If the evidence has not been inspected: `INSUFFICIENT EVIDENCE`, solutioning
`NOT YET`. The host should inspect it when accessible. If reliable observations
instead establish queue wait as the material delay: `REFORMULATE`, with that
revised problem. Neither result automatically authorizes a Redis implementation.
This is an illustrative example, not a reported production incident.

## When to use

Invoke explicitly when you want the current framing challenged. Automatic use
requires **both meaningful formulation uncertainty and non-trivial intervention
cost or risk**. Typical signals include:

- A proposed solution arriving before the problem has been tested.
- A causal hypothesis being treated as an observation.
- Repeated failed debugging or research attempts that preserve the same framing.
- Technology selection or an expensive product change preceding diagnosis.

## When NOT to use

Usually skip automatic activation for verified diagnoses, obvious compiler errors,
typos, formatting, translation, mechanical edits, or very cheap reversible changes.
Do not invent uncertainty merely because alternatives are logically possible.

For example, a compiler reports a missing `UserService`, and repository inspection
confirms it was renamed to `AccountService`. "Fix the import" normally bypasses
this skill. If explicitly invoked, a brief `KEEP` releases the host to fix it.

## What makes it different

**These methods overlap. This project focuses on a narrower operational responsibility.**

| Related method | Overlap and difference in emphasis |
| --- | --- |
| problem-framing | Often seeks a clearer, more useful, or better-scoped formulation. This skill treats the current one as falsifiable, seeks disconfirmation, updates from a discriminating test, and defines when to stop. Other framing methods can also challenge assumptions. |
| debugging | Often asks what caused a failure. This skill first asks why we classify the failure this way. Root-cause investigation may follow, but a list of possible causes is not sufficient formulation diversity. |
| grill-me | Attacks a plan, design, or proposal. This skill attacks the problem formulation before the plan should exist. |
| critical-thinking | A broader reasoning toolbox. This skill has one job: validate, weaken, reject, or replace the current problem framing before solutioning. |

The difference is emphasis, operational protocol, evidence update, and stopping
condition, not a claim to have invented reframing.

## Usage

```text
Use falsify-the-problem before solving this:
Our API P99 rose from 300 ms to 2.8 s. We think adding Redis will fix it.
Inspect the locally available evidence and challenge that framing first.
```

```text
Use falsify-the-problem:
Retention is low and we want to add push notifications.
What cheap observation would distinguish forgetting from never experiencing value?
```

```text
Use falsify-the-problem, then complete the authorized fix if the framing survives:
The compiler error and repository rename both show the import is outdated.
Fix that import.
```

The skill controls the framing pass. The host handles tools, access, permissions,
and downstream implementation. A gate on solutioning must not become a refusal
to inspect evidence or a permanent stop after `KEEP`.

## Evaluation

See [evaluation instructions](evals/README.md), [20 cases](evals/cases.md), and the
[scoring rubric](evals/rubric.md). Coverage includes all five domains, multi-turn
contradictions, unavailable evidence, accessible artifacts, and negative controls.
Cases test reasoning behavior rather than exact wording.

The [smoke-test record](evals/smoke-tests.md) records execution context, outputs,
scores, review findings, and revisions. **This is a behavioral smoke test, not a
statistically valid benchmark.** Small development runs cannot establish general
effectiveness or host-independent behavior. Baseline provenance and any missing
execution must be stated explicitly; a counterfactual analysis is not model output.

The [full-suite follow-up](evals/full-suite.md) records 20 paired cases, independent
grading with arm labels withheld, and catalog-based activation probes.
Some variants supply reports instead of underlying raw systems. Labels are hidden
from graders, but protocol wording can reveal the treatment. The record preserves
original scores, author disagreements, actual local fixes, and answer-length cost.
It does not establish cross-model or cross-host effectiveness.

The [R03 artifact follow-up](evals/r03-raw.md) uses staged, synthetic row-level
predictions to test selection and execution of a site-by-preprocessing comparison.
It separates target error reduction from reduction of the between-site gap.
These authored outputs do not constitute execution of an actual classifier.
Both arms scored 10/10 on this single variant; that is no evidence of a skill
advantage. The record preserves the label-audit and grading-scope qualifications.

The [R03 missing-pair test](evals/r03-stress.md) removes the initial replay hint and
adds regressions and incomplete coverage. It tests whether an agent distinguishes
matched-subset outcomes from an unresolved outcome for all selected records.
Both arms again scored 10/10; the record preserves the first-test labeling
ambiguity and its stricter alternative score. This remains a single authored pair.

The [harder formulation suite](evals/hard-suite.md) adds 12 cases targeting partial
explanations, shared blind spots, wrong targets, confounded tests, and reversals,
including two verified negative controls. The [coverage micro-suite](evals/coverage-eval.md)
adds six targeted cases across five domains. These development records report
quality, failure modes, and visible answer length separately; the earlier results
remain historical snapshots, not results for the revised skill.

In this run, the nine predeclared normal hard cases had median visible lengths of
218 words with the previous Skill, 178 with the revised Skill, and 117 with the raw
baseline (turns summed per case). Coverage scores tied at 10/10 on all six targeted
cases, and R03's first-round input-path omission remains. This supports a narrower
output-cost finding, not a demonstrated general coverage or raw-model advantage.

## Design principles

- One responsibility, one domain-agnostic protocol, one portable instruction file.
- Preserve evidence provenance; reports are not independent verification.
- Prefer materially different formulations to cosmetic variants of one cause.
- Choose tests whose possible outcomes change the decision.
- Let evidence overturn earlier conclusions. Keep investigation proportional.
- Treat `KEEP` and a prompt downstream handoff as normal success.

## Limitations

Markdown instructions guide a host; they do not enforce a runtime gate. Evidence
quality, access, model judgment, and selection behavior affect results. A test may
be inconclusive, support mixed causes, or only justify a narrow scope. The skill
does not prove causal identification, guarantee a correct replacement, or replace
specialist review. It is not a harness, runtime, generic debugging framework,
multi-agent system, orchestration engine, memory system, or AI scientist.

## License

[MIT](LICENSE).

Maintainers: see [Pages publishing and Bing setup](SEO.md).
