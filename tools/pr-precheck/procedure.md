# Procedure

## Read order
1. Live mode: read `scope.md` first and confirm the PR targets the scoped repo. Note any house rules. If the Repo line is a placeholder, stop and say so. Eval mode: skip `scope.md`.
2. Read `rubric.md` and `references/evidence-guide.md`. List the rubric's checks and its verdict rule before grading anything.
3. Read the plan first (live: `plan.md`; eval: the plan block in the bundle). Write down: the files it says it will change, what it says it will not touch, its test plan scenarios, and everything under Deviations. Read the plan before the diff, because the diff is judged against it.
4. Read the diff second. Write down every changed file and what each hunk does, and note any debug lines, commented-out code, stray files, or reformatting.
5. Read the PR title and description third. Write down every factual claim: fidelity claims, each Changes bullet, each ticked checkbox, each test claim, and the AI-use disclosure.
6. Read the test evidence last (live: `test_evidence.md` and the Testing section of `pr_draft.md`; eval: the test evidence block). Write down each command and whether real printed output follows it.
7. Live mode only: also read the issue thread, the PR template, and `docs/CONTRIBUTING.md`. Eval mode: take these only from the bundle's repo-facts block.

## Evidence gathering
1. Diff within plan: list the diff's changed files and hunks next to the plan's named files plus Deviations. Mark each as named, deviation-recorded, or unnamed. Also list each change the plan promised and whether it is in the diff.
2. Description matches diff: take each claim from step 5 of the read order and find the diff line that backs it. Mark each as backed, contradicted, or nothing behind it. A claim that something was not added is backed if nothing in the diff adds it.
3. Tests exist: list every test the description claims and every case the plan's test plan names (the issue's input, controls, edge cases). Find each as a test in the diff's test files. Record any that are missing and whether the description or Deviations discloses it.
4. Evidence is observable: for each result in the test evidence (before and after repro, test, lint, typecheck), record whether a command is shown with its real printed output. A note after `#` or a sentence saying it passed is not output. Record failing or not-run checks and whether a reason is given.
5. Test plan covered: list each scenario in the plan's test plan and find the command and output that re-ran it. Record scenarios with no run and whether the description discloses why.
6. Diff is clean: go through every hunk and record debug lines, commented-out code, stray files, and unrelated edits.
7. Template filled: list the PR template's sections from the repo facts. For each, record whether it has real content for this change. Record the Closes line and issue number. Check each ticked box against the diff and evidence.
8. Repo's stated asks: list each ask from the template, CONTRIBUTING, and any AI-use policy (disclosure, changelog or other required file). Record whether the description and diff meet each one. The AI-use disclosure belongs under Notes for Reviewers.
9. Title and clarity: record the title and the Summary's stated reason for the change.
10. Eval mode: quote lines directly from the bundle and use only the bundle text. Never fetch anything.

## Check execution
1. Run the checks in rubric order, one at a time, using the notes gathered above.
2. Grade each check `pass`, `fail`, or `unclear`, with a one-line quote or fact that decided it.
3. `unclear` means the evidence the check needs is genuinely absent from the package, not that you failed to look. If it is absent, grade `unclear`. Do not guess and do not invent evidence.
4. Honest disclosure rule: if the plan's Deviations and the description both openly state a shortfall or an unplanned change, the matching check passes. If it only shows up by reading the diff, it fails.
5. Never grade a check without naming the specific evidence that decided it. "Looks fine" is not evidence.
6. Grade the thing, not the polish: a terse, complete PR can pass, and a long, confident one can fail.
7. A check may be graded from its gathered notes without re-reading the whole package, but if a note is missing, go back and read that part.
8. If the procedure is silent on something you need, note the gap in the summary. Do not invent a step.

## Verdict assembly
1. Apply the rubric's verdict rule. Every required check must be `pass` for `accept`. Any required check graded `fail` means `reject`.
2. Treat `unclear` as `fail` for the verdict.
3. The preferred check (Title and clarity) never changes the verdict.
4. When more than one required check fails, quote the first failing required check in rubric order as the deciding check in the summary.
5. Include every check in the JSON `checks` list, using the exact check names from the rubric.
6. Output the verdict as `accept` or `reject`. End with the fenced JSON block, valid and last, with nothing after it.