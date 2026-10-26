# Red-eye Fixer

A single-page tool for removing red eye from photos, including film scans. Open it at
https://leethree.github.io/redeye-fixer/, or download `index.html` and open it in a browser.

Your photo stays on your device. Everything runs in the browser and nothing is uploaded.

## How to use

1. Open a photo, or drag it onto the page.
2. Click or tap each red eye. The mark snaps to the reddest point nearby.
3. Select a mark to adjust it:
   - **Size**: the radius of the area that is corrected.
   - **Red threshold**: lower it to catch fainter red, raise it if skin around the eye changes.
   - **Compare with skin / iris**: use "iris" when the skin is as warm as the red glow, so
     the pupil is compared with the eye's own iris instead.
4. Hold **Space** or the **Hold to compare** button to see the original.
5. **Save** downloads `<name>_fixed.jpg`.

Mouse: drag a mark to move it, drag elsewhere to pan, scroll to zoom, right-click or Delete
to remove a mark, `[` and `]` to resize, Ctrl/Cmd+Z to undo.
Touch: tap to mark, drag to pan or move a mark, pinch to zoom.

## How the correction works

Inside each marked circle, pixels that are clearly redder than the surrounding skin are
replaced with `min(green, blue)` in all three channels, the neutral repair described in
US patent 8837822. A small tint from the darkest nearby pixels is mixed back in so the
pupil matches the photo's colour balance instead of looking blue. Bright white glints keep
high green and blue values, so they survive. The mask edge is softened so there is no hard ring.

## Formats and limits

- Opens JPEG and PNG everywhere; WebP, GIF and BMP in most browsers; HEIC only in Safari.
- Saves JPEG input as JPEG (quality 97) and keeps its EXIF data (camera or scanner details).
  The orientation tag is reset because the browser has already rotated the pixels, and the
  embedded thumbnail is unlinked because it would still show red eyes.
  Other formats are saved as PNG without metadata.
- Colours are saved as sRGB, so wide-colour phone photos lose a little vividness.
- There is no automatic eye detection.
- Made for red and orange eyes in people, not the yellow or green eye-shine of pets.
- Marks are not kept if you close or reload the page.

## License

MIT. See [LICENSE](LICENSE).
