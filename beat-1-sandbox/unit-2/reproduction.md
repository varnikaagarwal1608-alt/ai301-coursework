# Unit 2 — Claim and Reproduce

## Your identity upstream

**GitHub username:** varnikaagarwal1608-alt

## Posted upstream

### Claim comment
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/36#issuecomment-5863303494

Investigating this issue — starting with the existing tests in `tests/unit/test_review_routes.py` to understand the current `POST /reviews` coverage, then adding a test for the no-ingested-documents case. I'll report back with what I find.

### Reproduction comment
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/36#issuecomment-5881982529

Environment: Windows (PowerShell), git 2.53.0.windows.2, Python 3.13.14 (repo requires 3.11+, so this satisfies it). Node.js and npm are not installed. Docker is not installed.

Steps attempted: cloned my fork of pathreview-ai301-fa26-s3, located setup instructions in docs/SETUP.md. The documented setup requires Docker Compose to start PostgreSQL and Redis (docker compose up -d), followed by `make setup` to run migrations and seed test accounts, before the API or any test can run.

Blocker: Docker is not installed on my machine (`docker --version` → "docker: The term 'docker' is not recognized"). Without the backing Postgres/Redis containers, `make setup` cannot run migrations, no test accounts get seeded, and POST /reviews has no database to write to. I could not proceed past this point in the documented setup.

What this means for the test: I could not independently reproduce the behavior trihiennguye-ux described (a profile with zero ingested documents still completes with a fabricated-looking score rather than erroring) because I could not stand up the environment required to run the endpoint at all. I'm reporting this honestly rather than guessing at behavior I haven't observed myself.

## Eval iterations

### Run history

1. Smoke test (`--limit 3`): 3/3 agreement
2. First full run: 16/17 scored items agreed (3 packages errored due to a Windows Unicode encoding bug in the terminal, not a rubric issue); one disagreement on pkg-05 (gold: accept, mine: reject, failed "Steps complete and followable")
3. Retried the 3 errored packages with `--workers 1` to fix the encoding issue (`--only pkg-04,pkg-07,pkg-11`): 2/3 agreed (pkg-11 disagreed: gold accept, mine reject, failed "Claim promises, doesn't assert")
4. Confirming full run (`--workers 1 --save-run eval-run.txt`): **19/20 scored items agreed (bar: 18/20 — PASS)**, every category matched (clear-accept 7/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 4/4)

### Package analysis

**pkg-05**: gold label says **accept**; my rubric said **reject**, failing the "Steps complete and followable" check. The package's repro report describes writing a minimal `env.yml` with a `category:` section but doesn't paste the file's literal contents — only a prose description of it. My check's pass condition required steps to be repeatable "verbatim," which this technically fails on a strict reading. But the bug only depends on the presence of the unrecognized `category:` key — the surrounding `dependencies:` values don't matter to reproducing it — so the omission doesn't actually block a stranger from reproducing the behavior. My rubric was judging the write-up's shape (did it show the literal file) rather than the outcome (can the bug still be reproduced from what's given), which is the trap the rubric template explicitly warned against.

### Check rationale

Quoted as it currently reads in `rubric.md`:

"Disclosure respects repo convention | Comment text, read against the repo-facts block's disclosure policy | If the repo requires disclosing AI assistance, the comment discloses it; if no such policy exists, this check passes automatically | required"

I wrote this check because the assignment flagged that one eval package specifically tests whether a rubric can catch an AI-disclosure violation, and a rubric with no check for it cannot recover those points elsewhere. Without this check, a comment written with AI assistance in a repo that requires disclosure would pass every other check and still get posted improperly.

### Trade-offs

This check gives up nuance on *how* disclosure should be phrased — it only checks whether disclosure is present at all, not whether it's clearly worded or placed prominently in the comment. I accepted this trade-off because the eval set's one disclosure-relevant package (the category floor's single-package category) only tests presence versus absence, not phrasing quality, so a stricter check risked false rejects on comments that disclose adequately but informally. My confirming full run matched this category (disclosure 1/1), so the simpler binary check was sufficient for what the eval set actually probes.
