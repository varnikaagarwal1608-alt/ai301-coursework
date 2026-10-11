# Evidence guide

Where each rubric check's evidence lives in a package, and what good
looks like there.

## Diagnosis

**Where it lives:** the `Cause:` line at the start of the "Candidate
plan" section.

**What good looks like:** the cause names a specific mechanism, not
just a symptom, and it's checkable against the "Repro evidence"
section above it. In calib-01, the plan's cause ("after a push...that
view's model is not refreshed...until the view is rebuilt on
re-entry") directly explains the repro's observed behavior (color
only updates after Esc and re-entry). A fail or unclear looks like a
cause that restates the issue's symptom ("pushing doesn't update the
color") without saying why, or a cause that the repro evidence doesn't
actually support.

## Scope

**Where it lives:** the `Change:` line in "Candidate plan", usually
split into `In:` and `Out:` statements.

**What good looks like:** at least one specific file or component
named for `In:`, and an explicit `Out:` statement naming what won't be
touched. calib-01's plan names
`pkg/gui/controllers/sync_controller.go` for `In:` and explicitly
excludes "how push status is computed" and "other views' refresh
behavior" for `Out:`. A fail looks like a plan that only says what it
will change with no `Out:`, or names a file but not what inside it
changes.

## Test plan

**Where it lives:** the `Test:` line in "Candidate plan".

**What good looks like:** concrete steps tied back to the repro
(re-running or extending it), with a stated expected outcome. calib-01
reuses the repro steps and adds two extra checks (main commits panel,
force push) with a clear pass condition ("color must flip without
leaving the view"). A fail or unclear looks like "will add tests" with
no steps, or steps that don't map back to the actual repro behavior.

## Thread & convention

**Where it lives:** compare the "Candidate plan comment" section
against two places: the "Thread highlights" section (does the comment
contradict anything already said on the issue?) and the "Repo facts"
section's `contribution policy` line (does the comment's approach fit
how the repo says it reviews contributions?).

**What good looks like:** the comment doesn't conflict with existing
thread discussion, and it respects stated repo norms. calib-01 has
zero thread comments (nothing to contradict), and the plan comment
explicitly acknowledges the contribution policy's review-bandwidth
note ("keeping it minimal given the review-bandwidth note in
CONTRIBUTING"). A fail looks like a comment that ignores or
contradicts a maintainer's stated preference in the thread, or that
ignores a repo policy that plainly applies (e.g. promising a large
PR when the repo says review bandwidth is scarce).