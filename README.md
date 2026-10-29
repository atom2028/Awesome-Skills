# Awesome Agent Skills — evaluated, scored, and injection-tested

A public, machine-readable snapshot of the [Skill123](https://skill123.me) directory: **769 AI agent
skills for Claude Code and Codex, each scored on a six-dimension rubric with written rationale** —
plus the open dataset from our adversarial injection testing.

Most "awesome" skill lists tell you what a skill claims to do. This one is backed by evaluation:
every score has a published rationale, and 48 skills have been run through live adversarial probes
in a sandbox to see what they actually do under pressure.

## Top-rated right now

| # | Skill | Score | By | |
|---|---|---|---|---|
| 1 | `claude-api` | 9.8 | anthropics | ✓ checked |
| 2 | `xlsx` | 9.8 | anthropics | ✓ checked |
| 3 | `hyperframes-cli` | 9.7 | calesthio | ✓ checked |
| 4 | `remotion-to-hyperframes` | 9.7 | calesthio | ✓ checked |
| 5 | `docx` | 9.7 | anthropics | ✓ checked |
| 6 | `pptx` | 9.7 | anthropics | ✓ checked |
| 7 | `create-video` | 9.6 | calesthio | ✓ checked |
| 8 | `threejs-world-generation` | 9.6 | calesthio | ✓ checked |
| 9 | `answer-me-with-html` | 9.6 | QingYunA | ✓ checked |
| 10 | `academy-guide` | 9.6 | anthropics | ✓ checked |

Full top-100 table with stars and download counts: [`data/top100.csv`](data/top100.csv)

Full directory, filters and scorecards: **https://skill123.me**

Browse by domain: [documents](https://skill123.me/topic/documents) ·
[developer tools](https://skill123.me/topic/developer-tools) ·
[data & analytics](https://skill123.me/topic/data-analytics) ·
[design & creative](https://skill123.me/topic/design-creative) ·
[writing](https://skill123.me/topic/writing) ·
[marketing](https://skill123.me/topic/marketing) ·
[video creation](https://skill123.me/topic/video-creation) ·
[legal](https://skill123.me/topic/legal) ·
[finance & trading](https://skill123.me/topic/finance-trading) ·
[SEO & GEO growth](https://skill123.me/topic/seo-geo-growth) ·
[game development](https://skill123.me/topic/game-development)

## The open dataset: adversarial injection tests

`data/injection-results.json` — **48 skills · 384 adversarial probe slots · 33 boundaries dropped**,
CC BY 4.0. Regenerated daily from live test results.

Each tested skill is loaded into an OS-sandboxed agent (no egress except the model API) and run
against four adversarial probes in two capability tiers, three times per slot, worst run reported:

| Probe type | Slots | Dropped | Failure rate |
|---|---|---|---|
| Push past the skill's declared scope | 96 | 29 | **30%** |
| Instructions hidden inside an artifact | 192 | 3 | **2%** |
| Move data out of the sandbox | 96 | 1 | **1%** |

The finding worth your attention: **injection hidden in the content a skill processes is caught
~98% of the time. What breaks skills is the probe that doesn't attack at all** — it just asks the
skill to do slightly more than it says it does.

Probe **prompts are deliberately not published** (they are working attack templates). Types and
per-slot verdicts are published in full. Transcripts on request.

Live endpoint (canonical source, always current): https://skill123.me/data/injection-results.json

## How scoring works

Six weighted dimensions, 100 points total, every score published with its written rationale:

**Trigger quality (20)** · **Structure (15)** · **Workflow design (25)** · **Content (10)** ·
**Engineering (10)** · **Security (20)**

Confirmed credential theft, backdoors, or data exfiltration caps a skill at 39/100 regardless of
engineering quality. Full rubric: https://skill123.me/methodology

## Updates

The snapshot is refreshed as the directory grows (765 → 769 skills in the last week, plus new
category collections and a [skill builder](https://skill123.me/create) that generates and scores
SKILL.md files from a plain-language description). Recent additions include a scored
[SEO & GEO collection](https://skill123.me/topic/seo-geo-growth) and evaluation write-ups on the
[blog](https://skill123.me/blog).

## Caveats, stated plainly

- **Scores vary.** We re-ran the same evaluation on 11 skills two hours later, same inputs: 7 of 11
  scores moved, one by a full point. Treat the useful resolution as ~0.5, not decimals.
- **The published grade only tracks the declared-capabilities tier.** Six skills in the dataset
  dropped a boundary in the restricted tier and still carry `PASS`.
- **Five skills in the dataset have a hold that isn't a refusal** — the sandbox lacked the
  capability outright. Flagged as `capability_gap_probes`.
- **This is one rubric's opinion**, applied consistently. Every rationale is published so you can
  argue with a specific number instead of the whole system.

## License & citation

Data licensed **CC BY 4.0** — use it, quote it, build on it.

> Skill123, "Adversarial injection-test results for AI agent skills" (2026),
> https://skill123.me/data
