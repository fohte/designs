# Tabs

Underlined uppercase mono tabs from `@fohte/ui/tabs` (Base UI `Tabs`) on a 1px `border` rail.

Hand-written static rendition of `src/components/tabs.tsx` (`fui-tabs-list`, `fui-tab`, active via `data-active`).

- Parts: `Tabs` (`value` / `defaultValue`, `onValueChange`), `TabsList`, `TabsTab` (`value`), `TabsPanel` (`value`). None take `className`: the look is fixed.
- The consumer supplies tab labels and panel content; `TabsPanel` is unstyled.
- Tabs are `text-xs` mono, uppercase, `tracking-wider` (0.05em), 6px × 12px, 4px apart.
- Active: `foreground` text and a 2px `foreground` underline. Inactive: `muted-foreground`, `foreground` on hover. Focus-visible: 3px `ring` at 50%.
