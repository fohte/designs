# StatusIcon

A task's status as a 20px circle (`web/src/components/task/status-icon.tsx`).

- The consumer supplies `status` and `statusReason`.
- `todo`: a 1.5px outline ring in `muted-foreground`.
- `completed`: a filled circle with a 12px lucide glyph in `background`. The reason picks fill and glyph: `completed` is `status-completed` with `Check`; `not_planned` is `muted-foreground-faint` with `X`; `duplicate` is `muted-foreground-faint` with `Equal`.
- A completed row's title gets `line-through` in `muted-foreground`, and the whole row is dimmed to 55% (`dim-completed`).
- `status-completed` is the only colored status; never swap it with `github-merged`, though they share a value.
