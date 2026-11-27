# List

Selectable rows from `@fohte/ui/list`: `List` with `ListItem`s rendered as pressable buttons (`role="list"`) or as listbox options (`role="listbox"`).

Hand-written static rendition of `src/components/list.tsx` and the `[data-slot='list-item']` rule in `tokens.css` (`fui-list`, `fui-list-item`).

- `List` props: `role` = `list` (default) | `listbox`, plus `div` props except `className` and `style`.
- `ListItem` props: `highlighted` (keyboard or pointer highlight), `selected` (adds a trailing 16px check; `aria-pressed` in a list, `aria-selected` in a listbox), `indent` (rem added to the 12px start padding), `onSelect`.
- The consumer supplies the row content; `CommandPalette` renders its results with it.
- Rows are at least 36px (44px on coarse pointers), `text-sm`, 8px gaps. Hover: `accent` at 50%. Highlighted: `accent` / `accent-foreground`. Focus-visible: a 2px `ring` outline.
