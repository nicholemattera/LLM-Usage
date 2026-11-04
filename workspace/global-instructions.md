# Global Instructions

## Git
- Never run `git commit` or `git push`. I review all work before it goes to remote.
- When suggesting commit messages, always follow the Conventional Commits standard.

## Boundaries
- Ask before making any calls to external APIs.
- Ask before adding features that were not requested or not laid out in plans/stories.

## Preferred Tooling
- Backend web development: Go with `gofmt` and `golangci-lint`.
- Frontend web development: TypeScript with PNPM, Vite, Vitest, Oxlint, and Oxfmt.
- Nintendo switch homebrew development: C++ using the DevkitPro toolchain

## Code Style
- Rely on self-documenting code over heavy use of comments.
- Functions should generally do one job, with a name that describes that job.
- Variable names must accurately describe what they hold.
- Declare variables close to where they are used, and group their uses together.
- Name functions with action verbs.
- Avoid syntax tricks; prioritize readability.
- Avoid magic numbers; use named constants.
