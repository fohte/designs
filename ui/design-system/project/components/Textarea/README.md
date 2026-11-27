# Textarea

The multi-line field from `@fohte/ui/textarea`, styled like the default `Input` with a 64px minimum height and vertical resize.

Hand-written static rendition of `src/components/textarea.tsx` (`fui-textarea`).

- Props: every `textarea` prop (`rows`, `value`, `placeholder`, `disabled`, `aria-invalid`). No variants.
- The consumer supplies the label.
- Same states and colors as the default Input: `input` border, `ring` focus, `destructive` invalid, 50% opacity disabled, dark fills at 30% / 80%. Text is 16px below `md`, 14px from `md`.
