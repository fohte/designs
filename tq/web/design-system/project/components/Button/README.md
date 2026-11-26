# Button

The square mono-labelled button from `@fohte/ui/button`: one emphasized gray `default` per screen, bordered `outline`/`secondary` for the rest, and borderless `ghost`/`plain` for low-emphasis actions.

- The consumer supplies the label or icon, `variant`, `size`, `disabled` and `onClick`; icon-only buttons need an `aria-label`.
- `default` is `border-strong` over `surface-strong`, not red: red stays punctuation (`primary`).
- `destructive` is quiet until hover, when its border and label turn `destructive`.
- `plain` has no geometry and inherits the surrounding typography; its hover turns red, so keep it for remove actions.
- Sizes: `xs` 24px, `sm` 28px, `default` 32px, `lg` 36px tall; `icon*` are square at the same heights.
- Disabled buttons drop to 50% opacity.
