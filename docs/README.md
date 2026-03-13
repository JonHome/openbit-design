# UI System Architecture v1

## Status

- `JSON-first` is the source of truth.
- `Penpot` is deprecated for this project and is no longer the primary design-system direction.
- `JsonRender` is the preview and output layer only.
- `OpenBit` is implemented as a domain pack on top of a product-agnostic UI kernel.

## Document Map

- `design/ui-system/ui-kernel-architecture-v1.md`
  - core kernel model
  - schema taxonomy
  - renderer adapter boundary
- `design/ui-system/foundation-domain-boundary-v1.md`
  - kernel/foundation/domain/app boundary
  - governance rules
- `design/ui-system/openbit-domain-pack-v1.md`
  - OpenBit vocabulary
  - OpenBit presets
  - OpenBit composition strategy
- `design/ui-system/schema-taxonomy-v1.md`
  - schema layer map
  - ownership matrix
  - dependency direction
- `design/ui-system/core-schema-sketches-v1.md`
  - five kernel schema drafts
  - concrete JSON examples
  - v1 formalization target

## Final Architecture

```text
ui-kernel
  ↓
ui-foundation
  ↓
ui-domain-*
  ↓
app-*
  ↓
ui-renderer-jsonrender
```

## Implemented Kernel Files

The first machine-readable kernel schemas now exist under:

- `packages/ui-kernel/README.md`
- `packages/ui-kernel/schemas/node.schema.json`
- `packages/ui-kernel/schemas/binding.schema.json`
- `packages/ui-kernel/schemas/condition.schema.json`
- `packages/ui-kernel/schemas/action.schema.json`
- `packages/ui-kernel/schemas/theme-ref.schema.json`

## Implemented Foundation/App Files

- `packages/ui-foundation/schemas/component-catalog-entry.schema.json`
- `packages/ui-foundation/schemas/variant.schema.json`
- `packages/ui-foundation/schemas/slot.schema.json`
- `packages/ui-foundation/schemas/prop-contract.schema.json`
- `packages/ui-foundation/schemas/token-hook-map.schema.json`
- `packages/ui-foundation/schemas/preset-variant-map.schema.json`
- `packages/ui-foundation/schemas/preset.schema.json`
- `packages/app-openbit/schemas/page.schema.json`
- `packages/app-openbit/schemas/section.schema.json`
- `packages/app-openbit/schemas/flow.schema.json`
- `packages/app-openbit/schemas/navigation.schema.json`
- `packages/ui-renderer-jsonrender/contracts/target-capability-contract.md`
- `packages/ui-renderer-jsonrender/contracts/node-to-renderer-map.md`
- `packages/ui-renderer-jsonrender/contracts/token-resolution-contract.md`
- `packages/app-openbit/examples/project-overview.page.json`

## Preview Result

The preview layer is intentionally thin. The same page spec can be rendered to:

- web page
- Expo / React Native screen
- image snapshot
- PDF
- email-compatible target

Static design-review artifacts now live under:

- `design/ui-system/previews/index.html`
- `design/ui-system/previews/project-overview.html`
- `design/ui-system/previews/token-board.html`
- `design/ui-system/previews/component-gallery.html`
- `design/ui-system/previews/preview-manifest.json`
- `design/ui-system/previews/README.md`

Generator scripts:

- `scripts/render-ui-preview-static.mjs`
- `scripts/export-ui-preview-artifacts.mjs`

Example preview shape for `OpenBit Project Overview`:

```text
┌──────────────────────────────────────────────────────────────┐
│ Project Overview                                             │
│ Atlas / status / participants / last runtime                 │
├──────────────────────────────────────────────────────────────┤
│ [Progress] [Tasks] [Runs] [Risk]                             │
├──────────────────────────────────────────────────────────────┤
│ Narrative Panel                                              │
│ Project context, intent, scope, current decision signal      │
├───────────────────────────────┬──────────────────────────────┤
│ Requirement List              │ Recent Runtime Activity      │
│ - Requirement A               │ - Run #201 success          │
│ - Requirement B               │ - Run #202 retry           │
│ - Requirement C               │ - Eval revision            │
├───────────────────────────────┴──────────────────────────────┤
│ Task Strip                                                    │
│ [Task A] [Task B] [Task C] [Task D]                          │
├──────────────────────────────────────────────────────────────┤
│ Participants / Resources / Artifacts                         │
└──────────────────────────────────────────────────────────────┘
```

Representative composition result:

```json
{
  "page": "page.project-overview",
  "themeRef": {
    "theme": "foundation.dark",
    "domainTheme": "openbit.dark"
  },
  "sections": [
    "openbit.page-header",
    "openbit.summary-grid",
    "openbit.narrative-panel",
    "openbit.requirement-list",
    "openbit.runtime-activity",
    "openbit.task-strip",
    "openbit.participant-panel"
  ]
}
```
