# SegmentedControl

One value from a small fixed set, from `@fohte/ui/segmented-control`: a `secondary` track with a `border`, the selected option on `background` in `foreground`.

- The consumer supplies `value`, `options` (`{value, label}`) and `onValueChange`.
- Each option is a button with `aria-pressed`; the group has `role="group"`.
- Labels are 12px sans, weight 500; unselected options are `muted-foreground`.
