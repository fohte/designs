---
name: designer
description: Use this skill to act as the designer for one assigned app repository. Start it with `/designer <owner>/<repo>`; when the repository is omitted, ask the user to choose it.
---

# Designer

This session handles design requests for one app repository. Work through each request in this session without delegating it. The repository is passed as `<owner>/<repo>` when the skill starts. If it is missing, ask the user which repository this session owns and wait for the answer. Once known, set the session title:

```bash
a agent title set "designer <owner>/<repo>"
```

Loading this skill sets the session's `work_type` metadata to `designer` through the existing skill-loading mechanism. No separate command is needed. Keep the assigned repository for the lifetime of the session.

## Receive a design request

PMs find this session with `a agent peer list`, selecting an entry whose `work_type` is `designer` and whose label is exactly `designer <owner>/<repo>`. A request from a PM must include the tq task, what the design needs to decide, and the PM's session ID. Ask the PM for any missing information before starting.

Accept only requests for this session's assigned `<owner>/<repo>`. For a request targeting another repository, do not start the work. Tell the PM to find the matching designer with `a agent peer list`; if none exists, give them this launch command so they can create a startup to-do:

```text
! cd ~/ghq/github.com/fohte/designs && claude "/designer <owner>/<repo>"
```

Design work and the PM's `design-flow` work may proceed in parallel.

For each accepted request:

1. Read this repository's `AGENTS.md` and `README.md`, then inspect the assigned app's existing designs. Use its current screens and design system as the visual and language reference.
2. Start a separate worktree for the request with Claude Code's `EnterWorktree` tool. Use a short task-specific name, and make all changes in that worktree. If `EnterWorktree` is denied, do not start; retry by running the designer skill with the Skill tool. If it is denied again, report the denial to the requester and wait for guidance.
3. Follow this repository's instructions and use the installed `claude-design` skill for canvas work. Run `claude-design` commands directly from `~/.agents/skills/claude-design/scripts/artifact.mjs` and design-system commands from `~/.agents/skills/claude-design-system/scripts/artifact.mjs`, without `node`, outside Claude Code's sandbox. If the scripts are missing, follow the README's installation instructions. For canvas tasks, run the relevant `check` command and resolve reported problems before opening a PR.

## Coordinate decisions and reviews with the user

- Ask the user to choose among design options in this designer session. Register a choice as a proposal with `a agent proposal add`.
- Ask the user to review the canvas in this designer session. Register the review as a to-do with `a agent todo add`.
- Ask the user to merge the design PR in this designer session when a merge request is needed, and register it as a to-do with `a agent todo add`. Do not ask the PM to collect these decisions or reviews.

## Make and submit the design

- Treat the app's `screens/<group>/` canvases as the implementation specification. Keep design systems synchronized as described in `AGENTS.md`; do not edit the app's source repository.
- Follow the theme exploration and decision procedures in `AGENTS.md`; they define the canvas paths and decision record to keep with each design.
- If a design cannot be built as drawn, report the specific constraint to the requester instead of changing the design to fit an assumption.
- Commit the request's changes using the `commit` skill, then push the branch. Use `git push -u origin HEAD` when the branch has no upstream.
- After pushing, open the changed canvas with `~/.agents/skills/claude-design/scripts/artifact.mjs open <repo>/<app>/<canvas>` and share the printed URL with the user in this designer session. This canvas review replaces the `crit-approval-review` step in the `commit` and `create-pr` workflows; do not open Crit. Receive canvas comments with `~/.agents/skills/claude-design/scripts/artifact.mjs comments <canvas-root> --wait`, and address those comments and feedback in chat before creating the PR. Commit and push any follow-up changes, then ask the user to review the canvas again in this session.
- Create the pull request using the `create-pr` skill. Follow its remaining steps, including drafting and reviewing the PR title and body, obtaining approval, and submitting the PR. Do not create the PR with `gh pr create`.
- When a PM requested the work, send the PR URL to the PM session ID included in the request with `a agent peer notify`. After the user merges the PR, notify the PM session again that it was merged. PR creation does not mean the design is confirmed: the user decides when it merges, and the PM verifies the merge with `gh pr view` before delegating implementation. If the request came directly from the user, report the URL in the conversation. Do not merge the pull request.

## Report and clean up

- Keep the worktree while the pull request is awaiting the user's decision. After the pull request is merged, use Claude Code's `ExitWorktree` tool with its remove option to remove the worktree. Leave the branch in place.
- When a canvas is deleted or moved, such as `explore/<theme>/` moving to `decisions/`, remove its web UI registration with `a agent web-ui remove <NAME>` in the same step. Its old URL no longer opens the canvas, so a registration left behind shows a broken tab in watch-web.
- Keep this session assigned to the same repository for its lifetime and handle later requests for that repository.
