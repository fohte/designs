@fohte/ui is the shared look of fohte's apps: square corners, 1px hairlines, a gray scale that carries almost everything, mono type on controls and sans on what people read, and one red used only as punctuation. It ships a light theme by default and a dark theme under `.dark`; both are drawn from the same token names, so a component never names a theme.

## Content

- Fixed UI text is English, short and plain: `Save draft`, `Cancel`, `Close search`, `Search...`. Buttons and menu items are sentence or title case as written; tabs are written in any case and rendered uppercase by the tab itself.
- Group titles in the command palette are uppercase words (`PAGES`, `COMMANDS`); section titles under them are sentence case.
- User content (titles, notes, names) may be Japanese. Show it as written; the sans stack falls back to Hiragino and Meiryo for it.
- Shortcut keys sit in a `Kbd` (`Esc`, `Tab`, `⌘ K`). The command palette prefix is `›`; a scoped search may use another glyph such as `#`.
- No emoji. Icons are lucide-react strokes.

## Color

Two themes. **Light** is `:root` in `tokens.css` and the package default; **Dark** is the `.dark` class, which the consuming app applies (the package does not follow `prefers-color-scheme`). Every token below has a value in each.

- Grounds: the page on `background`; floating surfaces (popover, select menu, command palette) on `popover`; cards on `card`. In light, `card`, `popover`, `secondary` and `muted` are all `#f0f0f0`; in dark `#141414`.
- Text tiers, brightest first: `foreground` → `muted-foreground-strong` → `muted-foreground` → `muted-foreground-faint` → `muted-foreground-ghost`. Pick a tier by how much attention the text needs; do not add a gray. Pairs under 4.5:1 that the source ships, kept as they are: dark `muted-foreground` on `background` 4.10:1 and on `popover` 3.81:1; dark `muted-foreground-faint` 2.56:1; `muted-foreground-ghost` 2.46:1 (light) and 1.90:1 (dark). Use faint and ghost for labels and hints, never for the only copy of information.
- `primary` (`#dc2626` light, `#ef4444` dark) is punctuation: link buttons, the palette prefix, focus. It is never a large fill, and the default button is gray (`border-strong` over `surface-strong`). `destructive` and `ring` share its value. `primary-foreground` on dark `primary` is 3.61:1: large text only.
- The highlighted row (list, select item, selected nav item) is `accent` with `accent-foreground`; hover on rows and ghost fields is `accent` at 50%. Hover on outline and ghost buttons is `muted`.
- Lines: `border` for every hairline, `border-strong` to emphasize (default button, strong chip, ghost-field focus underline). `border` and `input` are 1.21:1 (light) and 1.38:1 (dark) on `background`: dividers, under the 3:1 control-border floor as the source ships them.
- `tint-*` pairs (red, orange, yellow, green, cyan, blue, magenta) are for app labels: the tint as background with its `-foreground` as text, 4.54:1 or better in both themes. The source writes the tints as `color-mix()`; here they are the computed hex (22% over `#fafafa` in light, 12% over `#0a0a0a` in dark).
- `sidebar-*` tokens are exposed for app sidebars; no library component uses them.

## Type

- `sans` (Helvetica Neue, Arial, then Hiragino / Meiryo) is the default for everything people read: list rows, select items, dialog text, inputs, tooltips, nav labels.
- `mono` (JetBrains Mono Variable, then IBM Plex Mono) for controls and chrome: buttons, chips, keycaps, tabs, popover content, palette rows and hints.
- `code` (IBM Plex Mono) is exposed for code in apps; no library component uses it.
- Sizes are Tailwind's (`text-xs` 12/16, `text-sm` 14/20, `text-base` 16/24) plus the library's own `text-2xs` (10/14) for chips, keycaps and palette chrome, and an 11px nav label. Do not add another step.
- Inputs and textareas are 16px below 768px (no iOS zoom) and 14px from `md`.
- Weights: 400 for text, 500 for buttons, segments and the dialog title, 700 for the solid button and the palette prefix.

## Space and layout

- Tailwind's 4px step (`--spacing: 0.25rem`), half steps included: `space-0.5` 2px … `space-8` 32px. No invented steps such as 7px or 18px.
- Control heights: `control-xs` 24, `control-sm` 28, `control` 32, `control-lg` 36px. List rows are at least 36px, 44px on coarse pointers; bottom-nav items 52 × 52px.
- Breakpoints the components read: `sm` 640px (dialog width and footer row) and `md` 768px (input text size, command palette window).
- Floating surfaces open 4px from their trigger. The command palette window is 640px wide and at most 480px tall from `md`, full screen below. Dialogs are 384px wide from `sm`, `100% − 2rem` below.
- Placement of the bottom navigation (`fixed` / `sticky`, the space under it) belongs to the app.

## Shape and depth

- Every corner is square: `radius` is 0 in both themes, so every `radius-*` step and `btn-radius-*` computes to 0. The one exception is `keycap-radius` (4px) on `Kbd` and the palette key hints. A round shape (a color dot) is the consumer's.
- Borders are 1px. The tab underline is the only 2px line.
- Depth is rare: `shadow-md` on popovers and select menus; a 1px `ring-hairline` (`foreground` at 10%) on dialogs and select menus; overlays dim the page with black at 40% (dialog, with a 4px blur) or 50% (palette).

## States

- Hover: `muted` on outline and ghost buttons; a `foreground` border on the default button; `border-strong` on secondary; `destructive` border and text on destructive; `destructive` text on plain; `accent` at 50% on rows and ghost fields; `foreground` text on inactive tabs, segments and nav items.
- Focus-visible: buttons, tabs and segments draw `focus-ring` (3px `ring` at 50%), plus a `ring` border on buttons; fields and checkboxes draw a `ring` border with `focus-ring-field` (1px); ghost fields switch to a `border-strong` underline; list rows a 2px `ring` outline; nav items a 2px inset `ring`.
- Invalid (`aria-invalid`): `destructive` border and a faint `destructive` ring (20% light, 40% dark, border at 50% in dark); ghost fields get a `destructive` underline.
- Selected: `foreground` underline (tabs), `background` lift (segments), `accent` fill (nav items, highlighted rows), a trailing check (list and select items), a `foreground` fill (checkbox).
- Disabled: 50% opacity (`opacity-disabled`), no pointer events.
- Pressed buttons move down 1px.

## Iconography

- lucide-react stroke icons in `currentColor`, 16px by default (`size-4`), 14px in `sm` buttons, 12px in `xs` buttons, chips and checkbox marks. Field and select chevrons are `muted-foreground`.
- There is no logo file. The package name is the plain words `@fohte/ui`.

## Using the cards

The component cards are static renditions: plain HTML styled by `components/bundle.css` with `fui-` classes that mirror each component's Tailwind classes. Hover, focus and open states that need interaction are shown with the `is-hover` and `is-focus` modifiers; open, selected and invalid states use the component's own `data-*` / `aria-*` attributes (`aria-expanded`, `data-popup-open`, `data-active`, `aria-invalid`). Dark-only rules apply under `[data-theme="dark"]` or `.dark`. The command palette's `md:` layout is the `fui-palette--md` modifier so both layouts fit one card.

On a Design canvas, load `tokens.css` first and then `components/bundle.css`: `bundle.css` reads colors, fonts, radii, shadows and layout sizes from the variables in `tokens.css`.

## Not synced

Source: fohte/ui `origin/main@2d45bab`, package `@fohte/ui` 0.1.8 (`tokens.css`, `package.json` exports, `src/components/*.tsx` and their stories; `src/index.ts` exports no component, the subpath exports in `package.json` are the inventory).

- Route: read-only. Every card is a hand-written static rendition; no `components/bundle.js` was built, because the package publishes TSX source that needs Tailwind v4, `tw-animate-css` and `shadcn/tailwind.css` compiled in the consuming app, and running the repository's build was not part of this sync.
- Not rendered: motion (dialog, tooltip and select fade / zoom / slide, the loading spinner's rotation, button transitions), Base UI positioning (collision flipping, `alignItemWithTrigger`, `--available-width`), portals, focus trapping and keyboard handling (palette ↑↓ / Tab / Enter / Esc, bottom-nav scroll-into-view), the select scroll arrows, and coarse-pointer sizing except through a media query.
- Values computed instead of copied: `tint-*` backgrounds (from `color-mix()`), every `radius-*` and `btn-radius-*` step (from `calc()` / `min()` over `--radius: 0rem`), `select-content-min-width` (`max(anchor, spacing × 36)`). The spacing, size, shadow and type steps are Tailwind defaults the classes use; `tokens.css` declares only colors, fonts, `text-2xs`, radii and the four layout variables.
- Kept from the source though unusual: the `DialogFooter` top border and the `md` command-palette border have no color class, so Tailwind's preflight draws them in `currentColor`.
- Fonts are not bundled by the package and not copied here. `bundle.css` loads IBM Plex Mono from Google Fonts; JetBrains Mono Variable is not available under that family name there, so previews show the mono stack's IBM Plex Mono fallback unless it is installed locally. The sans stack is system fonts.
