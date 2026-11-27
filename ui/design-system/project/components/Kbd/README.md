# Kbd

A keycap from `@fohte/ui/kbd` for shortcut hints, the one element with rounded corners (`keycap-radius` 4px).

Hand-written static rendition of `src/components/kbd.tsx` (`fui-kbd`).

- Props: any `kbd` prop. The consumer supplies the key text (`Esc`, `K`, `⌘`).
- `text-2xs` mono in `muted-foreground-strong` on a `muted` fill with a `border` line; at least 16px wide.
- Inside a `solid` Button it turns transparent-bordered with `background` text on a 10% `background` fill; inside a tooltip its radius becomes `radius-sm`.
