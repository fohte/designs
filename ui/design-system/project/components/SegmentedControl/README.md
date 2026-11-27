# SegmentedControl

A single-choice row of pressed buttons from `@fohte/ui/segmented-control`: the selected segment lifts to `background` inside a `secondary` track.

Hand-written static rendition of `src/components/segmented-control.tsx` (`fui-segmented`, `fui-segment`).

- Props: `value`, `options` (`{ value, label }[]`), `onValueChange`, `disabled` (all segments); plus `div` props except `className`, `role`, `style`, `children`, `onChange`.
- The consumer supplies the options and an `aria-label` for the group.
- Segments are sans `text-xs` 500 with 4px × 10px padding inside a 2px track with a `border` line.
- Selected: `background` fill, `foreground` text, `aria-pressed="true"`. Others: `muted-foreground`, `foreground` on hover. Focus-visible: 3px `ring` at 50%. Disabled: 50% opacity.
