# booklet-pdf

A single-file, fully client-side booklet imposition tool. Turn any PDF into a
foldable, bindable booklet using nothing but your printer's "pages per sheet"
setting — no Acrobat, no server, no uploads.

**Live tool:** `https://<your-username>.github.io/booklet-pdf/`

## What it does

- Generates the saddle-stitch page order (e.g. `24,1,2,23,…`) for any page count
- Splits long documents into multiple booklets — by count or by max pages per booklet
- Handles 2 / 4 / 6 / 9 / 16 pages per sheet, as folded signatures (even-column
  grids) or cut & stack piles (any grid)
- LTR and RTL (Arabic) books — RTL mirrors every spread so the spine lands on the right
- One-sided books: content on recto pages only, covers printed as usual
- Padding placement: front / back / front-and-back / end, plus a
  "start page 2 on the reading side" option
- **Load a PDF** and download a ready-to-print copy with pages reordered and
  blank pages inserted — processed entirely in the browser with
  [pdf-lib](https://pdf-lib.js.org/), nothing leaves your device
- Sheet-by-sheet preview with fold/cut guides and per-sheet page ranges of the
  generated PDF, so a jammed sheet can be reprinted by range

## Printing

1. Load your PDF, pick a layout, download the imposed PDF
2. Print **all pages in order**, pages-per-sheet set to your chosen layout,
   two-sided with the flip that mirrors left↔right
3. Fold along the dashed guides (cut along solid ones first for multi-up
   layouts), bind at the fold

Without a PDF loaded the tool still produces a copy-paste page serial for
print dialogs that respect page-list order (Acrobat, Foxit, most native dialogs).

## Deploy on GitHub Pages

This is a static single file — no build step.

```bash
cd booklet-pdf
git init -b main && git add -A && git commit -m "booklet imposition tool"
gh repo create booklet-pdf --public --source=. --remote=origin --push
gh api "repos/{owner}/booklet-pdf/pages" -X POST -f "source[branch]=main" -f "source[path]=/"
```

Or without `gh`: create the repo on github.com, push, then
Settings → Pages → Deploy from a branch → `main` / `/ (root)`.

## Notes

- pdf-lib and the fonts load from CDNs, so the PDF features need an internet
  connection; the page-serial calculator works offline once the page is cached
- Password-protected PDFs are rejected with a message
- Always print one test sheet first; if backs land behind the wrong halves,
  switch the "back side mirrors" option or your printer's flip setting
