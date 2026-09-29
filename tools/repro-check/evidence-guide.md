# Evidence guide: where proof lives in a reproduction package

## Environment

Where it lives: the environment record in the repro report (OS, runtime
version, dependency versions, or a lockfile reference), read against
the versions the issue itself targets.

What good looks like: the named versions match what the issue targets,
or any difference from the issue's stated target is explicitly called
out rather than left silent.

## Steps

Where it lives: the ordered steps section of the repro report, from
starting state to the point the bug triggers.

What good looks like: each step is a concrete, repeatable action (an
exact command, input, or file change) — a stranger starting from the
same state could follow them and land on the same trigger point, with
no step requiring them to guess or infer what was actually done.

## Behavior shown

Where it lives: pasted output, error text, log excerpts, or screenshots
attached to the repro report — not the author's prose summary of them.

What good looks like: the shown artifact demonstrates the same behavior
the issue describes (same error, same symptom, same trigger condition),
not a similar-looking but different behavior from an adjacent part of
the system.

## Honesty

Where it lives: the report's stated conclusion, read directly against
its own attached evidence (steps + behavior shown).

What good looks like: the conclusion claims no more than the evidence
supports. An honest "could not reproduce" backed by the same rigor
(environment, steps tried, behavior attempted) counts as sufficient
evidence. A "reproduced" conclusion whose attached artifact doesn't
actually show the issue's behavior does not.

## Comms

Where it lives: the claim comment (read against the issue it names) and
the repro comment (read against the repo's contribution templates and
any stated AI-assistance disclosure policy in the repo-facts block).

What good looks like: the comment is specific to this issue and this
repo, not boilerplate — it names the issue, follows the repo's expected
comment shape, and discloses AI assistance if the repo's policy
requires it. A comment that could be pasted onto any issue unchanged
fails this.