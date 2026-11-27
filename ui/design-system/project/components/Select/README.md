# Select

The dropdown from `@fohte/ui/select` (Base UI `Select`): a bordered or ghost trigger with a chevron, and a square `popover` menu whose chosen item carries a check.

Hand-written static rendition of `src/components/select.tsx` (`fui-select-trigger--default|ghost`, `fui-select-content`, `fui-select-item`, `fui-select-label`, `fui-select-separator`).

- Parts: `Select` (root), `SelectTrigger` (`size` = `default` 32px | `sm` 28px; `variant` = `default` | `ghost`; `iconClassName`), `SelectValue` (`placeholder`), `SelectContent` (`side`, `align`, `sideOffset` 4, `alignItemWithTrigger` true), `SelectGroup`, `SelectLabel`, `SelectItem`, `SelectSeparator`.
- The consumer supplies the items and an accessible name on the trigger.
- Trigger text is `text-sm`; the placeholder is `muted-foreground`. Default trigger states match the Input (dark adds an `input` 50% hover fill). Ghost trigger: ghost-field look, and its underline stays `border-strong` while the menu is open.
- Content: `popover` fill, `popover-foreground` text, a 1px `foreground` 10% ring plus `shadow-md`, at least 144px or the trigger's width. Groups pad 4px; labels are `text-xs` `muted-foreground`.
- Items: `text-sm`, 32px end padding for the 16px check; the keyboard or pointer highlight is `accent` / `accent-foreground`; disabled items are 50% opacity. Separators are a 1px `border` line.
- Scroll arrows (chevrons on a `popover` strip) appear only when the list overflows; not shown.
