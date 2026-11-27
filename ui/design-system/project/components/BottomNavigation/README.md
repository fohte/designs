# BottomNavigation

The phone tab bar from `@fohte/ui/bottom-navigation`: one horizontal row of icon-over-label destinations and actions that scrolls sideways when it does not fit.

Hand-written static rendition of `src/components/bottom-navigation.tsx` (`fui-bottom-nav`, `fui-bottom-nav-item`).

- Props: `items` and an accessible name (`aria-label` or `aria-labelledby`); plus `nav` props. Each item has `id`, `label`, optional `icon`, `selected`, `className`, and is either `type: 'link'` with `renderLink` (the app's router link gets `children`, `className`, `aria-current`) or `type: 'button'` with `onClick` and optional `disabled`.
- The consumer supplies the icons (16px lucide strokes), the router link, and the placement: `fixed` / `sticky` positioning and the space under the bar are the app's job. The bar has no fill or top border of its own.
- Items are at least 52 × 52px, grow to share the width, 11px labels at line-height 1 on one line, icon and label 4px apart.
- Selected (`aria-current="page"` or `aria-pressed`): `accent` fill, `accent-foreground`. Others: `muted-foreground`, `foreground` on hover. Focus-visible: a 2px inset `ring`. Disabled actions: 50% opacity.
- Keyboard focus scrolls an off-screen item into view; a 4px trailing space lets the last item clear the edge.
