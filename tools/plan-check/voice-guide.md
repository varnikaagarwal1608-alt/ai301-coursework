# Voice guide: how I talk upstream

## Who I am in threads

I'm a student investigating this issue as coursework, not a maintainer
and not an expert in this codebase. I say so plainly when it's
relevant, and I don't imply authority or experience I don't have.
Readers can expect a genuine, evidenced attempt at reproduction — not
a fix, not a timeline, and not confidence I haven't earned.

## Rules I write by

### Rule: Promise, don't assert

A claim comment says what I'm about to investigate, never what I've
already concluded.

- Wrong: "This is caused by the retry logic timing out."
- Right: "Starting to investigate — will report back with what I find."

### Rule: Show it, don't just say it

A repro comment includes the actual output/error, not just my summary
of what happened.

- Wrong: "I ran it and it crashed with the same error."
- Right: "Ran `npm test`; here's the exact stack trace: [output]."

# Voice guide: how I talk upstream

## Who I am in threads

I'm a student investigating this issue as coursework, not a maintainer
and not an expert in this codebase. I say so plainly when it's
relevant, and I don't imply authority or experience I don't have.
Readers can expect a genuine, evidenced attempt at reproduction — not
a fix, not a timeline, and not confidence I haven't earned.

## Rules I write by

### Rule: Promise, don't assert

A claim comment says what I'm about to investigate, never what I've
already concluded.

- Wrong: "This is caused by the retry logic timing out."
- Right: "Starting to investigate — will report back with what I find."

### Rule: Show it, don't just say it

A repro comment includes the actual output/error, not just my summary
of what happened.

- Wrong: "I ran it and it crashed with the same error."
- Right: "Ran `npm test`; here's the exact stack trace: [output]."

### Rule: Say "couldn't reproduce" as confidently as "reproduced"

A cannot-reproduce result gets the same evidence and the same
directness as a successful one — no hedging it away.

- Wrong: "Hmm, not totally sure, might just be me, sorry!"
- Right: "Could not reproduce after 3 attempts with this exact setup:
  [environment + steps]. Here's what I tried."

### Rule: No piggybacking on shared issues

Even if a classmate already commented on this issue, I post my own
proof, in my own words, from my own environment.

- Wrong: "Same as above, can confirm."
- Right: "Confirmed independently — here's my environment and what I
  observed: [details]."
### Rule: A plan asserts, a claim promises

Unlike a claim comment, a plan comment states a conclusion on
purpose: the diagnosis and the proposed fix, backed by the repro
evidence already posted. "Promise, don't assert" governs claim
comments; a plan comment does the opposite by design, because its job
is to propose, not to announce intent to investigate.

- Wrong (treating a plan like a claim): "Starting to look into
  whether this might be a refresh issue, will report back."
- Right: "The post-push refresh scope misses the branch-commits
  context; proposing a one-line addition to the push callback's
  refresh scope."

### Rule: Name the repo's own review norms when they apply

If the repo's contribution policy says something about review
bandwidth, AI-generated PR scrutiny, or scope preferences, a plan
comment acknowledges it rather than ignoring it.

- Wrong: promising a broad refactor when CONTRIBUTING.md says review
  time is scarce.
- Right: "Keeping this minimal given the review-bandwidth note in
  CONTRIBUTING."

## Things I never post

- A fix or a timeline in a claim comment.
- A root cause I haven't actually verified with evidence.
- "Same as above" or any restatement of someone else's reproduction as
  my own.
- An apologetic or uncertain tone standing in for missing evidence.