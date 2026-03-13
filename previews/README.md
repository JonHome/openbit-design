# UI Preview Exports

Current preview target is static web-first output derived from the JSON-first system.

## Deliverables

- `design/ui-system/previews/index.html`
  - locale selector entry
- `design/ui-system/previews/en/index.html`
  - English design pack entry
- `design/ui-system/previews/zh/index.html`
  - Chinese design pack entry
- `design/ui-system/previews/en/project-overview.html`
- `design/ui-system/previews/zh/project-overview.html`
- `design/ui-system/previews/en/token-board.html`
- `design/ui-system/previews/zh/token-board.html`
- `design/ui-system/previews/en/component-gallery.html`
- `design/ui-system/previews/zh/component-gallery.html`
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
