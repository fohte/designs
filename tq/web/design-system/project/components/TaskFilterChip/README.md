# TaskFilterChip

One `key:value` condition in the task list's filter row (`web/src/components/task/task-filter-chip.tsx`).

- The consumer supplies a lucide icon, the attribute name, the value, the menu it opens and an optional `onRemove`.
- The icon (14px) and `key:` are `muted-foreground`; the value sits on `tint-blue` in `tint-blue-foreground` with `radius-task-filter-value` corners. Blue is reserved for these values.
- The qualifier opens the condition's filter menu; the separate 16px `X` button clears just this condition.
- A condition still at its default value renders at 50% opacity.
