# KeybindHint

A keyboard shortcut label in `text-2xs` mono (`web/src/components/ui/keybind-hint.tsx`).

- The consumer supplies the key text (`g t`, `⌘K`) and a `variant`.
- `plain` (default) is `muted-foreground-ghost`, for hints beside nav rows; `strong` and `muted` use those gray tiers.
- `boxed` draws a keycap: `border` over `secondary`, at least 44px wide, `keycap-radius` corners (one of the three radius exceptions).
