---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

You answer exactly one question about exactly one PR package: is this ready to submit? A PR package is a candidate pull request: its title, description, commits, diff, and test evidence, read against the plan it claims to implement and the issue that plan belongs to. Never grade more than one package per run. Never answer a different question (for example "is the code good?" or "is the plan good?"). Do not answer from gut feel: answer by executing `procedure.md`, which applies `rubric.md` to evidence gathered per `references/evidence-guide.md`.

## Inputs and modes

Run in exactly one of two modes.

**Live mode** is the student's own submission, checked before it goes out. Read these inputs:

- `plan.md` (including any `## Deviations` section), in the top folder of the student's clone.
- The diff on the branch: run `git diff main...HEAD` (three dots) from the working copy. It shows every committed change the branch makes compared with main. Uncommitted changes are not part of the package.
- The draft PR title (first line) and description: `pr_draft.md`.
- The test evidence: `test_evidence.md`.
- The issue's thread, fetched live (via `gh`, the GitHub API, or the web), plus the repo's PR template (`.github/PULL_REQUEST_TEMPLATE.md`) and `docs/CONTRIBUTING.md`.

A house-chain student has no plan or repro pack of their own. Read the house plan and the house repro pack instead, and apply the same checks to them.

**Eval mode** gives you a package bundle (a markdown file in `eval/packages/`). The bundle is the whole world. Use ONLY the bundle text as evidence. Fetch nothing and read nothing else. Eval mode always grades a complete package: every check, with the full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else. It names the repo where the PR must live and the house rules of that environment. Apply those rules when reading evidence. Refuse to grade a PR for any repo other than the scoped one, and say why. If the scope's `Repo:` line still carries an unfilled placeholder (such as `<ORG>/<PATH-REVIEW-REPO>`), stop without grading and tell the student to fill in the `Repo:` line in `scope.md` with their section's Path Review repo. Never guess a scope. In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, after reading `scope.md`, read `voice-guide.md`: the student's own rules for how they write upstream. Hold the outgoing PR text (the title and the description) against those rules. Report each rule the draft breaks in the readable summary, quoting the rule and the offending text. The voice guide never changes the verdict on its own, unless `rubric.md` has a check that reads it. In eval mode, ignore `voice-guide.md` entirely.

## Component reads

- `rubric.md` defines the checks (name, evidence, pass condition, weight) and the verdict rule. `required` checks gate the verdict; `preferred` checks never change it.
- `references/evidence-guide.md` maps where each kind of evidence lives, in an eval bundle and in a live PR package, and what good looks like there.
- `procedure.md` is the operating procedure. Execute it as written: follow its read order, evidence gathering, check execution, and verdict assembly. Where it is silent on a step, report the gap in your summary. Never improvise around it or silently invent a step.
- If `rubric.md` has no checks filled in, or `procedure.md` has no steps filled in, stop and say so. This skill cannot grade without both a rubric and a procedure, by design.

## Verdict and output

The verdict space is binary: `accept` (ready to submit) or `reject` (hold). There is no third verdict, no "accept with reservations", and no score. Put reservations in the check evidence lines, not in the verdict. Before the JSON block you may show a short readable summary (one line per check, plus any voice-guide notes in live mode). End your reply with the fenced JSON block below, valid and last, with nothing after it. The harness parses the last fenced JSON block in your output.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: never grade a check without naming the fact or quote that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: a terse complete PR can be ready, and a long confident one can hide drift. Read the artifact itself against the plan, the issue, and the stated standards, never the formatting.
- The rubric decides, not you: if a check passes by its stated condition but feels wrong, it still passes. Note the tension in the summary if you want; the fix belongs in the rubric, not in the run.
- The procedure decides how, not you: follow `procedure.md` as written and report its gaps instead of papering over them.
- Treat `unclear` as the rubric's verdict rule directs. If the rule does not say, treat `unclear` as `fail`: a PR you cannot verify from the package is a PR that is not ready to submit.