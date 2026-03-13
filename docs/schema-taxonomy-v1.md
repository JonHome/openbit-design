# Schema Taxonomy v1

## Intent

Define the complete schema landscape for the JSON-first UI system before any renderer-specific implementation begins.

This taxonomy separates:

- expression mechanics
- visual design values
- component capability contracts
- domain extensions
- page composition
- preview/output adapters

## Layered Taxonomy

```text
L0  Kernel Schemas
L1  Token Schemas
L2  Catalog Schemas
L3  Preset Schemas
L4  Page Schemas
L5  Renderer Adapter Contracts
```

## L0. Kernel Schemas

These schemas define how UI is expressed.

### Required

- `node.schema.json`
- `binding.schema.json`
- `condition.schema.json`
- `action.schema.json`
- `theme-ref.schema.json`

### Optional later

- `layout-hint.schema.json`
- `responsive-rule.schema.json`
- `a11y.schema.json`
- `analytics-hook.schema.json`

### Ownership

- package: `ui-kernel`
- product-agnostic
- renderer-agnostic

## L1. Token Schemas

These schemas define visual values.

### Required

- `primitive-token.schema.json`
- `semantic-token.schema.json`
- `theme-overlay.schema.json`

### Optional later

- `motion-token.schema.json`
- `elevation-token.schema.json`
- `chart-token.schema.json`

### Ownership

- foundation owns `primitive.*` and `semantic.*`
- domain packs may add overlays like `domain.*`, `runtime.*`, `state.*`

## L2. Catalog Schemas

These schemas define what components exist and what they are allowed to do.

### Required

- `component-catalog-entry.schema.json`
- `variant.schema.json`
- `slot.schema.json`
- `prop-contract.schema.json`

### Optional later

- `action-contract.schema.json`
- `binding-contract.schema.json`
- `renderer-capability.schema.json`

### Ownership

- foundation catalog for reusable generic components
- domain catalog for business presets and domain-specific composition units

## L3. Preset Schemas

These schemas define reusable component compositions built on top of catalog entries.

### Required

- `preset.schema.json`
- `token-hook-map.schema.json`
- `preset-variant-map.schema.json`

### Purpose

Presets bridge the gap between:

- generic component capability
- domain-specific semantic expression

### Ownership

- foundation presets stay product-agnostic
- domain presets may use business vocabulary

## L4. Page Schemas

These schemas define actual screens, sections, flows, and navigation compositions.

### Required

- `page.schema.json`
- `section.schema.json`
- `flow.schema.json`
- `navigation.schema.json`

### Optional later

- `route-param.schema.json`
- `loader-contract.schema.json`
- `page-state.schema.json`

### Ownership

- application packs only

## L5. Renderer Adapter Contracts

These are not source-of-truth schemas. They are adapter contracts.

### Required

- `target-capability-contract.md`
- `node-to-renderer-map.md`
- `token-resolution-contract.md`

### Target examples

- web
- Expo / React Native
- PDF
- image snapshot
- email

### Rule

Renderer contracts must consume the upper layers. They must not redefine them.

## Canonical Dependency Direction

```text
Kernel
  ↓
Tokens
  ↓
Catalog
  ↓
Presets
  ↓
Pages
  ↓
Renderer Adapters
```

Reverse dependencies are forbidden.

## Ownership Matrix

| Layer | Owner | Product-agnostic | Renderer-agnostic |
|---|---|---:|---:|
| Kernel | `ui-kernel` | yes | yes |
| Tokens | `ui-foundation` / `ui-domain-*` | foundation yes / domain no | yes |
| Catalog | `ui-foundation` / `ui-domain-*` | foundation yes / domain no | yes |
| Presets | `ui-foundation` / `ui-domain-*` | mixed | yes |
| Pages | `app-*` | no | yes |
| Renderer contracts | `ui-renderer-*` | yes | no |

## v1 Freeze

For v1, the minimum schema set to stabilize is:

```text
node
binding
condition
action
theme-ref
component-catalog-entry
preset
page
```

All later schemas should build on these rather than bypass them.
