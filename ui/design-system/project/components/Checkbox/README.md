# Checkbox

A 16px square checkbox from `@fohte/ui/checkbox` (Base UI `Checkbox`) that fills with `foreground` when checked and shows a check or a minus.

Hand-written static rendition of `src/components/checkbox.tsx` (`fui-checkbox`, state via `data-checked`, `data-indeterminate`, `data-disabled`, `aria-invalid`).

- Props: Base UI `Checkbox.Root` props: `checked` / `defaultChecked`, `indeterminate`, `onCheckedChange`, `disabled`, `aria-invalid`, `aria-label`.
- The consumer supplies the visible label (wrap both in a `label`) or an `aria-label`.
- Unchecked: an `input` border, no fill. Checked and indeterminate: `foreground` border and fill, a 12px `background` mark.
- Focus-visible: `ring` border plus a 1px `ring` at 50%. Invalid: `destructive` border and a 1px ring at 20% (dark: border at 50%, ring at 40%). Disabled: 50% opacity.
- The `input` border is 1.21:1 (light) / 1.38:1 (dark) on `background`, under the 3:1 control-border floor; the source ships it that way.
