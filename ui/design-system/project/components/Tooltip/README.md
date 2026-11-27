# Tooltip

A small inverted label from `@fohte/ui/tooltip` (Base UI `Tooltip`): `background` text on a `foreground` fill with a square arrow, above its trigger by default.

Hand-written static rendition of `src/components/tooltip.tsx` (`fui-tooltip`, `fui-tooltip-arrow`).

- Parts: `TooltipProvider` (`delay` 0 by default), `Tooltip`, `TooltipTrigger`, `TooltipContent` (`side` top, `sideOffset` 4, `align` center).
- The consumer supplies the text and, optionally, a `Kbd`; with a Kbd the end padding drops to 6px.
- `text-xs`, 6px × 12px, at most 320px wide, square corners. The arrow is a 10px square rotated 45° in `foreground`, shifted by `tooltip-arrow-offset`.
- It fades and zooms in from 95% and slides 8px from its side; static cards show the open state only.
