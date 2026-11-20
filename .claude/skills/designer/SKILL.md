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

Resolve `vibe_mode` for each accepted request with `~/.agents/skills/delegate/references/vibe-policy.md`, even when the session was started with `--vibe`. Follow that policy for an initial denial, a policy error, and any later fallback to the normal flow. Save the initial result for the submit and merge checks below. Recheck the policy immediately before submitting a PR and immediately before merging; use the automatic path only when the initial result and the latest result are both `true`.

## Coordinate decisions and reviews with the user

- Ask the user to choose among design options and review the canvas in this designer session. Register a choice as a proposal and canvas review as a to-do. In the normal flow, also ask the user to merge the PR here and register that request as a to-do. In `vibe_mode`, wait for the user's explicit canvas approval, then continue through PR creation and merge without another approval request. Do not ask the PM to collect these decisions or reviews.

## Make and submit the design

- Treat the app's `screens/` canvas as the implementation specification. Keep design systems synchronized as described in `AGENTS.md`; do not edit the app's source repository.
- Follow the theme exploration and decision procedures in `AGENTS.md`; they define the canvas paths and decision record to keep with each design.
- If a design cannot be built as drawn, report the specific constraint to the requester instead of changing the design to fit an assumption.
- Commit the request's changes using the `commit` skill, then push the branch. Use `git push -u origin HEAD` when the branch has no upstream.
- After pushing, open the changed canvas with `~/.agents/skills/claude-design/scripts/artifact.mjs open <repo>/<app>/<canvas>` and share the printed URL with the user in this designer session. This canvas review replaces the `crit-approval-review` step in the `commit` and `create-pr` workflows; do not open Crit. Receive canvas comments with `~/.agents/skills/claude-design/scripts/artifact.mjs comments <canvas-root> --wait`, and address those comments and feedback in chat before creating the PR. Commit and push any follow-up changes, then ask the user to review the canvas again in this session.
- In `vibe_mode`, after the user approves the canvas, remove the `before/` comparison and difference notes described in `AGENTS.md`, restore the canvas layout, and commit and push that cleanup before submitting the PR.
- Create the pull request using the `create-pr` skill. Do not create it with `gh pr create`. Always draft and review the PR title and body and complete the skill's machine and context-free review steps. For `vibe_mode`, the approved canvas is the user's approval to proceed: skip the create-pr flow's Crit review, editor approval, draft-ready notification, PR-ready notification, and waits for the PM's approval. Recheck `vibe_mode` immediately before submit; when it remains permitted, submit with `a ai pr-draft submit --no-review`. If it is no longer permitted, follow the normal create-pr review and approval flow, without `--no-review`.
- In the normal flow, before registering the merge to-do, remove the `before/` comparison and difference notes described in `AGENTS.md`, restore the canvas layout, and commit and push that cleanup. The user may merge as soon as the to-do appears.
- Confirm that CI has passed, that `gh pr view <PR> --json mergeable -q .mergeable` returns `MERGEABLE`, and address review comments with the `check-pr-review` skill. Treat `UNKNOWN` as unchecked: query again until it settles. `create-pr` may skip its review-comment step for this repository's owner, but bots can still review design PRs, and a merged base PR can leave this one conflicting. Resolve conflicts with the `sync-base-branch` skill. Repeat these checks after any later push to the PR.
- In the normal flow, register a merge to-do after these checks and let the user merge. In `vibe_mode`, recheck `vibe_mode` after all checks and immediately before merge. If it remains permitted, merge with `a gh pr-merge <PR>`; if permission has changed, follow the normal flow and register the merge to-do instead. Never use `gh pr merge` or the merge API directly. Do not notify the PM about PR creation or completion. A successful `a gh pr-merge` closes the head worktree and notifies the parent automatically; verify the worktree state and use `ExitWorktree` only if it still exists. In the normal flow, report the PR URL in this conversation when the request came directly from the user.

## Report and clean up

- Keep the worktree while a normal-flow pull request awaits the user's decision. After merge, check whether the worktree still exists; `a gh pr-merge` may already have closed it. If it remains, use Claude Code's `ExitWorktree` tool with its remove option. Leave the branch in place.
- When a canvas is deleted or moved, such as `explore/<theme>/` moving to `decisions/`, remove its web UI registration with `a agent web-ui remove <NAME>` in the same step. Its old URL no longer opens the canvas, so a registration left behind shows a broken tab in watch-web.
- Keep this session assigned to the same repository for its lifetime and handle later requests for that repository.
