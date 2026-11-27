# CommandPalette

The search-and-run overlay from `@fohte/ui/command-palette`: a `›`-prefixed ghost input over grouped `ListItem` results, full screen on phones and a 640px window from 768px.

Hand-written static rendition of `src/components/command-palette.tsx` (`fui-palette-overlay`, `fui-palette`, `fui-palette--md` for the `md:` layout, `fui-palette-head`, `fui-palette-key`, `fui-palette-foot`).

- Props: `open`, `onOpenChange`, `value`, `onValueChange`, `groups` (each `{ id, title }` with `items` or titled `sections`; each item has `key`, `select`, optional `selectOnTab`, and `render({ isSelected, onMouseMove })`), `loading`, `emptyMessage`, `initialMessage`, `prefix` (default `›`), `inputAdornment`, `mobileToolbar`, `body` (replaces the results), `footer`, `placeholder` (`Search...`), labels, `inputRef`, `onKeyDown`, `defaultSelectedIndex`.
- The consumer supplies every row through `render`, normally a `ListItem` with `highlighted={isSelected}`; the palette handles ↑↓, Tab, Enter and Esc.
- Overlay: black at 50%, the window 15vh from the top from `md`. Window: `popover` fill, `popover-foreground` text; from `md` a 1px border that has no color class, so it is drawn in `currentColor` (`popover-foreground`).
- Header: 48px, a `border` bottom line, the prefix in bold mono `primary`, an `Esc` key hint (from `md`) or a 36px ghost close button (below `md`). An optional mobile toolbar of chips sits below it on phones.
- Group titles are `text-2xs` mono, `tracking-widest`, `muted-foreground-faint`; groups after the first get a 1px `border` divider. Empty and initial messages are centered `text-xs` mono `muted-foreground-faint`.
- Footer (from `md`): key hints in `secondary` keycaps (`keycap-radius`, at least 44px) with `muted-foreground-ghost` words. The ghost words are 1.76:1 on dark `popover` and faint titles 2.38:1, as the source ships them.
- The loading spinner (lucide `Loader2`) rotates; static cards show it still.
