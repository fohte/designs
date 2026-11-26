# ScreenHeaderBar

The top row of every screen and panel (`web/src/components/ui/screen-header-bar.tsx`): 40px tall, 12px side padding, a `border` hairline below, on `background`.

- The consumer supplies the children: a mono title or `SectionHeading`, then trailing actions pushed right with `margin-left: auto`.
- Items are 10px apart; `spacing="compact"` tightens them to 6px below `sm` for narrow queue headers.
- The nav rail's header row is also 40px, so their bottom borders line up across the shell.
