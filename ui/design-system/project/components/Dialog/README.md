# Dialog

A centered modal from `@fohte/ui/dialog` (Base UI `Dialog`): a square `background` popup with a hairline ring over a dimmed, blurred page, with optional header, footer and close button.

Hand-written static rendition of `src/components/dialog.tsx` (`fui-dialog-overlay`, `fui-dialog`, `fui-dialog-header`, `fui-dialog-title`, `fui-dialog-description`, `fui-dialog-footer`, `fui-dialog-header-bar`).

- Parts: `Dialog`, `DialogTrigger`, `DialogPortal`, `DialogOverlay`, `DialogPopup` (unstyled), `DialogContent` (`showCloseButton`, default true), `DialogHeader`, `DialogHeaderBar`, `DialogTitle`, `DialogDescription`, `DialogFooter` (`showCloseButton`, default false), `DialogClose`.
- The consumer supplies title, description and actions; a title is required for an accessible name.
- Overlay: black at 40% with a 4px backdrop blur. Content: `background`, `text-sm`, 16px padding and gap, a 1px `foreground` 10% ring, `radius-xl` (0); 384px wide from 640px, `dialog-inset` (100% − 2rem) below.
- The close button is a ghost `icon-sm` X, 8px from the top right. The title is `text-base` 500 at line-height 1; the description `text-sm` `muted-foreground` with underlined links.
- Footer: bleeds to the popup edges on a `muted` 50% fill, actions stacked in reverse below 640px and right-aligned in a row above. Its top border has no color class, so it is drawn in `currentColor` (`foreground`), not `border`.
- `DialogHeaderBar` is a 56px row with a `border` bottom line and 24px sides, for popups the consumer pads itself.
