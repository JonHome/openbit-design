# UI Preview Exports

Current preview target is static web-first output derived from the JSON-first system.

## Deliverables

- `design/ui-system/previews/index.html`
  - entry page for the review pack
- `design/ui-system/previews/project-overview.html`
  - business dashboard draft
- `design/ui-system/previews/token-board.html`
  - token review board
- `design/ui-system/previews/component-gallery.html`
  - foundation catalog + domain preset gallery
- `design/ui-system/previews/preview-manifest.json`
  - generated artifact manifest

Each page is intended to have sibling exports:

- `.html`
- `.png`
- `.pdf`

## Generate HTML

```bash
node scripts/render-ui-preview-static.mjs
```

## Export PNG / PDF

```bash
node scripts/export-ui-preview-artifacts.mjs
```

## Notes

- PDF export uses Playwright CLI.
- Browser-opened HTML remains the easiest review format.
- React / RN adapter work remains available under `lib/ui-preview/` when needed again.
