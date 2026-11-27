# Chip

A small bordered mono label from `@fohte/ui/chip` for tags, scopes and filter toggles, optionally removable or rendered as a button.

Hand-written static rendition of `src/components/chip.tsx` (`fui-chip`, `fui-chip--md`, `fui-chip--strong`, `fui-chip--faint`).

- Props: `size` = `sm` (default, 4px sides) | `md` (2px × 6px); `tone` = `muted` (default) | `strong` | `faint`; `as` = `span` (default) | `button`; on a span, `onRemove` with a required `removeLabel` adds a `plain` remove button.
- The consumer supplies the children (text, or a dot and text). A `button` chip takes `aria-pressed` for toggles.
- All chips are `text-2xs` mono with a 1px line: `muted` is `muted-foreground` on `border`, `strong` is `foreground` on `border-strong`, `faint` is `muted-foreground-faint` on `border`.
- The remove button is a 12px X that turns `destructive` on hover; its click does not bubble to the chip.
- `faint` text is 2.56:1 on the dark `background`: use it for de-emphasized labels, never for the only copy of information.
