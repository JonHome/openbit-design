# Core Schema Sketches v1

## Intent

Provide concrete draft shapes for the five required kernel schemas:

- `node`
- `binding`
- `condition`
- `action`
- `theme-ref`

These are architecture sketches, not final machine-validated JSON Schema files yet.

## 1. Node Schema Sketch

### Purpose

Describe a renderable UI node in a renderer-agnostic form.

### Draft shape

```json
{
  "id": "project-overview.header",
  "kind": "component",
  "component": "openbit.page-header",
  "variant": {
    "tone": "default",
    "density": "comfortable"
  },
  "props": {
    "sticky": false
  },
  "slots": {
    "actions": [],
    "meta": []
  },
  "bind": {
    "entity": "$data.project"
  },
  "visibleWhen": null,
  "actions": [],
  "themeRef": {
    "theme": "foundation.dark",
    "domainTheme": "openbit.dark"
  }
}
```

### Required fields

- `id`
- `kind`
- `component`

### Optional fields

- `variant`
- `props`
- `slots`
- `bind`
- `visibleWhen`
- `actions`
- `themeRef`

### Notes

- `kind` may later distinguish `component`, `slot`, `fragment`, `text`, `collection`
- `component` must resolve through a catalog entry
- `slots` should contain nodes or collections of nodes, never renderer-native structures

## 2. Binding Schema Sketch

### Purpose

Describe how a node reads from a view-model or derived state.

### Draft shape

```json
{
  "entity": "$data.project",
  "title": "$data.project.name",
  "subtitle": "$data.project.summary",
  "status": "$derived.projectStatus",
  "items": "$data.requirements"
}
```

### Rules

- bindings always resolve against normalized view-models
- bindings should stay declarative
- bindings should not embed imperative logic

### Forbidden

- arbitrary JS
- renderer-specific expressions
- backend transport details

## 3. Condition Schema Sketch

### Purpose

Control visibility and branch selection declaratively.

### Draft shape

```json
{
  "all": [
    { "path": "$data.run.status", "op": "=", "value": "failed" },
    { "path": "$viewer.mode", "op": "!=", "value": "compact" }
  ]
}
```

### Supported operators in v1

- `=`
- `!=`
- `in`
- `not_in`
- `exists`
- `not_exists`
- `>`
- `>=`
- `<`
- `<=`

### Supported combinators in v1

- `all`
- `any`
- `not`

### Notes

- conditions must be serializable
- conditions must be deterministic

## 4. Action Schema Sketch

### Purpose

Describe user or system actions without binding to platform event code.

### Draft shape

```json
{
  "type": "navigate",
  "target": "page.task-detail",
  "params": {
    "taskId": "$data.task.id"
  }
}
```

### v1 action types

- `navigate`
- `open`
- `submit`
- `invoke`
- `select`
- `toggle`

### Notes

- action execution is adapter-owned
- action meaning is schema-owned
- side effects must be explicit in the contract

## 5. ThemeRef Schema Sketch

### Purpose

Describe which theme layers should resolve for a node subtree.

### Draft shape

```json
{
  "theme": "foundation.dark",
  "domainTheme": "openbit.dark"
}
```

### Rules

- foundation theme is optional but recommended
- domain theme is optional and only valid when a domain pack is involved
- theme references must stay symbolic, not resolved into raw values

## 6. Combined Example

```json
{
  "id": "page.project-overview.summary",
  "kind": "component",
  "component": "openbit.summary-grid",
  "variant": {
    "density": "comfortable"
  },
  "bind": {
    "stats": "$data.summary"
  },
  "visibleWhen": {
    "any": [
      { "path": "$data.summary.runCount", "op": ">", "value": 0 },
      { "path": "$data.summary.taskCount", "op": ">", "value": 0 }
    ]
  },
  "actions": [
    {
      "type": "navigate",
      "target": "page.project-overview"
    }
  ],
  "themeRef": {
    "theme": "foundation.dark",
    "domainTheme": "openbit.dark"
  }
}
```

## 7. v1 Constraints

To keep v1 stable:

- no arbitrary scripting in bindings
- no renderer-native props in nodes
- no domain words inside kernel field names
- no token values directly embedded in page composition

## 8. Next Formalization Step

After this sketch phase, the next deliverable should be:

- machine-readable JSON Schema files under `packages/ui-kernel/schemas/`
- a validation pipeline that checks page specs against catalog and kernel contracts
