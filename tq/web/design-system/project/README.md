tq builds on `ui/design-system` (@fohte/ui): its palette, gray tiers, tints, fonts, type scale, spacing, radius scale and components (Button, Chip, Input, SegmentedControl, Panel, Kbd, Dialog, …) are @fohte/ui's and are documented there. This system adds only what tq defines itself: a few tokens and tq's own components. A canvas for tq installs both systems.

tq is a personal task manager drawn as a near-monochrome dark terminal: square corners, 1px hairlines, mono UI chrome around sans reading text, and red used only as punctuation.

## Content

- Fixed UI text is English and short. Chrome labels are lower case (`tasks`, `subtasks`, `today`); buttons are title or sentence case as the app writes them (`Add Task`, `Delete`).
- Task titles, descriptions, comments, project and label names come from the user and are often Japanese. Show them as written; never translate or re-case them.
- Section headings read like Markdown: `## subtasks`, `### checklist`. Field labels in sidebars are `text-2xs` mono in a dim gray tier (`PRIORITY`, `PROJECT`).
- Task numbers are `#` plus the number (`#128`) in mono. Separate metadata with `·`.

## Color

- Dark only: the app always renders with `class="dark"`, so use @fohte/ui's dark values. Screens sit on `background`; modals and cards on `card`; menus on `popover`; hover and the keyboard-highlighted row on `accent`.
- @fohte/ui's `tint-blue` pair is reserved in tq for task-filter values; the other `tint-*` pairs color user labels.
- `status-completed` (magenta) marks a task closed as done; `github-open`, `github-closed`, `github-merged` mark GitHub state. They alias @fohte/ui tints and share values but never stand in for each other.
- `scrim` dims the page behind a bottom sheet or modal.

## Type

- `code` (IBM Plex Mono) only for plain textareas and code in the markdown editor.
- Task and project titles on detail screens are `title` (`text-2xl` bold), `title-sm` on phones. Prose uses `prose` (`leading-relaxed`, 1.625).

## Layout

- The shell: a 200px nav rail (`width-nav`) on the left from `md` (768px), and a bottom tab bar below it. Every screen and panel starts with a 40px `ScreenHeaderBar` (`size-header`).
- Detail screens put a 240px `DetailSidebarPanel` (`width-detail-sidebar`, 16px padding, `border` on its left) to the right of a body capped at `width-reading` (768px).
- Desktop forms open in a 600px `ModalPanel` (`width-modal`) on `card`; on phones the same forms open as bottom sheets over `scrim`, capped at 85% of the visual viewport.
- Tap targets are at least 44px.

## Shape and depth

- tq's radius exceptions to @fohte/ui's square corners: `radius-task-filter-value` (filter values), `radius-inline-code` (markdown inline code) and `radius-round` (`StatusIcon` circles). The boxed `KeybindHint` uses @fohte/ui's `keycap-radius`.
- The desktop modal is the only shadow tq adds: `shadow-modal` with a 1px `foreground` ring at 10%.

## States

- Completed rows dim to 55% opacity, with `line-through` titles in `muted-foreground`.
- A filter condition at its default value: 50% opacity.

## Not synced

Source: fohte/tq `origin/main@958790f6` (`web/src/index.css`, `web/src/components/ui/markdown-editor.css`, the component files in `tokens.json` `meta`). `index.css` declares `scrim`, the `status-completed` / `github-*` aliases and `radius-task-filter-value`; the aliases point at @fohte/ui tints and are written here as their dark hex. The layout sizes, `radius-round` and `shadow-modal` are the Tailwind values tq's components use. Not copied: viewport-relative sizes (`max-height-sheet` and the composer caps), `z-index-max`, grid tracks and popup widths.

Components are static renditions hand-written from the source (read-only route): KeybindHint, SectionHeading, ScreenHeaderBar, StatusIcon, PriorityBadge, TaskFilterChip and ProgressBar. Where a card shows an @fohte/ui part (the action in ScreenHeaderBar, the remove button in TaskFilterChip), it draws a minimal stand-in; on a canvas use ui/design-system's components. `components/bundle.css` gives the @fohte/ui dark values the cards read a zero-specificity fallback so they render in this editor alone; ui/design-system's `tokens.css` overrides them wherever both load. Not built: tq's bottom sheet, modal frame, dropdown and actions menus, markdown editor and calendar.
