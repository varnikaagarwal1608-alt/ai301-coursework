# Unit 4 — Test and Submit

## Your pull request

### Pull request
https://github.com/codepath/pathreview-ai301-fa26-s3/pull/224

### Branch
fix/24-role-switch-whitespace

## Eval iterations

### Run history
Scores in order: 2/3 (smoke run, `--limit 3`), 0/1 (`--only pkg-02`), 3/3 (`--only pkg-02,pkg-01,pkg-03`), 14/19 (first full run; pkg-05 errored on a Windows cp1252 encoding error, so nothing was saved), 0/6 (`--only` on the six clear accepts), 9/10 (the six clear accepts plus four not-tested rejects), 19/20 (final full run, saved with `--save-run`). The last score matches the line in my committed eval-run.txt: "agreement: 19/20 scored items  (bar: 18/20: PASS)".

### Package analysis
Package: pkg-11 (ripgrep#3477, a clear-accept).

My rubric decided reject; the gold label is accept. My rubric failed it on Description matches diff, Tests exist and Evidence is observable. The grader's reason for Description matches diff was: "Description claims tests for 'escaped, unescaped, and double-backslash cases' but the one new test covers only escaped and double-backslash; no unescaped-trim case exists."

The PR description says "tests added for the escaped, unescaped, and double-backslash cases", but the diff adds one test, `escaped_trailing_space_is_kept`, which covers the escaped and double-backslash cases and has no unescaped case. My rubric says "A claimed test that is not in the diff fails," so it rejected the overclaim. I think that is a defensible reading, and I left the rule alone. Loosening it to flip pkg-11 would risk the reject packages that depend on the same rule. I count pkg-11 as one of the arguable packages.

### Check rationale
This is the Evidence is observable row from my uploaded rubric.md, exactly as it reads now:

| Evidence is observable | The test evidence section: the before and after of the issue's scenario, and the checks the repo's own facts name | The issue's scenario has a before result and an after result that show the behavior changing as the issue expects, as printed output or as a specific stated result (for example the exact output line, or "1462 passed"). The repo's required checks are reported as run, with counts or output, or an honest note saying why not. Fails only if the decisive before/after is missing, vague ("it works"), contradicts the fix, or a required check is silently absent. Side claims such as "controls unchanged" or "lint clean" do not fail this check by themselves. Do not demand checks the repo never names. | required |

Why it reads this way: my first version required "a command plus its real printed output" for every result. On pkg-02 that rejected a clear accept for a bare "pytest ... passes
