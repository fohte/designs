# designs

@fohte's personal design workspace for Claude Design canvases and shared design systems, edited with the [baoyu-design](https://github.com/JimLiu/baoyu-design) skills. [AGENTS.md](AGENTS.md) describes the layout, who edits what, and how a design goes from options to a decision.

## Install the design skills

The upstream canvas and design-system skills are not committed, because their upstream NOTICE grants no license for the parts adapted from Anthropic's material. Install them into this repository from its root:

```sh
DO_NOT_TRACK=1 npx skills@1.7.6 add JimLiu/baoyu-design --skill claude-design-system claude-design --agent claude-code -y
```

`skills-lock.json` records the installed versions, and this command rewrites it.

## Start a designer session

The repository includes a project skill for the resident designer. Start Claude Code from the repository root:

```sh
claude
```

`AGENTS.md` instructs the session to start as the resident designer.

## Open a design

Run these from the repository root. Each command starts a local editor and prints its URL:

```sh
# A design system
node .claude/skills/claude-design-system/scripts/artifact.mjs open <repo>/<app>/design-system
# A canvas: screens, explore/<theme> or decisions/<YYYY-MM-DD>-<theme>
node .claude/skills/claude-design/scripts/artifact.mjs open <repo>/<app>/<canvas>
```

Design PRs are reviewed on the changed canvas after changes are pushed. The designer shares the editor URL and receives canvas comments with `node .claude/skills/claude-design/scripts/artifact.mjs comments <canvas-root> --wait`; chat feedback is handled in the conversation before the designer creates the PR. PR titles and bodies are in English, and the user decides when the PR merges.
