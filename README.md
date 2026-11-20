# designs

@fohte's personal design workspace for Claude Design canvases and shared design systems, edited with the [baoyu-design](https://github.com/JimLiu/baoyu-design) skills. [AGENTS.md](AGENTS.md) describes the layout, who edits what, and how a design goes from options to a decision.

## Install the design skills

The upstream canvas and design-system skills are not committed, because their upstream NOTICE grants no license for the parts adapted from Anthropic's material. Install them into the user-level agent skill directory from the repository root:

```sh
DO_NOT_TRACK=1 npx skills@1.7.6 add JimLiu/baoyu-design --skill claude-design-system claude-design --agent codex --global -y
```

This installs the skills under `~/.agents/skills/`. Run their `artifact.mjs` commands directly from there, outside Claude Code's sandbox. Project-local copies are not required.

## Start a designer session

Run one session per app repository, passing the assigned GitHub repository as `<owner>/<repo>`:

```sh
claude "/designer <owner>/<repo>"
```

If the repository is omitted, the designer asks which repository it owns. It sets the session title to `designer <owner>/<repo>`, which PMs use with the `designer` work type to find the right session. See [AGENTS.md](AGENTS.md) for the request, handoff, and implementation workflow.

## Open a design

Run these commands outside Claude Code's sandbox. Each command starts a local editor and prints its URL:

```sh
# A design system
~/.agents/skills/claude-design-system/scripts/artifact.mjs open <repo>/<app>/design-system
# A canvas: screens, explore/<theme> or decisions/<YYYY-MM-DD>-<theme>
~/.agents/skills/claude-design/scripts/artifact.mjs open <repo>/<app>/<canvas>
```

Design changes are committed and pushed before the designer shares the changed canvas editor URL for human review. The designer receives canvas comments with `~/.agents/skills/claude-design/scripts/artifact.mjs comments <canvas-root> --wait`; chat feedback is handled in the conversation. The designer addresses feedback before creating the PR, then commits and pushes follow-up changes and requests canvas review again if feedback changes the design. PRs follow the standard drafting, review, approval, and submission process in the normal flow. In `vibe_mode`, canvas approval authorizes submission and merge after CI and review checks pass. In the normal flow, the user merges and the design is confirmed only after merge. The designer does not send separate PR-created or completion notifications to the PM; merge-time worktree cleanup notifies the parent automatically.
