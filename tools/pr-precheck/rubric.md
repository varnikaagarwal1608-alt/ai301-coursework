# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diff within plan | The diff's changed files and hunks, read against the plan's stated files and boundary plus its Deviations section | Every changed file and hunk is named by the plan or recorded under Deviations, and every change the plan promised is in the diff or disclosed as left out. A change that only exists in the diff, or a planned change silently missing, fails. | required |
| Description matches diff | Each factual claim in the PR description (fidelity claims like "exactly as planned" or "no options added", the Changes bullets, checklist items like "changelog added"), read against the diff | Every claim about what the PR changed or added is true according to the diff. A claim the diff contradicts, or one with nothing in the diff behind it, fails. A claim that something was not added passes if nothing in the diff adds it. | required |
| Tests exist | The description's claims about tests and the plan's test plan, read against the test files in the diff | The diff contains a regression test for the issue's own scenario (the input that triggered the bug), and every test the description claims to have added is in the diff. A plan control that the evidence reports as checked and unchanged does not need its own new test. A claimed test that is not in the diff fails. | required |
| Evidence is observable | The test evidence section: the before and after of the issue's scenario, and the checks the repo's own facts name | The issue's scenario has a before result and an after result that show the behavior changing as the issue expects, as printed output or as a specific stated result (for example the exact output line, or "1462 passed"). The repo's required checks are reported as run, with counts or output, or an honest note saying why not. Fails only if the decisive before/after is missing, vague ("it works"), contradicts the fix, or a required check is silently absent. Side claims such as "controls unchanged" or "lint clean" do not fail this check by themselves. Do not demand checks the repo never names. | required |
| Test plan covered | The plan's test plan read against the test evidence and the test files in the diff | The plan's main scenario (re-running the issue's scenario) and its suite run are covered in the evidence. Secondary scenarios the plan names are covered if the evidence states them as checked or a test in the diff exercises them. Fails if the main scenario was never re-run, or a named scenario is neither mentioned in the evidence nor in the diff nor disclosed as skipped. | required |
| Diff is clean | Every hunk in the diff | No debug lines, no commented-out code, no stray files, no unrelated reformatting or edits that bury the change. An unrelated hunk fails even if the description explains it. | required |
| Template filled | The repo-facts block's description of the PR template (or the live template file) read against the description | Every section or ask the repo's template states has real content for this change. Linking the issue by number counts when the repo asks for it or the PR names the issue. Judge only the sections the repo's template names, not a generic template. Placeholder text, empty sections, or a ticked box the diff contradicts fails. If the repo has no template, this passes. | required |
| Repo's stated asks | The repo's stated rules (PR template, CONTRIBUTING, AI-use policy) read against the description and diff | Every ask the repo states for a PR is met, including the AI-use disclosure and any required file like a changelog entry. Ignoring a stated ask fails. | required |
| Title and clarity | The PR title and the description's Summary | The title says what the change does, and a reviewer could tell from the Summary why it is needed. | preferred |

## Verdict rule

- Accept if every required check is graded pass.
- Any required check graded fail means reject.
- A check graded unclear counts as fail.
- Preferred checks never change the verdict.
- Honest disclosure counts: if the PR leaves something out or changes something the plan did not name, and the description and the plan's Deviations both say so, the matching check passes. A shortfall that is only discovered by reading the diff fails.