Unit 1 — Issue Selection

## Selected issue

### Issue link
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/36

### Verdict output

All three issues are inside the scoped repo (codepath/pathreview-ai301-fa26-s3). Graded each independently against the six required checks in rubric.md - the rubric defines no `preferred` checks, so ranking below comes purely from the fit profile in scope.md.

Shared repo evidence (same for all three):
- Maintainer active - Aburke225 (COLLABORATOR) committed "chore: track five more manifest entries..." on 2026-09-16, 6 days before today, and opened/labeled all three issues.
- Repo in active use - archived: false, last push 2026-09-16 (no releases, but push is well inside 12 months).
- AI policy - docs/CONTRIBUTING.md and the PR template state no AI restriction of any kind; silence passes.
- Not claimed - repo has 0 open PRs; all three issues have 0 comments, 0 assignees, no cross-referenced PRs in their timelines.

Accepted, in fit order:

1. #36 - no test for `POST /reviews` with a profile that has no ingested documents - best fit: it's the only one labeled `good first issue` (plus `tier-1`), the smallest at 2-3 hours, and it's confined to a single existing file (tests/unit/test_review_routes.py). Pure backend Python, which matches the profile's comfort zone, and it's the one that actually fits "limited time this week."
2. #38 - integration tests for authentication edge cases - backend Python, and the body enumerates exactly four cases (expired, malformed, missing header, wrong secret), so it's bounded. Costs more: 3-5 hours, tier-2, and requires standing up a new file in an empty tests/integration/ plus touching tests/conftest.py.
3. #16 - failed tool calls in tool_results never reach the review output - a genuine, well-described backend bug fix, but the largest at 4-6 hours, tier-2, and it changes behavior across two modules (agent/orchestrator.py and core/services/review_service.py) rather than adding a test.

Rejected: none.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/36",
    "checks": [
      {"name": "Maintainer active", "grade": "pass", "evidence": "Aburke225 (COLLABORATOR) commit 2026-09-16T21:42:18Z, 6 days before today; also opened and labeled this issue"},
      {"name": "Repo in active use", "grade": "pass", "evidence": "archived: false, pushed_at 2026-09-16T21:50:20Z (within 12 months)"},
      {"name": "Issue has been triaged by a maintainer", "grade": "pass", "evidence": "Opened by Aburke225 (author_association COLLABORATOR) with labels ['good first issue','api','devops','docs','tests','tier-1']"},
      {"name": "Scope is bounded", "grade": "pass", "evidence": "One test in one named file (tests/unit/test_review_routes.py), 'Estimated effort: 2-3 hours'; not a tracking issue, no design debate, no abandoned-claim history"},
      {"name": "Not already claimed right now", "grade": "pass", "evidence": "assignees: [], comments: 0, no cross-referenced PRs in timeline, repo has 0 open PRs"},
      {"name": "Contribution policy allows AI-assisted work", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md contain no AI restriction; no AI_POLICY.md in repo"}
    ],
    "verdict": "accept"
  }
]
```

## Eval iterations

### Run history
1. First full run: 15/20 agreement (below bar; missed issue-01, 04, 19 on Scope is bounded; wrongly accepted issue-15, 20)
2. Cheap re-check (`--only issue-01,issue-04,issue-19,issue-15,issue-20`) after revising the rubric: 5/5 agreement on the re-checked issues
3. Final full confirming run (saved to eval-run.txt): 20/20 agreement, bar 18/20: PASS

### Issue analysis
issue-15: my rubric's first version wrongly graded this **accept** (gold label: **reject**). The issue has no current assignee and no open linked PR, so my original "Not already claimed" check passed it cleanly. But the thread shows the issue has been open since 2021, claimed and abandoned by at least six different contributors, with two closed/unmerged linked PRs. My original rubric had no way to see that history — it only checked *current* claim status, not the issue's track record. I moved this signal into the "Scope is bounded" check (a long history of abandoned attempts is itself a scope/difficulty signal, per the evidence guide's family-3 notes on age and history), and the final rubric correctly rejects it.

### Check rationale
Quoted as currently written in rubric.md:
"Issue has been triaged by a maintainer | Labels, thread comments, and who opened the issue | Pass if the issue has at least one meaningful label (not "none"/empty), OR a maintainer/collaborator has commented in the thread, OR the issue was opened by a maintainer/collaborator. Fail if opened by a bot account with no labels and no maintainer engagement at all | required"

I added this check because my first rubric had no way to tell a maintainer-vetted issue apart from an unfiled idea. issue-20 (a feature request opened by a bot account, with no labels and zero maintainer response) slipped through my original rubric as an accept, when the gold label says reject — nobody had actually looked at it or confirmed it was worth doing.

### Trade-offs
I re-ran this check as a canary with `--only issue-20` after adding it, and it correctly flipped that issue from accept to reject without changing any of the other 19 verdicts. The trade-off: this check could reject a genuinely good issue from a maintainer who is simply slow to add labels, or one opened by a real new contributor rather than a maintainer, even if the work itself is fine. I accept that risk because in this eval set the pattern only ever showed up on the one bot-filed, zero-engagement issue, and unlabeled/unvetted issues are a reasonable thing for a first-time contributor to avoid regardless.

## Selection rationale

1. **Fit to interests and time available:** #36 is a small, self-contained backend Python test addition (2-3 hours), which matches both my comfort zone and how much time I have this week.
2. **What the verdict identified vs. what I weighed:** the skill's live-mode run confirmed all required checks passed — no claim conflicts, an active maintainer, no AI restrictions. What the rubric couldn't weigh was personal fit: I additionally favored #36 over #38 and #16 specifically because it touches only one existing file rather than requiring me to scaffold new test infrastructure, which lowers my setup risk given limited time.
3. **Anticipated difficulty in claiming it:** low — the issue has zero comments, no assignee, and no competing claims, so claiming it should be straightforward with no need to negotiate a shared issue.
