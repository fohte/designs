# ButtonGroup

A `role="group"` row from `@fohte/ui/button-group` that joins adjacent `Button`s into one bar by dropping every left border but the first.

Hand-written static rendition of `src/components/button-group.tsx` (`fui-button-group`).

- Props: any `div` prop except `role`. Give it an `aria-label` that names the set.
- The consumer supplies the `Button` children; use one variant across the group (the stories use `outline`).
- A focused button rises (`z-index` 10) so its ring is not clipped by its neighbour.
- `xs` / `sm` buttons inside a group use `radius-lg` instead of their own radius (all 0 in this library).
