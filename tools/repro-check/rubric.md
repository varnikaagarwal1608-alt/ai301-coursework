# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment recorded | Repro report's environment section | Report states OS, runtime, and dependency versions specific enough that someone else could rebuild the same setup without guessing | required |
| Steps complete and followable | Repro report's steps section | Each step is a concrete, ordered action (exact command, input, or file) that could be repeated verbatim to reach the same point | required |
| Behavior matches the issue | Output/error/log excerpt in the repro report, read against the issue's description | The shown behavior is the same behavior the issue describes, not an adjacent or similar-looking one | required |
| Outcome stated honestly | The report's stated conclusion, read against its own evidence | A cannot-reproduce conclusion backed by the same rigor (environment + steps + attempted behavior) passes; a confident reproduction not actually backed by the shown evidence fails | required |
| Claim promises, doesn't assert | Claim comment text | Claim names the issue and states investigation is starting, with no fix, no date, and no asserted root cause | required |
| Disclosure respects repo convention | Comment text, read against the repo-facts block's disclosure policy | If the repo requires disclosing AI assistance, the comment discloses it; if no such policy exists, this check passes automatically | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept if every required check passes. There are no preferred checks in this rubric. Any check marked "unclear" is treated as a fail — accept only on a clean pass across all required checks.
