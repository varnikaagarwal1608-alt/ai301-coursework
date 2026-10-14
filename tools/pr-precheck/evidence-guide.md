# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

**Where it lives.**
- Eval bundle: the plan's files, "Not in scope" line, and test plan are in the **Plan context** block. Any deviation note is there too. What actually changed is in **Candidate PR > Diff** (changed files and hunks) and **Commits**. The description's fidelity claims are in **Candidate PR > Description**.
- Live mode: the plan is `plan.md` in the top folder of the clone, including its `## Deviations` section. What changed is the output of `git diff main...HEAD` (three dots; committed changes only). Claims are in `pr_draft.md` (Summary, Changes, Checklist).

**What good looks like.** Every changed file and hunk is named by the plan's files or recorded under Deviations, and every change the plan promised is in the diff or disclosed as left out. Every claim in the description ("exactly as planned", "no options added", each Changes bullet) has a diff line behind it. Silent drift is a diff that does more than the plan (extra files, extra hunks), does less with no note, or a description claiming more or less than the diff delivers. An honest deviation means the change appears in the plan's Deviations AND the description.

## Test evidence (harness category: not-tested)

**Where it lives.**
- Eval bundle: **Candidate PR > Test evidence**, plus any test files in **Candidate PR > Diff**. Compare against the **Plan context** test plan and the repro evidence's steps. In eval mode, expect only the checks the bundle's **Repo facts** block names. Do not demand checks the repo never mentions.
- Live mode: `test_evidence.md` and the Testing section of `pr_draft.md`, plus test files in `git diff main...HEAD`. Compare against the test plan in `plan.md`. In live mode only, the repo's own checks are the four in the Path Review PR template: `make test-unit`, `make test-integration`, `make lint`, `make typecheck`.

**What good looks like.** Each result is a command with its real printed output, or a concrete test result with counts (for example "1462 passed, 12 skipped"). A bare "passes" with no command or counts, or a `# comment` saying what was printed, is not evidence. The before and after of the repro are both shown. Every scenario the plan's test plan names is exercised by a command with output, or by a test in the diff that the evidence shows passing. Every test the description claims exists in the diff. A failing or not-run check reported honestly with the reason counts as evidence. In live mode for Path Review, `make test-integration` stopping with "no tests ran" is expected and counts if pasted as is.

## Diff quality (harness category: unreviewable)

**Where it lives.**
- Eval bundle: **Candidate PR > Diff** and **Commits**.
- Live mode: `git diff main...HEAD` and `git diff main...HEAD --stat` for the file list.

**What good looks like.** The fix is visible and nothing unrelated rides along. Every hunk is part of the change. The debris tells are: debug lines (print, console.log, debugger), commented-out code, stray files, whitespace or formatting churn in untouched code, and drive-by edits the issue does not need. A hunk unrelated to the plan fails even if the description explains it.

## Standards and comms (harness category: standards-wall)

**Where it lives.**
- Eval bundle: the **Repo facts** block lists the PR template (or says there is none), the contribution docs' asks, and any stated AI policy. The **Thread highlights** may hold explicit maintainer direction. The PR's answer is in **Candidate PR > Title** and **Description**. In eval mode, the template is whatever the Repo facts block describes. Do not require sections it does not mention.
- Live mode: `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md` in the Path Review repo, and the issue thread (fetched live). The PR's answer is in `pr_draft.md`: title on line 1, then the template sections (Summary, Issue, Changes, Testing, Screenshots / Demo, Notes for Reviewers).

**What good looks like.** Every section or ask the repo's template states has real content for this change. The issue is linked when the repo asks for it (live mode: `Closes #<number>`). Every ticked checkbox is true of the diff and evidence (live mode: the CI box is left unticked). Every ask the repo states (a required file like a changelog entry, a disclosure, small PRs, referencing the issue) is met, and the AI-use disclosure is present wherever the repo's policy or template asks for it (live mode: Notes for Reviewers, in the student's own words). Maintainer direction in the thread is engaged, not ignored. If the repo has no PR template, there are no sections to fail, but the description must still meet whatever asks the contribution docs state. Boilerplate, empty sections, or a visibly ignored ask fails. Whether claims match the diff is plan fidelity, above, not this section.