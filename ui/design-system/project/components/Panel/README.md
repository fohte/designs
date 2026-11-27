# Panel

A plain 1px `border` box from `@fohte/ui/panel` for grouping content, with three padding steps and no fill or shadow.

Hand-written static rendition of `src/components/panel.tsx` and `src/padding.ts` (`fui-panel`, `fui-pad-none|sm|md`).

- Props: `padding` = `none` (0) | `sm` (6px × 12px) | `md` (12px, default); plus any `div` prop.
- The consumer supplies the content and any background; the panel inherits the surface it sits on.
