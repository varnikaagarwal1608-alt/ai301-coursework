# Contribution: docs: verified workaround for missing desktop Dot while keeping codex-lb routing

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Varnika Agarwal
**GitHub Username:** varnikaagarwal1608-alt
**Issue:** https://github.com/Soju06/codex-lb/issues/2669
**Pull Request:** https://github.com/Soju06/codex-lb/pull/2713

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built my issue-scout and search strategy, then fixed its ranking**

I installed the issue-scout skill, wrote three `gh search issues` queries from my fit profile (good first issue and documentation, Python and JavaScript), and added ranking filters. My first scan's top 5 were all issues filed minutes earlier, because I ranked by most recently updated and my 60-day filter removed nothing. I changed the tie-break to oldest created first, added a rule to drop issues created in the last 3 days, and added the missing createdAt field to my queries so those rules can work. I haven't re-run a scan to confirm the fix. When I graded my three picks, the scout accepted an issue that was already fixed (a merged PR), so the rubric needs an "already resolved" check, which I plan to add.

**Unit 6: Voice guard installed and used by hand, scout rubric patched, memory file not written**

I installed the voice guard (one canonical voice guide with an Upstream section, `check_voice.py`, and a PreToolUse hook). `/hooks` showed the hook loaded, but my wiring test (`gh issue comment --help`) ran instead of being stopped, even after I widened the matcher to `Bash|PowerShell`, so I ran `check_voice.py --draft` by hand before each post and posted with `gh`. The guard also stopped my claim draft twice on rules I had written: one rule asked for a report-back date while repro-check rejects dates in a claim, and another demanded a question that names what I had already read. I rewrote the first rule and dropped the question from the claim. I also patched the scout rubric: I replaced "Scope is bounded" with the staff scope-feasible row and added a difficulty note, plus a new required "Not already resolved" check. I have not written the CLAUDE.local.md memory file yet.

**Unit 7: Did not install the ship-gate; checked the branch by hand**

I did not install the ship-gate or write a ship-manifest.md. I ran the equivalent checks by hand before opening my PR: I searched the two docs pages before and after the change, read `git diff --stat` (2 files, 26 insertions, 0 deletions), and confirmed that both new anchor links point at headings that exist. I could not run the repo's own checks (`uv run pre-commit` and `make lint`) because `uv` and `make` are not installed on my Windows machine, and `.pre-commit-config.yaml` has no markdown hooks. The change has no code. I wrote that gap into the PR description instead of ticking the box. I would install the ship-gate earlier next time, so the manifest decides which checks count before I open the PR.

**Unit 8: Did not install the PR monitor; no maintainer feedback yet**

I did not install the PR monitor or write a playbook. My PR (#2713) is a draft that I opened on 2026-11-09. As of 2026-11-10 it has no reviews or comments, so there was nothing for a monitor to draft. I checked the PR page by hand and posted one report-back comment on the issue linking the PR, after running my voice check on it. Without a playbook I have no written threshold for when to nudge. The repo's CONTRIBUTING.md says to ask in a draft PR when unsure about OpenSpec, and I asked there.

---

## Why I Chose This Issue

I searched with three `gh search issues` queries built from my fit profile (small Python or JavaScript bug fixes and docs improvements), then used the AI301 Issue Selection site with Language set to Python and Tag set to documentation and bug. My first scout scan put brand-new one-person-repo issues at the top, so I changed the ranking. In Unit 5 the scout graded three picks and accepted all three, but one (simpler-grants-gov#9806) had already been fixed by a merged PR, and another (pygmt#1370) had a comment from someone saying "I can take this". When I read each thread myself I dropped pygmt#1370, and I also dropped dynamo#13317, because its author had offered to submit the PR. After I patched my rubric I graded two more: dynamo#13497 was rejected (it is a sub-task of a tracking issue, with two open PRs), and codex-lb#2669 was accepted with a difficulty note of straightforward.

I chose Soju06/codex-lb#2669 because it fits my profile: a small docs change in a Python project, with the two files named in the issue (docs/client-setup.md and docs/troubleshooting.md). It had no assignee, no comments and no linked PRs, and the repo's CONTRIBUTING.md lists documentation recipes as a welcome contribution. I hope to learn how a real project takes a docs PR: Conventional Commit titles, the PR template, and the OpenSpec rule. My claim comment is https://github.com/Soju06/codex-lb/issues/2669#issuecomment-6729866116.

My honest read of the scout: it did the broad search work, but it missed things I only caught by reading the threads. It accepted an already-fixed issue and an issue with a visible "I can take this", because my "not claimed" check only looked at assignees and open PRs. It also passed #2669's "triaged by a maintainer" check on labels that look auto-added (one of them is "triage"). I fixed the first two by adding "Not already resolved" and the scope-feasible row. I have not yet changed the triage check; I would make it ignore labels added at creation and treat a "triage" label as not triaged. I also did not re-run a full scan after the patch.

**Toolkit**

- Tool: issue-scout (my search strategy and rubric), run as `claude "issue-scout: run a scan"` and `claude "issue-scout: grade <urls>"`, plus my own reading of each issue thread with `gh issue view --comments`.
- What it produced: a first scan of 5 accepted issues ranked by newest creation, three accepted Unit 5 picks, and in Unit 6 an accept for codex-lb#2669 (straightforward) and a reject for dynamo#13497, with a note proposing a stricter triage check.
- Difficulties: it accepted an already-fixed issue and an issue with a visible claim, and it passed the triage check on auto-added labels. The GitHub API rate limit also ran out once during grading, and it reset.
- What changed: I changed the tie-break and added a created-date rule, replaced the scope row, added the difficulty note, and added a "Not already resolved" check. I still plan to tighten the triage check.

---

## Understanding the Issue

**Problem Description**

The issue reporter says the Dot sidebar entry disappeared from the Codex desktop app when `model_provider = "codex-lb"` was set, while it still worked on web and phone. They found a configuration that brought Dot back while keeping requests routed through codex-lb, and asked for it to be documented as an optional desktop recipe. The docs do not contain it.

**Expected Behavior**

docs/client-setup.md and docs/troubleshooting.md should describe the optional recipe (keep the built-in `openai` provider ID and set `openai_base_url` to codex-lb), with its limits and a rollback.

**Current Behavior**

Neither page mentions it. Searching both for `Dot|openai_base_url|desktop` returns one unrelated match (troubleshooting.md line 5, about `rate_limited`).

**Affected Components**

Documentation only: docs/client-setup.md and docs/troubleshooting.md. No code changes.

**Toolkit**

- Tool: `gh issue view 2669 --comments` in PowerShell to read the issue and thread, and Claude to help me read the pasted text and the existing docs structure.
- What it produced: the issue's working configuration, its stated limits (loopback-only proxy, API key auth disabled, macOS only, native voice not tested), and the repo's doc layout.
- Difficulties: the workaround was verified on macOS and I am on Windows, so I cannot test it myself.
- What changed: I wrote the recipe as "reported by the issue author" and added "not verified on other platforms" to the docs text.

---

## Reproduction Process

**Environment Setup**

Windows with PowerShell, Python 3.13.14, git, and GitHub CLI 2.102.0. I forked Soju06/codex-lb with `gh repo fork Soju06/codex-lb --clone`, ran `gh repo set-default Soju06/codex-lb`, and created the branch `docs/desktop-dot-recipe` from main. `git remote -v` shows `origin` as my fork and `upstream` as Soju06/codex-lb. Challenges: `uv` and `make` are not installed on my machine, so I could not run the repo's lint gate, and PowerShell mangled one `--jq` command, which I replaced with PowerShell formatting. I cannot run the macOS desktop app, so I could not reproduce the Dot problem itself.

**Steps to Reproduce**

1. Clone the repo and check out main (before my change).
2. Run `Select-String -Pattern "Dot|openai_base_url|desktop" -Path docs\client-setup.md, docs\troubleshooting.md`.
3. Observed result: 1 match, troubleshooting.md:5, a question about `rate_limited` in Codex Desktop. There is no mention of Dot or `openai_base_url`, so the recipe is missing from both pages.

**Reproduction Evidence**

- **Commit showing reproduction:** none. This is a docs gap, so the reproduction is a search of the unmodified main branch. The fix commit is 2e72fe66 on my fork, branch docs/desktop-dot-recipe.
- **Screenshots/logs:** the search output above (1 match, unrelated), run before I edited either file.
- **My findings:** I could confirm that the docs lack the recipe, but I could not confirm the underlying Dot behavior, because it was reported on the macOS desktop app. I said so in my claim comment and in the PR.

**Toolkit**

- Tool: repro-check (real-repo scope), run as `claude "repro-check: grade my draft claim comment in claim-draft.md for issue <url>"`. I have not run it on my repro report.
- What it produced: a reject on my first claim ("Claim promises, doesn't assert", because the draft promised a report-back date) and an accept on the second draft, with the repro checks marked "unclear: not yet applicable".
- Difficulties: my own voice guide rule asked for a report-back day, which conflicted with repro-check, and my "one question" rule stopped a draft that asked something before I had read the docs.
- What changed: I rewrote the rule to "report back once that step is done, with no date" and dropped the question from the claim.

---

## Solution Approach

**Analysis**

This is not a code bug. It is a gap in two documentation pages: docs/client-setup.md has sections for the Codex CLI and IDE extension, but nothing about the desktop app's Dot entry, and docs/troubleshooting.md has no entry for it.

**Proposed Solution**

Add a section "Desktop app: restoring Dot (optional)" to docs/client-setup.md before "Verify WebSocket transport", with the two top-level config keys, a backup step, rollback steps and the limits from the issue. Add a short entry "Dot missing from the Codex desktop sidebar" to docs/troubleshooting.md that links to it. I am deliberately not changing any code, not adding an OpenSpec entry (CONTRIBUTING.md says only behavior, requirement, contract or schema changes need one), not editing CHANGELOG.md, and not claiming the workaround is verified.

**Implementation Plan**

1. Insert the new section in docs/client-setup.md before "Verify WebSocket transport".
2. Insert the new entry in docs/troubleshooting.md before "Old Codex sessions missing after migrating".
3. Check that both new headings exist, that the two anchor links resolve, and that the diff only adds lines.

No deviations from this plan.

**Toolkit**

- Tool: Claude, which drafted the recipe wording from the issue text and the style of the existing sections. I read it and kept the limits from the issue. I did not run plan-check, and I did not write plan.md.
- What it produced: the two inserted blocks (21 lines in client-setup.md, 5 in troubleshooting.md).
- Difficulties: I had no way to verify the recipe on Windows, and I did not use the plan-check step the course describes.
- What changed: I added "Reported on the macOS desktop app... not verified on other platforms" and the API-key warning to the text.

---

## Testing Strategy

I re-ran the reproduction search and the checks on my branch. Before the change (on main), the search for `Dot|openai_base_url|desktop` found one unrelated match. After the change, the headings exist at client-setup.md:199 ("Desktop app: restoring Dot (optional)") and troubleshooting.md:19 ("Dot missing from the Codex desktop sidebar"), and `git diff --stat` shows 2 files changed, 26 insertions(+), 0 deletions. I checked that the new anchors `#desktop-app-restoring-dot-optional` and `#migrating-from-direct-openai-session-retagging` point at headings that exist. I could not run `uv run pre-commit run local-ci --hook-stage manual --all-files` or `make lint` because `uv` and `make` are not installed on my machine. The change is docs only, and `.pre-commit-config.yaml` has no markdown hooks. I said this in the PR instead of ticking the box.

**Toolkit**

- Tool: PowerShell `Select-String` and `git diff --stat` for the before and after checks, written into the PR's test plan.
- What it produced: the before output (1 unrelated match), the after output (both headings found), and the diff stat.
- Difficulties: no test suite applies to a docs change, and `uv` and `make` were missing, so I had no repo-run check to show.
- What changed: I wrote the missing checks into the PR checklist as not run, with the reason.

---

## Implementation Notes

**2026-11-08**

Chose codex-lb#2669 after reading CONTRIBUTING.md (`.github/CONTRIBUTING.md`; the root path returned 404). Drafted a claim, and repro-check rejected the first version because it promised a date. I reworded it to promise a report-back event, then posted it with `gh issue comment` after my voice check passed. Wrong turn: I first tried pygmt#1370, which the scout had accepted, but the thread already had "I can take this".

**2026-11-09**

Forked and cloned the repo, created branch `docs/desktop-dot-recipe`, and confirmed the docs lack the recipe. Added the two doc blocks, committed (2e72fe66, "docs: add optional desktop Dot recipe for codex-lb routing (#2669)") and pushed to my fork. I filled in the repo's PR template, opened the PR as a draft because CONTRIBUTING.md says to ask when unsure about OpenSpec, and verified that it targets Soju06/codex-lb and not my fork. I also posted a report-back comment on the issue with the PR link.

**Toolkit**

- Tool: git, `gh`, and my voice guard run by hand (`check_voice.py --draft`) before each public post.
- What it produced: one commit, one draft PR, a claim comment and a report-back comment, each checked first.
- Difficulties: the voice guard's hook did not block in Claude Code, so the check was manual.
- What changed: I ran the check myself and only posted when it said pass.

---

## Pull Request

**PR Link:** https://github.com/Soju06/codex-lb/pull/2713

**PR Description:** I opened it as a draft, using the repo's PR template. Summary: add an optional desktop Dot recipe to docs/client-setup.md and a pointer in docs/troubleshooting.md, based on the working configuration reported in the issue and keeping its limits. Type: docs. Linked issue: Fixes #2669. OpenSpec: not applicable (docs only), with a note asking the maintainer whether they want a spec entry. Test plan: before and after output of the search, the diff stat, and the anchors check. Checks not run: `uv run pre-commit` and `make lint`, because `uv` and `make` are not installed, with the reason that the change contains no code. AI assistance: Claude helped read the issue and docs and draft wording, which I edited and reviewed.

**Maintainer Feedback:**

- 2026-11-10: none yet. The PR is a draft with no reviews or comments, and the issue has only my two comments.

**Status:** Awaiting review

**Toolkit**

- Tool: `gh pr create --draft` after a manual `check_voice.py --draft pr_draft.md` pass. I did not install the ship-gate.
- What it produced: the draft PR #2713 on Soju06/codex-lb (not on my fork), with every template item answered.
- Difficulties: the ship-gate was not installed, so no tool decided whether the branch was ready, and I made that call myself. `uv` and `make` were missing, so I could not run the repo's checks.
- What changed: I wrote the unrun checks into the PR with reasons, and I opened it as a draft to ask the OpenSpec question.

---

## Learnings and Reflections

**Technical Skills Gained**

I learned how to read a real project's contribution rules (CONTRIBUTING.md, PR template, Conventional Commit titles, OpenSpec-first workflow), how to fork and clone with `gh repo fork --clone` and point `gh` at the original repo with `gh repo set-default`, and how to open a draft PR against an upstream repo from a fork with `gh pr create --repo ... --head user:branch`. I also learned how to use PowerShell where the course commands assume bash.

**Challenges Overcome**

The hardest part was trusting my scout. It accepted an issue that a merged PR had already fixed, and one with a visible "I can take this", and I only caught those by reading each thread myself. I also had to work around Windows: the course's `cp`, `mv` and `ln` commands, `python3`, and a hook that loaded but did not block. My voice guide rules and the repro-check grader also disagreed about dates in a claim, and I reconciled them.

**What I'd Do Differently Next Time**

I would read every thread before grading, not after, and I would install the ship-gate and the PR monitor when the unit starts so they decide what counts as ready. I would also write the memory file and the plan in the week they belong to, and start earlier so that I do not have to do two weeks of work at once.

---

## Resources Used

- `.github/CONTRIBUTING.md` in Soju06/codex-lb, for the branch, commit and OpenSpec rules.
- Soju06/codex-lb#2669, the issue itself, for the configuration and its limits: https://github.com/Soju06/codex-lb/issues/2669
- The repo's `.github/PULL_REQUEST_TEMPLATE.md`, which I answered item by item in the PR.
- The `gh search issues` manual, for the flags and JSON fields in my scout queries: https://cli.github.com/manual/gh_search_issues
- The Unit 6 `skill/INSTALL.md` and `skill/rubric-scope-patch.md`, which I followed for the voice guard and the rubric patch.
