---
name: write-plan
description: Writes a step-by-step plan broken into bite-sized chunks for review, with a suggested commit message per chunk.
argument-hint: [description-of-the-work]
allowed-tools: [Read, Glob, Grep, Bash(git log:*), AskUserQuestion]
disable-model-invocation: true
---

Write a plan for the following work:

$ARGUMENTS

If no work was described, ask what it is instead of guessing.

## Process

1. **Explore first.** Use Read, Glob, and Grep to understand the relevant code before planning. Cite real file paths. Do not invent files or APIs.
2. **Clarify.** If requirements are ambiguous or there are meaningful design choices, ask with AskUserQuestion before writing the plan.
3. **Check commit style.** Run `git log --oneline -20` and match the repo's convention. If there is no clear convention, use Conventional Commits.
4. **Write the plan.** Output it in chat. This skill only plans: do not implement and do not edit files.

## Chunking rules

- Each chunk is one logical change with a clear boundary.
- Each chunk leaves the build and tests passing.
- Keep chunks small enough to review easily (roughly 5 files or ~200 lines of diff at most). Split anything larger.
- Order chunks so foundational or risky work comes first. Note any dependency on earlier chunks.

## Output format

Start with a one-to-two sentence summary of the approach.

Then, for each chunk:

### N. Title
- **Goal:** one line
- **Files:** paths touched
- **Steps:** short bullet list
- **Verify:** test or command that proves the chunk works
- **Commit:** `suggested commit message`

End with an **Assumptions & open questions** section listing assumptions made, unknowns, and anything explicitly out of scope.
