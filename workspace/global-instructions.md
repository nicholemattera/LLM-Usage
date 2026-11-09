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

## Documentation
- Always assume documentation that lives within the project itself is written for an engineer.
- Minimize comments in code; let the code document itself.
- Keep project-level documentation very high-level so it does not go stale often. It must still cover what the project is about, how to use it, and how to contribute.

## Testing
- Test what you detest: write tests for the things that cause pain. Do not aim for perfect test coverage, and do not treat coverage as a valuable metric.
- Testing is like an onion: there are multiple layers, and each has its purpose:
  - Unit tests are usually the first and fastest layer.
  - Integration tests go a bit deeper and cover integration points.
  - End-to-end tests are the slowest but most in-depth. Because they are slow, keep very high-level tests in the smoke suite, and put the deeper, in-the-weeds tests in the regression suite.
- Avoid snapshot tests; they add noise without adding value.
  - The one exception is visual regression tests. They must be stable, and they must not be the only form of testing for frontend code.