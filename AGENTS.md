# AGENTS.md

Run the skills' `artifact.mjs` from `.claude/skills/<skill>/scripts/` at the repository root. [README.md](README.md) has the install and open commands.

## Roles

- A Claude Code session started from this repository's root must first invoke the `designer` skill with the Skill tool and act as the resident designer for this repository.
- The design session edits the canvases and the design systems, then commits and pushes its changes. A human reviews a design PR on the changed canvas after the push: the designer opens the canvas editor, shares its URL, and addresses canvas comments or chat feedback before creating the PR. The PR title and body are in English. The user decides when it merges.
- The implementation session reads the app's `screens/` as the spec and changes the app in the app's repository. It does not edit this repository. Where the design cannot be built as drawn, it reports back to the design session instead of choosing another look.

## Layout

Each app's designs live in `<repo>/<app>/`: `<repo>` is the name of the app's repository without its owner, and `<app>` is the app's path in that repository, left out for an app at the repository's root. For example, an app at `apps/web/` in `fohte/example` goes in `example/apps/web/`.

Each canvas is a folder with `project/canvas.json`. An app's folder holds:

- `design-system/`: the app's design system. It belongs in `@fohte/ui` and lives here until it moves there.
- `screens/`: the canvas of the screens and parts the app should have. It differs from the app only between a design PR and the implementation PR that follows it.
- `explore/<theme>/`: one canvas per theme being decided, holding its options and `<theme>-current.dc.html`, a copy of the screen as it is now to compare against.
- `decisions/<YYYY-MM-DD>-<theme>/`: a decided theme. Its `README.md` records the options, the one chosen, and why; its `project/` is the theme's canvas, kept as it was when decided.

## Explore a theme

1. Create a canvas at `<repo>/<app>/explore/<theme>/` with the `claude-design` skill, installing the design system from the app's `design-system/`.
2. Run `artifact.mjs check <repo>/<app>/explore/<theme>` until it reports no problems.

## Decide a theme

In one design PR:

1. Apply the chosen option to `screens/`.
2. `git mv explore/<theme> decisions/<YYYY-MM-DD>-<theme>` and write its `README.md`.

## Keep the design system in step with the app

The design system is written by hand from the app's source. When the app's CSS changes a token or a built component, update `design-system/`, then copy it into `screens/` and each canvas under `explore/`:

```sh
node .claude/skills/claude-design/scripts/artifact.mjs ds-sync <repo>/<app>/<canvas>
```

Canvases under `decisions/` keep the copy they were decided with.

## Code organization rules

### Split files before they grow past ~500 lines of production code

When a change would push a file's non-test code past ~500 lines, split it along responsibility seams before adding more. Keep external import paths unchanged by keeping the entrypoint file in place and re-exporting the pieces you split out into new files. Tests move together with the code they verify.

Prefer creating a new focused file over appending to the largest existing one.
