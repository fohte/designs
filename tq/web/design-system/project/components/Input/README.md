# Input

The single-line text field from `@fohte/ui/input`: 32px tall, square, one `input` border over a 30% `input` fill.

- The consumer supplies `value`, `placeholder`, `aria-label` or a `<label>`, and `aria-invalid` on error.
- Text is 16px on phones (so iOS Safari does not zoom) and 14px from `md`.
- Focus turns the border `ring` with a 1px ring at 50%; an invalid field gets a `destructive` border at 50%.
- The `ghost` variant drops the border for inline-editable fields such as titles.
