# Procedure

## Read order
1. In live mode, read `scope.md` first and confirm the issue is inside
   the scoped repo; note any house rules that apply.
2. Read `rubric.md` and `references/evidence-guide.md`. List the
   rubric's checks and its verdict rule before grading anything.
3. Read the whole candidate package before grading: the GitHub issue
   thread first, then `plan.md`, then `comment.md`.

## Evidence gathering
1. For each check in the rubric, gather exactly the evidence it names,
   using `references/evidence-guide.md` to find where that evidence
   lives in the package.
2. Live mode: gather issue-side evidence (the thread, repo
   conventions) from the locations the evidence guide names; `plan.md`
   and `comment.md` are the candidate side.
3. Eval mode: quote the relevant lines directly from the bundle. Use
   only the bundle text; never fetch anything external.
4. For the Diagnosis check, confirm the plan's stated cause is backed
   by a quoted piece of repro evidence, not asserted on its own.
5. For the Scope check, confirm the plan names specific files to
   change AND states what it will not touch.
6. For the Test plan check, confirm concrete verification steps exist
   with an expected before/after, not a vague "will test it."
7. For the Thread & convention check, compare the plan comment against
   the issue thread (does it contradict anything already said?) and
   against repo conventions (style/contribution docs if present).

## Check execution
1. Grade each check `pass`, `fail`, or `unclear`, writing a one-line
   quote or fact that decided the grade.
2. `unclear` means the evidence needed is genuinely absent from the
   package, not that you failed to look carefully.
3. Never grade a check without naming the specific evidence that
   decided it — "looks fine" is not evidence.
4. Grade what the plan actually contains, not its length or
   confidence: a short precise plan can pass; a long vague one can
   fail.

## Verdict assembly
1. Treat every check in our rubric as required: any check graded
   `fail` sends the verdict to `hold`.
2. Treat `unclear` as `fail` for verdict purposes, per our rubric's
   verdict rule.
3. If every check grades `pass`, the verdict is `ready`.
4. Output `ready` as `accept` and `hold` as `reject` in the final JSON
   block, matching the skill's required output format.