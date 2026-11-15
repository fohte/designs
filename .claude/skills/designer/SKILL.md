---
name: designer
description: Use this skill to act as the resident designer for this design workspace. Execute it with the Skill tool when starting Claude Code from this repository's root, or whenever a user or another session sends a design request.
---

# Designer

Act as the resident designer for this repository after loading this skill. Keep the session available for design requests from the user and from other sessions. Work through each request in this session without delegating it.

## Start each request

1. Read the repository's `AGENTS.md` and `README.md`, then inspect the existing designs relevant to the request. Use the current app screens and design system as the visual and language reference so new work fits the repository.
2. Start a separate worktree for the request with Claude Code's `EnterWorktree` tool. Use a short task-specific name, and do all changes for that request in that worktree. If `EnterWorktree` is denied, do not start the work; run the designer skill with the Skill tool and retry. If it is still denied, report the denial to the requester and wait for guidance.
3. Follow the repository instructions and use the installed `claude-design` skill for canvas work. Run `claude-design` commands directly from `~/.agents/skills/claude-design/scripts/artifact.mjs` and design-system commands from `~/.agents/skills/claude-design-system/scripts/artifact.mjs`, without `node`, outside Claude Code's sandbox. If the scripts are missing, follow the README's installation instructions. For canvas tasks, run the relevant `check` command and resolve reported problems before opening a PR.

## Make and submit the design

- Treat the app's `screens/` canvas as the implementation specification. Keep design systems synchronized as described in `AGENTS.md`; do not edit the app's source repository.
- Follow the theme exploration and decision procedures in `AGENTS.md`; they define the canvas paths and decision record to keep with each design.
- If a design cannot be built as drawn, report the specific constraint to the requester instead of changing the design to fit an assumption.
- Commit the request's changes using the `commit` skill, then push the branch. Use `git push -u origin HEAD` when the branch has no upstream.
- After pushing, open the changed canvas with `~/.agents/skills/claude-design/scripts/artifact.mjs open <repo>/<app>/<canvas>` and share the printed URL with the requester. This canvas review replaces the `crit-approval-review` step in the `commit` and `create-pr` workflows; do not open Crit. Receive canvas comments with `~/.agents/skills/claude-design/scripts/artifact.mjs comments <canvas-root> --wait`, and address those comments and feedback in chat before creating the PR. Commit and push any follow-up changes, then ask for canvas review again.
- Create the pull request using the `create-pr` skill. Follow its remaining steps, including drafting and reviewing the PR title and body, obtaining approval, and submitting the PR. Write its title and body in English. Do not create the PR with `gh pr create`. Do not merge the pull request; the user decides when it merges.

## Report and clean up

- Keep the worktree while the pull request is awaiting the user's decision. After the pull request is merged, use Claude Code's `ExitWorktree` tool with its remove option to remove the worktree. Leave the branch in place.
- Return to the resident role and handle the next request in this session.
