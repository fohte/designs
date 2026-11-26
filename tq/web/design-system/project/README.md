tq is a personal task manager drawn as a near-monochrome dark terminal: square corners, 1px hairlines, mono UI chrome around sans reading text, and red used only as punctuation. It follows the fohte.net look through the shared `@fohte/ui` tokens.

## Content

- Fixed UI text is English and short. Chrome labels are lower case (`tasks`, `subtasks`, `today`); buttons are title or sentence case as the app writes them (`Add Task`, `Delete`).
- Task titles, descriptions, comments, project and label names come from the user and are often Japanese. Show them as written; never translate or re-case them.
- Section headings read like Markdown: `## subtasks`, `### checklist`. Field labels in sidebars are `text-2xs` mono in a dim gray tier (`PRIORITY`, `PROJECT`).
- Task numbers are `#` plus the number (`#128`) in mono. Separate metadata with `·`.
- No emoji. Icons are lucide-react strokes.

## Color

- Dark only: the app always renders with `class="dark"`. Screens sit on `background`; modals and cards on `card`; menus on `popover`; hover and the keyboard-highlighted row on `accent`.
- Text picks a gray tier by how much attention it needs, brightest first: `foreground` → `muted-foreground-strong` → `muted-foreground` → `muted-foreground-faint` → `muted-foreground-ghost`. Never add another gray. `muted-foreground-faint` and `muted-foreground-ghost` fall under 4.5:1 on `background` (2.6:1, 1.9:1) and are kept for labels, tree lines and hints, as the source ships them.
- `primary` red is punctuation: the active nav marker, links, the `##` of a heading, focus borders. It is never a large fill, and the default button is gray (`border-strong` over `surface-strong`), not red. `destructive` shares the hue.
- Blue (`tint-blue`, `tint-blue-foreground`) is reserved for task-filter values.
- `status-completed` (magenta) marks a task closed as done; `github-open`, `github-closed`, `github-merged` mark GitHub state. They share tint values but never stand in for each other.
- The other `tint-*` pairs color user labels: the tinted background with its `-foreground` text.

## Type

- `sans` (Helvetica Neue, then Hiragino for Japanese) for everything people read: titles, rows, descriptions, comments.
- `mono` (JetBrains Mono) for all chrome: nav labels, tabs, headings, chips, buttons, keybind hints, counters, task numbers.
- `code` (IBM Plex Mono) only for plain textareas and code in the markdown editor.
- Sizes are Tailwind's scale (`text-xs` 12, `text-sm` 14, `text-base` 16, `text-xl` 20, `text-2xl` 24) plus one custom tier, `text-2xs` (10px / 14px), for the smallest chrome. Do not add another.
- Prose uses `leading-relaxed` (1.625). Task and project titles on detail screens are `text-2xl` bold.

## Space and layout

- Tailwind's 4px grid, half steps included (`space-0.5` 2px … `space-3.5` 14px). No invented steps such as 7px or 18px.
- The shell: a 200px nav rail (`width-nav`) on the left from `md` (768px), and a bottom tab bar below it. Every screen and panel starts with a 40px `ScreenHeaderBar`.
- Detail screens put a 240px `DetailSidebarPanel` (`width-detail-sidebar`, 16px padding, `border` on its left) to the right of a body capped at `width-reading` (768px).
- Desktop forms open in a 600px `ModalPanel` (`width-modal`) on `card`; on phones the same forms open as bottom sheets over `scrim`, capped at 85% of the visual viewport.
- Tap targets are at least 44px (`size-tap`).

## Shape and depth

- Every corner is square (`radius` 0). Three exceptions only: `keycap-radius` (boxed keybind hint), `radius-task-filter-value` (filter values) and `radius-inline-code`. `StatusIcon` circles are round.
- Borders are 1px `border`; `border-strong` marks the active tab, the default button and strong chips.
- No shadows except the desktop modal (`shadow-modal` with a 1px `foreground` ring at 10%).

## States

- Hover and keyboard highlight: `accent` fill on menu items and rows; `muted` on outline and ghost buttons.
- Focus: `ring` red, at 50% alpha.
- Completed rows dim to 55% opacity, with `line-through` titles in `muted-foreground`.
- Disabled: 50% opacity. A filter condition at its default value: 50% opacity.

## Iconography

- lucide-react stroke icons in `currentColor`, usually 16px (`size-4`), 14px in filter chips, 12px inside chips and status glyphs.
- There is no logo file. The product name is the plain word `tq`.

## Not synced

The source declares no spacing, size or shadow tokens; those families list the Tailwind values the components use. `tint-*` backgrounds are `color-mix()` in the source and are written here as their computed hex (12% of the foreground over `background`). Fonts are not copied: `components/bundle.css` loads JetBrains Mono and IBM Plex Mono from Google Fonts, and the sans stack is system fonts. The light palette in `@fohte/ui/tokens.css` is unused by tq and left out. Components are static renditions hand-written from the source (read-only route): Button, Chip, Input, SegmentedControl, KeybindHint, SectionHeading, ScreenHeaderBar, StatusIcon, PriorityBadge, TaskFilterChip, ProgressBar and Panel. Not built: Dialog, Select, Popover, Tooltip, BottomNavigation, CommandPalette, Tabs, and tq's bottom sheet, modal frame, dropdown and actions menus, markdown editor and calendar.
