# Input

The single-line text field from `@fohte/ui/input` (Base UI `Input`): a square `input`-bordered box by default, or a borderless `ghost` field that shows an underline on focus.

Hand-written static rendition of `src/components/input.tsx` and `ghostFieldClassName` in `src/utils.ts` (`fui-input fui-input--default`, `fui-input fui-ghost-field fui-input--ghost`).

- Props: `variant` = `default` | `ghost`; plus every `input` prop (`type`, `value`, `placeholder`, `disabled`, `aria-invalid`).
- The consumer supplies the label (visible or `aria-label`).
- 32px tall. Text is `text-base` (16px) below 768px so iOS does not zoom, `text-sm` from `md`.
- Default: `input` border, transparent fill (dark: `input` at 30%), placeholder `muted-foreground`. Focus-visible: `ring` border and a 1px ring at 50%. Invalid: `destructive` border, ring at 20% (dark: border 50%, ring 40%). Disabled: 50% opacity on an `input` fill at 50% (dark 80%).
- Ghost: no box; it bleeds 4px past its column (`-mx-1 px-1`, width +0.5rem), fills `accent` at 50% on hover, and draws a `border-strong` underline on focus (`destructive` when invalid). `CommandPalette` uses it.
