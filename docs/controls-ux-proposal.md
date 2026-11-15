# Controls panel: UX proposal

Status: proposal only. Nothing applied. Source: code read of `index.html` (browser pass pending).

Current panel: 9 sections, about 60 controls. Five are open by default, so the first screen is mostly scrolling.

## Cuts (need approval)

1. **Remove Export "Resolution" select.** Fix export at 600 dpi.
   - Why: default already 600. The A4 sheet code also reads `#dpi` (`buildSheets`), so one fixed scale simplifies it. Preview is always 300.
   - Risk: low. Saved JSON never stores `dpi` (not in `ids`). Larger files and slower sheets. Sheet PDF at 600 dpi is big; keep 300 for sheets if that is a problem.
2. **Remove Offset X / Offset Y sliders.** Keep Zoom slider. Drag on the preview does positioning.
   - Why: duplicate of drag-to-position. Two sliders with a 0 to 1 range are a poor way to move an image.
   - Risk: low-medium. `offx`/`offy` stay in `ids` and state, only the DOM rows go. Old JSON still loads. Add a "Reset position" link next to Zoom. Touch users lose a fine-tune path unless drag works on phones (verify).
3. **Remove the "Set code" field and "Collector number" from Card > Print details.** Printing picker already fills them on Scryfall loads.
   - Why: it is the same data the picker sets. Hand-typed custom cards rarely need a set code.
   - Risk: medium. Custom proxies lose the footer set code. Alternative: keep them, but only inside "Print details" (already there) and drop the cut. My lean: keep, do not cut.
4. **Merge the two "Random" buttons.** Keep both functions, change labels: "Random card" (Scryfall section) and "Random picture" (Picture section). Menu bar Special already uses these names.
   - Risk: none. Relabel only.
5. **Merge Photocopy and Damage into one "Aging" section** with two sub-groups, or collapse Damage into a disclosure.
   - Why: 13 sliders across two sections, most never touched.
   - Risk: low. Pure DOM move.
6. **Remove "Rules text case" select.** Rarely used, and uppercase can be typed.
   - Risk: low-medium. `rulesStyle` stays in state; old JSON with `caps` would render as typed. Skip unless you agree.

## Defaults, order, grouping (confident)

7. **Reorder sections:** Card, Picture, Frame, Aging, Collection, Export. Load a card stays first. Content comes before style.
8. **Open by default: Load a card, Card, Picture only.** Frame and Export start closed. Export actions (Download PNG, Clear card) also live in the File menu, so Export can be a small footer bar.
9. **Move "Banding strength" slider** under the Frame "Print treatment" select. It only matters for banding. Show it only when treatment is `banding`, like the poker color.
10. **Move "Invert picture" and "Border around picture"** next to the halftone controls, and put Halftone mode, Dot size, Contrast, Brightness, Invert behind an "Adjust halftone" disclosure inside Picture.
11. **Merge "Custom card" checkbox into Name.** Keep the checkbox, relabel "Custom name above real name". The current label reads as a mode switch.
12. **Move "Clear card" out of Export** into Card, as a text button.
13. **Lookup placeholder** is long. Shorten to "Card name". Move the hint to `title`.

## Relabels

- "Fit" select: "Picture fit". Options: "Fit inside", "Fill (crop)".
- "Halftone mode" to "Picture dither".
- "Handwritten note" to "Scribble".
- "Footer text (right)" to "Footer".
- "Collection (session only)" to "Collection". Keep the memory-only line in the hint.
- Button "Empty" to "Empty collection".

## Not touching

Card renderer, search (Commons / LoC), drag, printing picker, JSON import/export, PDF/PNG export. `ids` array stays intact so old saves load.
