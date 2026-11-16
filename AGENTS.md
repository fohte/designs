# AGENTS.md

Run canvas `artifact.mjs` scripts directly from `~/.agents/skills/<skill>/scripts/`, without `node` and outside Claude Code's sandbox. [README.md](README.md) has the installation and open commands.

## Roles

- A Claude Code session started from this repository's root must first invoke the `designer` skill with the Skill tool and act as the designer for one app repository. This also applies when starting with plain `claude`; if `/designer <owner>/<repo>` is omitted, the skill asks the user which repository it owns.
- The designer handles one assigned repository per session. It sets the session title to `designer <owner>/<repo>`; loading this skill sets its `work_type` to `designer`.
- The designer accepts requests only for its assigned repository. For a request targeting another repository, it declines and directs the requester to the matching designer or the launch command `cd ~/ghq/github.com/fohte/designs && claude "/designer <owner>/<repo>"`.
- The designer edits the canvases and design systems, then commits with the `commit` skill and pushes its changes. After pushing, a human reviews the changed canvas: the designer opens the canvas editor, shares its URL, and addresses canvas comments or chat feedback before creating the PR. This canvas review replaces the `crit-approval-review` step in the `commit` and `create-pr` workflows; do not open Crit. The designer creates the PR with the `create-pr` skill and follows its remaining drafting, review, approval, and submission steps, then sends the PR URL to the requester with `a agent peer notify`.
- A design is confirmed only after its PR is merged. The user decides when it merges; the designer does not merge the PR.

## Layout

Each app's designs live in `<repo>/<app>/`: `<repo>` is the name of the app's repository without its owner, and `<app>` is the app's path in that repository, left out for an app at the repository's root. For example, an app at `apps/web/` in `fohte/example` goes in `example/apps/web/`.

Each canvas is a folder with `project/canvas.json`. An app's folder holds:

- `design-system/`: the app's design system. It belongs in `@fohte/ui` and lives here until it moves there.
- `screens/<group>/`: one canvas per group of related screens the app should have, such as one page of the app and its dialogs, so that each canvas stays small enough to read. A screen's mobile artboards sit beside its desktop artboard in the same canvas. Together they differ from the app only between a design PR and the implementation PR that follows it. A part that screens in several groups `<dc-import>` is copied into each of those canvases, because the editor looks for a part only beside the artboard that imports it; change every copy in the same PR.
- `explore/<theme>/`: one canvas per theme being decided, holding its options and `<theme>-current.dc.html`, a copy of the screen as it is now to compare against.
- `decisions/<YYYY-MM-DD>-<theme>/`: a decided theme. Its `README.md` records the options, the one chosen, and why; its `project/` is the theme's canvas, kept as it was when decided.

## Explore a theme

1. Create a canvas at `<repo>/<app>/explore/<theme>/` with the `claude-design` skill, installing the design system from the app's `design-system/`.
2. Run `artifact.mjs check <repo>/<app>/explore/<theme>` until it reports no problems.

## Decide a theme

In one design PR:

1. Apply the chosen option to the `screens/<group>/` canvases it changes.
2. `git mv explore/<theme> decisions/<YYYY-MM-DD>-<theme>` and write its `README.md`.

## Show a design PR's changes to `screens/`

The reviewer cannot tell from the canvas alone what a design PR changed, so put the changes on the canvas before asking for review:

1. Copy from the base branch into `screens/<group>/project/before/` each artboard whose look changed, including one whose own file is unchanged but which `<dc-import>`s a changed part, directly or through other parts. Prefix its name with `Before` so stems stay unique. Copy every part it imports, directly or through other parts, into the same folder: the editor looks for a part only beside the artboard that imports it.
2. On the canvas, place each old artboard beside its new one, with a sticky note listing the differences.
3. Before the PR merges, delete `before/` and the notes, and restore the layout.

## Keep the design system in step with the app

The design system is written by hand from the app's source. When the app's CSS changes a token or a built component, update `design-system/`, then copy it into each canvas under `screens/` and `explore/`:

```sh
~/.agents/skills/claude-design/scripts/artifact.mjs ds-sync <repo>/<app>/<canvas>
```

Canvases under `decisions/` keep the copy they were decided with.

## Code organization rules

### Split files before they grow past ~500 lines of production code

When a change would push a file's non-test code past ~500 lines, split it along responsibility seams before adding more. Keep external import paths unchanged by keeping the entrypoint file in place and re-exporting the pieces you split out into new files. Tests move together with the code they verify.

Prefer creating a new focused file over appending to the largest existing one.
