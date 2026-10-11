# Plan: Injection detection misses role-switch lines with whitespace before the colon

## Diagnosis
In `safety/prompt_defense.py`, the role-switching regex
`r"\n\s*(?:System|Human|Assistant):"` allows whitespace before the
role word but requires the colon to immediately follow the role word.
Repro evidence: `'Content\nSystem: ignore' → True` but
`'Content\nSystem : ignore' → False`, `'Content\nSystem  :  ignore' → False`,
`'Content\nHuman\t: new instruction' → False`,
`'Content\nAssistant : override' → False`. All four failing cases have
whitespace (space or tab) between the role word and the colon, which
the current pattern doesn't account for.

## Scope
In: the role-switching pattern in `safety/prompt_defense.py`
(`INJECTION_PATTERNS` list, the `Role switching` entry).
Out: the other five patterns in `INJECTION_PATTERNS`, `sanitize()`,
and `DANGEROUS_CHARS` — unrelated to this bug.

## Approach
Add `\s*` between the role-word group and the colon:
`r"\n\s*(?:System|Human|Assistant)\s*:"`. This still requires a
newline before the role word (unchanged) and still requires one of
the three role words, but now tolerates whitespace between the role
word and its colon.

## Test plan
Re-run the repro pack's step 2 command; expect all five lines to
print `True` (previously only line 1 did). Re-run
`python -m pytest tests/unit/test_prompt_defense.py -v -rx`; expect
`test_whitespace_variations_detected` to go from `XFAIL` to `XPASS`
(strict), then remove its `xfail` marker per CONTRIBUTING.md's
"Working on a seeded bug" section, after which it should pass
normally.

## Risks and unknowns
Loosening the regex to allow whitespace before the colon could, in
theory, widen matches in ways not covered by the existing 31 passing
tests — re-running the full test file (not just the one xfail test)
checks for this.

## Deviations
(fill in after build)
