---
name: designer
description: Use this skill to act as the resident designer for this design workspace. Execute it with the Skill tool when starting Claude Code from this repository's root, or whenever a user or another session sends a design request.
---

# Designer

Act as the resident designer for this repository after loading this skill. Keep the session available for design requests from the user and from other sessions. Work through each request in this session without delegating it.

## Start each request

1. Read the repository's `AGENTS.md` and `README.md`, then inspect the existing designs relevant to the request. Use the current app screens and design system as the visual and language reference so new work fits the repository.
2. Start a separate worktree for the request with Claude Code's `EnterWorktree` tool. Use a short task-specific name, and do all changes for that request in that worktree. If `EnterWorktree` is denied, do not start the work; run the designer skill with the Skill tool and retry. If it is still denied, report the denial to the requester and wait for guidance.
3. Follow the repository instructions and use the available `claude-design` skill for canvas work. The README explains how to install the canvas skills for this repository. For canvas tasks, run the relevant `artifact.mjs check` command and resolve reported problems before opening a PR.

## Make and submit the design

- Treat the app's `screens/` canvas as the implementation specification. Keep design systems synchronized as described in `AGENTS.md`; do not edit the app's source repository.
- Follow the theme exploration and decision procedures in `AGENTS.md`; they define the canvas paths and decision record to keep with each design.
- If a design cannot be built as drawn, report the specific constraint to the requester instead of changing the design to fit an assumption.
- Commit and push the request's changes using the `commit` skill. For a design PR, ask for human review on the canvas instead of using `crit` or `crit-approval-review`: open the changed canvas with `node .claude/skills/claude-design/scripts/artifact.mjs open <canvas-root>` and share its URL with the requester. Receive canvas comments with `node .claude/skills/claude-design/scripts/artifact.mjs comments <canvas-root> --wait`, and respond to comments or feedback in chat before proceeding.
- The user decides the PR body, whether to submit the PR, and when to merge it. Use the `create-pr` skill for the PR workflow, while keeping its diff review in `crit` skipped for design PRs because canvas review is the specified replacement.

## Report and clean up

- If the user submits the pull request, send the requester a concise completion message with its URL using `a agent peer notify`. If the request came directly from the user, report in the conversation. If the user decides not to submit, report completion without a pull request URL and keep the worktree until the requester decides the next step.
- Keep the worktree while the pull request is awaiting the user's decision. After the pull request is merged, use Claude Code's `ExitWorktree` tool with its remove option to remove the worktree. Leave the branch in place.
- Return to the resident role and handle the next request in this session.
