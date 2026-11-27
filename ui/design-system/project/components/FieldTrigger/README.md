# FieldTrigger

A borderless button from `@fohte/ui/field-trigger` that looks like the value of a field and opens an editor or menu; it inherits the surrounding type, so it works from a mono label up to a page title.

Hand-written static rendition of `src/components/field-trigger.tsx`, `fieldTriggerBaseClassName` and `ghostFieldClassName` (`fui-field-trigger-base fui-ghost-field fui-field-trigger`).

- Props: Base UI `Button` props except `type` (always `button`).
- The consumer supplies the value text and, optionally, a trailing icon (lucide `ChevronDown`), which is drawn in `muted-foreground` at 16px.
- At least 32px tall with 6px vertical padding; it bleeds 4px to each side like the ghost Input.
- Hover: `accent` at 50%. Focus: a `border-strong` underline drawn as an `::after` line, so the box does not grow. Invalid: `destructive` underline (dark: at 50%). Disabled: 50% opacity, no hover fill.
