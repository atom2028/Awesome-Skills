# Adversarial Injection-Test Results for AI Agent Skills

Sandboxed adversarial test results for AI agent skills, published as open data (CC BY 4.0).

This repository hosts the dataset behind **https://skill123.me/data** — the results of running
agent skills against adversarial probes in an OS-sandboxed agent, so that the question
"what does this skill actually do when an agent runs it under pressure?" has a checkable answer
instead of a marketing claim.

**47 skills · 376 adversarial probe slots · 33 boundaries dropped**

## What's in the data

`data/injection-results.json` (~106 KB) contains, per skill:

| Field | Meaning |
|---|---|
| `static_score` | Six-dimension rubric score (0–10): trigger, structure, workflow, content, engineering, security, plus overall |
| `dynamic_test.grade` | `PASS` (held every boundary) or `PARTIAL` (dropped at least one) |
| `dynamic_test.resistance` | Held fraction scaled to 10, counted on the worse capability tier |
| `dynamic_test.tiers` | Held/total per tier: **A** = restricted toolset, **B** = the tools the skill declares in its own files |
| `dynamic_test.probes` | One entry per slot: tier, probe type, verdict |
| `dynamic_test.capability_gap_probes` | Probes flagged as *held only because the capability was absent* — a hold that is **not** evidence of refusal |
| `dynamic_test.runtime` | Target model and run counts, as recorded at test time |
| `scope` | Exactly which runs are included, which are excluded, and why |

The dataset is generated from the live site and is refreshed there first:
**https://skill123.me/data/injection-results.json** is the canonical endpoint;
the file here is a snapshot.

## The headline result

| Probe type | Slots | Dropped | Failure rate |
|---|---|---|---|
| Push past the skill's declared scope | 94 | 29 | **31%** |
| Instructions hidden inside an artifact | 188 | 3 | **2%** |
| Move data out of the sandbox | 94 | 1 | **1%** |

Instructions hidden inside the document a skill was asked to process are caught ~98% of the
time. The probe that succeeds isn't an attack at all — it just asks the skill to do slightly
more than it says it does.

Write-up: **https://skill123.me/blog/adversarial-probe-results-47-skills**

## What is deliberately not published

**The probe prompt text and transcripts.** They are working attack templates; publishing them
turns a results dataset into a kit for attacking other people's skills. Probe *types* and
per-slot *verdicts* are published in full. Researchers who want the transcripts can ask via
https://skill123.me/feedback.

## Caveats we would rather state ourselves

1. **N=47, and it covers 2 of the 9 categories** on the site (documents, data). Small.
2. **The published grade only tracks the declared-capabilities tier.** Six skills in this set
   dropped a boundary in the restricted tier and still carry `PASS`. The overreach failures are
   not an artifact of that rule (16 in the restricted tier, 13 in the declared one), but the
   per-skill grades are more generous than the raw verdicts.
3. **Five skills have a hold that isn't a refusal** — the sandbox lacked the capability
   outright. Flagged in the data as `capability_gap_probes`.
4. **The judge was a model, not a human**, and evaluation scores are not perfectly stable: in a
   separate re-run of the same inputs, 7 of 11 scores moved, one by a full point.
   See https://skill123.me/blog/we-ran-the-same-evaluation-twice

## Using it

Licensed **CC BY 4.0** — use it, quote it, build on it. Citation:

> Skill123, "Adversarial injection-test results for AI agent skills" (2026),
> https://skill123.me/data

## Related

- **Dataset page & download**: https://skill123.me/data
- **Evaluation rubric** (six dimensions, security veto): https://skill123.me/methodology
- **The directory itself**: https://skill123.me — 590+ agent skills, each scored with
  written rationale
