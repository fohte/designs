# designs

@fohte's personal design workspace for Claude Design canvases and shared design systems, edited with the [baoyu-design](https://github.com/JimLiu/baoyu-design) skills. [AGENTS.md](AGENTS.md) describes the layout, who edits what, and how a design goes from options to a decision.

## Install the design skills

The upstream canvas and design-system skills are not committed, because their upstream NOTICE grants no license for the parts adapted from Anthropic's material. Install them into the user-level agent skill directory from the repository root:

```sh
DO_NOT_TRACK=1 npx skills@1.7.6 add JimLiu/baoyu-design --skill claude-design-system claude-design --agent codex --global -y
```

This installs the skills under `~/.agents/skills/`. Run their `artifact.mjs` commands directly from there, outside Claude Code's sandbox. Project-local copies are not required.

## Start a designer session

The repository includes a project skill for the resident designer. Start Claude Code from the repository root:

```sh
claude
```

`AGENTS.md` instructs the session to start as the resident designer.

## Open a design

Run these commands outside Claude Code's sandbox. Each command starts a local editor and prints its URL:

```sh
# A design system
~/.agents/skills/claude-design-system/scripts/artifact.mjs open <repo>/<app>/design-system
# A canvas: screens, explore/<theme> or decisions/<YYYY-MM-DD>-<theme>
~/.agents/skills/claude-design/scripts/artifact.mjs open <repo>/<app>/<canvas>
```

Design PRs are reviewed on the changed canvas after changes are pushed. The designer shares the editor URL and receives canvas comments with `~/.agents/skills/claude-design/scripts/artifact.mjs comments <canvas-root> --wait`; chat feedback is handled in the conversation. The designer addresses feedback before creating the PR, then commits and pushes follow-up changes and requests canvas review again if feedback changes the design. PR titles and bodies are in English, and the user decides when the PR merges.
