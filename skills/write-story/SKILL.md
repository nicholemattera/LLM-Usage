---
name: write-story
description: Writes a user story with acceptance criteria and a story point estimate for described work.
argument-hint: [description-of-the-work]
allowed-tools: [Read, Glob, Grep, AskUserQuestion]
disable-model-invocation: true
---

Write a user story for the following work:

$ARGUMENTS

If no work was described, ask what it is instead of guessing.

If the work refers to code, read it to confirm what needs to change, then use that to choose the roles and estimate.

Requirements:
- **Title:** short and to the point.
- **User stories:** try to stick to a single user story when possible. If the work affects more than one role write a user story for each role. A user story is a single sentence in the form "As a <role>, I can <activity> so that <business value>." If the role isn't obvious, pick the most plausible one.
- **Acceptance criteria:** 3-6 bullets, each starting with "Verify that...". Describe observable end results, not implementation steps. Keep them conceptual but testable. Cover every user story with at least one criterion.
- **Projected Story Points:** estimate in Fibonacci points (1, 2, 3, 5, 8, 13...). A story must be 8 points or fewer. If it's more, follow the split steps below.

If the estimate is above 8 points, don't output a story yet:

1. Ask the user clarifying questions about scope, priorities, and anything that would change the estimate or the natural boundaries of the work. Ask only what you need, at most a few questions. Use AskUserQuestion.
2. Recommend a split into stories of 8 points or fewer. Present it with AskUserQuestion, recommended split first, so the user can confirm or adjust.
3. Once the user confirms or adjusts the split, output one story per piece using the structure below, each with its own title, criteria and points.

Output as rendered markdown (not inside a code fence) using this structure:

# Title

As a ..., I can ... so that ...

(repeat per role)

## Acceptance Criteria

- Verify that ...
- Verify that ...

**Projected Story Points:** ...

Example:

# Password Reset by Email

As a registered user, I can reset my password through an emailed link so that I can regain access to my account without contacting support.

As a security administrator, I can have reset links expire and be single-use so that stolen or forwarded emails can't be used to take over accounts.

## Acceptance Criteria

- Verify that requesting a reset for a registered email address sends a reset link to that address.
- Verify that requesting a reset for an unregistered email address shows the same confirmation message and sends no email.
- Verify that the reset link expires after 60 minutes and cannot be used a second time.
- Verify that submitting a new password that meets the password rules lets the user sign in with it, and the old password no longer works.

**Projected Story Points:** 5
