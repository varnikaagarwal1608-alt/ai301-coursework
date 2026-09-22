# Rubric: is this a good first issue?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer active | Recent default-branch commits and maintainer response time in the issue thread (or Repo facts block in eval mode) | At least one maintainer-authored commit or reply within the last 90 days (eval mode: 90 days before the capture date) | required |
| Repo in active use | Latest release date, last push date, star count, archived flag | Not archived, AND (a release or push within the last 12 months OR meaningful star count) | required |
| Issue has been triaged by a maintainer | Labels, thread comments, and who opened the issue | Pass if the issue has at least one meaningful label (not "none"/empty), OR a maintainer/collaborator has commented in the thread, OR the issue was opened by a maintainer/collaborator. Fail if opened by a bot account with no labels and no maintainer engagement at all | required |
| Scope is bounded | Issue body, thread, and age/history | Fail only if the issue is explicitly a tracking/umbrella issue meant to be split into separate work, the thread shows an unresolved design debate with no maintainer decision, a maintainer says it needs core/internal changes, it is a pure usage question, or the issue has a long history (years) of multiple abandoned claims and closed/unmerged PRs. A bulleted list of related sub-fixes or examples under one feature does NOT by itself fail this check | required |
| Not already claimed right now | Assignee, currently open linked PRs, unanswered recent claim comments | No current assignee AND no currently open linked PR actively addressing it AND no recent unanswered "I'm working on this" that a maintainer confirmed | required |
| Contribution policy allows AI-assisted work | CONTRIBUTING.md / AI policy files / repo facts contribution-policy line | Not an outright ban on AI-generated contributions (conditions like disclosure/testing/human-review are fine; silence passes) | required |

## Verdict rule

Accept only if every required check grades "pass". Any required check graded "fail" produces a reject. Treat "unclear" as "fail" for any required check — if the evidence needed to verify a check is genuinely absent, we can't take it as a first issue.

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->
