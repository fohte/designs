# Button

The square, mono-labelled action from `@fohte/ui/button` (Base UI `Button`): one emphasized gray `default` per view, bordered `outline` / `secondary` / `destructive` for the rest, borderless `ghost`, `link` and `plain` for the quietest actions.

Hand-written static rendition of `src/components/button.tsx` (classes `fui-button`, `fui-button--<variant>`, `fui-button--<size>`, `fui-button-plain`).

- Props: `variant` = `default` | `solid` | `outline` | `secondary` | `ghost` | `destructive` | `link` | `plain`; `size` = `default` | `xs` | `sm` | `lg` | `icon` | `icon-xs` | `icon-sm` | `icon-lg`; plus Base UI button props (`disabled`, `onClick`, `render`, `aria-*`).
- The consumer supplies the label or icon; an icon-only button needs `aria-label`. Mark an icon with `data-icon="inline-start"` or `"inline-end"` to trim the padding on that side.
- `default` is `border-strong` over `surface-strong` with a `foreground` border on hover, not red: `primary` stays punctuation. `solid` inverts to a `foreground` fill with bold text and recolors a `Kbd` inside it.
- `destructive` is quiet (`muted-foreground-strong` on a `border` line) until hover turns border and label `destructive`.
- `plain` has no box and no size geometry: it inherits the surrounding type, is `muted-foreground`, and turns `destructive` on hover. Use it for remove and inline edit actions.
- Heights: `xs` 24, `sm` 28, `default` 32, `lg` 36px; `icon*` are squares at the same steps. Icons are 16px (12px in `xs`, 14px in `sm`).
- States: focus-visible draws a `ring` border and a 3px `ring` at 50%; `aria-invalid` a 3px `destructive` ring at 40%; pressed shifts down 1px; disabled is 50% opacity with no pointer events. `aria-expanded` keeps the hover look on outline, secondary and ghost.
