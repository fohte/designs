# Popover

A floating mono panel from `@fohte/ui/popover` (Base UI `Popover`) that opens 4px below its trigger, start-aligned.

Hand-written static rendition of `src/components/popover.tsx` (`fui-popover`, `fui-pad-none|sm|md`).

- Parts: `Popover` (`open`, `onOpenChange`, optional `anchor` ref: presses on the anchor do not close it), `PopoverTrigger` (usually `render={<Button variant="outline" />}`), `PopoverContent` (`padding` = `none` | `sm` | `md` default; `side` bottom, `sideOffset` 4, `align` start, `alignOffset` 0).
- The consumer supplies the content; it renders in a portal, at most the available width.
- Content: `popover` fill, 1px `border`, `radius-md` (0), `font-mono`, `shadow-md`.
- An outline trigger keeps its `muted` fill while open (`aria-expanded`).
