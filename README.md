# How I Use LLMs

This repo documents how I use LLMs in my day-to-day work, both in professional and personal projects. It covers the principles I follow, my workspace, and the workflows I use to take a task from idea to artifact.

## Principles

* **LLMs are a tool, not a replacement for people.** LLMs are trained on existing knowledge, so relying on them alone means accepting mediocrity. They are not artificial general intelligence, regardless of what OpenAI, Anthropic, and other large tech companies want you to think from their marketing. Remarkable work comes from human ingenuity, which can be aided by tools.
* **A human is always involved.** That means the idea, the execution, and the publishing. This applies to any task I hand to an LLM, not just software engineering. I never unquestioningly accept the result.
* **I don’t use MCPs.** They give the tool too much autonomy and skip the chance for a human to review what is happening.
* **Scripts over prompts.** When an LLM needs data, I have it write a script to pull it from APIs. I can review the code, run it on my terms, and check the data before the LLM consumes it. In the same vein, I will have the LLM write scripts for repetitive tasks, since they are more consistent than a simple prompt.

## Workspace

This is how I’ve set up my workspace to work with LLMs.

### Global .gitignore

In my home directory, I have a `.gitignore` file that includes the following:

```
llm_*.md
llm_*.htm
llm_*.html
llm_*.txt
llm_*.json
llm_*.yml
llm_*.yaml
llm_*.csv
```

These `llm_` files are where I store generated plans/reports and data I want to provide to the LLM. This global git ignore file is also a nice place to store OS specific git ignores. To make Git honor this global `.gitignore`, you will need to modify `.gitconfig` to include the following:

```
[core]
	excludesFile = ~/.gitignore
```

### Global Instructions

These are things I want my LLMs to follow globally across all tasks, not just one project. Below is a summary, but for how the global instructions work, see [workspace/global-instructions.md](workspace/global-instructions.md). Depending on your harness, you would put this in different places. (e.g. `~/.claude/CLAUDE.md` or `~/.continue/rules/*.md`)

- Never run `git commit` or `git push`
- Use Conventional Commit when suggesting commit messages
- Always ask before making any calls to external APIs
- Ask before adding features not requested or not laid out in the plan
- Preferred tooling (PNPM, Vite, Vitest, Oxlint, Oxfmt, etc.)
- Rely on self-documenting coding styles over comments

### Firefox

I mainly use a web browser for LLMs outside of Software Engineering tasks, whether that's for Claude, Grammarly, or Open WebUI. My browser of choice is Mozilla Firefox because it supports a free and open internet and is committed to privacy. With that being said, I do turn off all “AI” options within Firefox, and I use DuckDuckGo with its “AI” features turned off.

### VSCodium

VSCodium ([link](https://vscodium.com/)) is not a fork of Microsoft’s Visual Studio Code, but instead a set of scripts to automatically build VSCode into freely licensed binaries with a community-driven default configuration. (With free meaning freedom, not price.) It strips out all telemetry and tracking and builds it under the MIT license. It also relies on [open-vsx.org](https://open-vsx.org), an open-source registry for Visual Studio Code extensions, instead of Microsoft’s marketplace.

An IDE is still an important part of my workspace as a software engineer, so I stay involved with the code, unlike headless agents and terminal-based chat options. Below are some extensions I use related to LLMs:

- [Claude Code for VS Code](https://open-vsx.org/extension/Anthropic/claude-code)
- [Continue - open-source AI code agent](https://open-vsx.org/extension/Continue/continue)

In addition, some nice-to-have extensions I use:

- [EditorConfig](https://open-vsx.org/extension/EditorConfig/EditorConfig)
- [GitLens — Git supercharged](https://open-vsx.org/extension/eamodio/gitlens)
- [Go](https://open-vsx.org/extension/golang/Go)
- [Oxc](https://open-vsx.org/extension/oxc/oxc-vscode)

## Workflow

These are some common workflows in my day-to-day job. Anything italicized is where LLMs are used to assist in that task.

### Planning Work

1. Navigate to the project in my terminal
2. Check out the default branch
3. Pull the latest
4. _Create a new chat session and use a medium model, such as Sonnet, to request the story; see the write story skill_
5. Create the story in project management software

### Small One-off Code Changes

1. Navigate to the project in my terminal
2. Check out the default branch
3. Pull the latest
4. Create a new feature branch
5. Open the project in VSCodium
6. _Create a new chat session and use a medium model, such as Sonnet, to request the small one-off change_
7. Review the work in VSCodium
   - Optionally, either manually make changes or go back to the chat session and request changes
   - Optionally, if there is no story for this work, I’ll use my write story skill to have it write a story for the work done
8. Commit the changes and push to the remote in my terminal
9. Create a pull request

### Large Code Changes

1. Navigate to the project in my terminal
2. Check out the default branch
3. Pull the latest
4. Create a new feature branch
5. Open the project in VSCodium
6. Pull down the story for the work to be done as a Markdown file in the root of the project
7. _Create a new chat session and use a larger model, such as Opus, to request a plan for the changes; see the plan skill_
8. Read through and review the plan
   - Optionally, either manually make changes to the plan or go back to the chat sessions and request changes
9. Write the plan to the root of the project as `llm_short_description_of_plan.md`
10. _Create a new chat session and use a medium model, such as Sonnet, to start working on a step of the plan_
11. Review the work in VSCodium
    - Optionally, either manually make changes or go back to the chat session and request changes
12. _Open the original chat session with the larger model and have it review the work in my staged changes according to the plan it wrote_
13. Review feedback
14. Commit the changes to my local branch
15. Repeat steps 9-12 until all steps are complete
16. _Open the original chat session with the larger model and have it review all of the work according to the plan it wrote_
17. Review feedback
    - Optionally, either manually make changes or go back to a chat session and request changes
18. Create a pull request
