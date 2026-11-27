# SectionHeading

A Markdown-style inline heading for a section inside a screen (`web/src/components/ui/section-heading.tsx`): the `##` or `###` mark in `primary`, then the lower-case label in mono.

- The consumer supplies `level` (2 or 3) and the label.
- Level 2 is 12px weight 500; level 3 is 14px weight 700. The mark is 12px weight 700.
- Use it for sections (subtasks, checklist), never for a screen title; screen titles sit in a `ScreenHeaderBar`.
