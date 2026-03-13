# UI Kernel Architecture v1

## Intent

Build a product-agnostic UI system whose source of truth is structured JSON rather than a canvas tool.

The kernel describes how UI is expressed, not what business domain it represents.

## Core Principle

```text
Core JSON = what the UI means
Renderer  = how the UI is displayed
```

## Architectural Layers

```text
UI Kernel
  node / slot / variant / state / bind / action / condition / themeRef

Foundation System
  tokens / primitives / generic catalog / base presets

Domain Pack
  domain vocabulary / domain presets / domain theme overlay

App Composition
  pages / flows / navigation / data mapping

JsonRender Adapter
  web / expo / pdf / image / email
```

## Package Topology

```text
packages/
  ui-kernel/
    schemas/
      node.schema.json
      binding.schema.json
      condition.schema.json
      action.schema.json
      theme-ref.schema.json

  ui-foundation/
    tokens/
    catalog/
    presets/

  ui-renderer-jsonrender/
    adapters/

  ui-domain-*/
    vocab/
    tokens/
    catalog/
    presets/

  app-*/
    pages/
    flows/
    navigation/
```

## Kernel Responsibilities

Allowed:

- node tree structure
- slots
- props
- variants
- state
- data binding
- visibility conditions
- action contracts
- layout primitives
- theme references
- accessibility metadata

Forbidden:

- product domain vocabulary
- renderer-specific style objects
- React props conventions
- Expo-only layout rules
- PDF-only output hacks

## Core Schemas

### Node

```json
{
  "id": "node-id",
  "type": "component",
  "component": "surface.card",
  "variant": {
    "tone": "default",
    "density": "comfortable"
  },
  "props": {},
  "slots": {},
  "bind": {},
  "visibleWhen": {},
  "actions": []
}
```

### Binding

```json
{
  "text": "$data.project.name",
  "items": "$data.requirements",
  "status": "$derived.status"
}
```

### Condition

```json
{
  "all": [
    { "path": "$data.run.status", "op": "=", "value": "failed" },
    { "path": "$viewer.mode", "op": "!=", "value": "compact" }
  ]
}
```

### Action

```json
{
  "type": "navigate",
  "target": "page.task-detail",
  "params": {
    "taskId": "$data.task.id"
  }
}
```

### ThemeRef

```json
{
  "theme": "foundation.dark",
  "domainTheme": "openbit.dark"
}
```

## Data Flow

```text
tokens + catalog + presets + page + data
                 │
                 ▼
           schema validation
                 │
                 ▼
         normalized composition tree
                 │
                 ▼
        variant + token resolution
                 │
                 ▼
         JsonRender target adapter
```

## Catalog Contract

Each component catalog entry must provide:

- stable component id
- prop schema
- variant schema
- slot schema
- action contract
- token hooks
- renderer mapping metadata

Example:

```json
{
  "id": "surface.card",
  "kind": "component",
  "slots": ["header", "body", "footer"],
  "props": {
    "interactive": "boolean"
  },
  "variants": {
    "tone": ["default", "subtle", "raised"],
    "density": ["compact", "comfortable"]
  },
  "tokenHooks": {
    "surface": "semantic.surface.card",
    "border": "semantic.border.default"
  }
}
```

## Stable Naming Rules

- page ids use `page.*`
- foundation components use short generic ids like `surface.card`
- domain presets use prefixed ids like `openbit.object-card`
- token ids are stable semantic paths, not renderer paths

## Renderer Boundary

`ui-renderer-jsonrender` is a consumer only.

It may:

- resolve the node tree
- map catalog ids to target components
- render to supported targets
- generate snapshots and previews

It may not:

- invent schema fields
- contain domain logic
- redefine token semantics
- serve as the design source of truth
