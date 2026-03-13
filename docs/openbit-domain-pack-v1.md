# OpenBit Domain Pack v1

## Intent

OpenBit is modeled as a domain pack on top of a product-agnostic UI system.

This document defines how OpenBit plugs into the generic kernel without contaminating it.

## OpenBit Vocabulary

### Entity vocabulary

- `agent`
- `organization`
- `project`
- `requirement`
- `task`
- `resource`
- `run`
- `artifact`
- `model`

### Runtime vocabulary

- `attempt`
- `evaluation`
- `cost`
- `retry`
- `fallback`
- `lineage`
- `status`
- `assignment`
- `evidence`

These words are valid in the OpenBit domain pack only.

## OpenBit Token Overlay

OpenBit extends foundation semantics with domain and runtime overlays.

Suggested namespaces:

- `domain.*`
- `runtime.*`
- `state.*`
- `component.*`

Examples:

- `domain.agent.accent`
- `domain.project.surface`
- `runtime.cost.warn`
- `runtime.lineage.output`
- `state.failed.border`

Foundation remains owner of:

- `primitive.*`
- `semantic.*`

## OpenBit Domain Presets

Suggested preset ids:

- `openbit.page-header`
- `openbit.summary-grid`
- `openbit.object-card`
- `openbit.object-row`
- `openbit.status-badge`
- `openbit.domain-badge`
- `openbit.cost-badge`
- `openbit.artifact-chip`
- `openbit.evaluation-badge`
- `openbit.run-attempt-card`
- `openbit.runtime-timeline-row`
- `openbit.attention-panel`
- `openbit.property-panel`
- `openbit.artifact-list`

## OpenBit Page Strategy

OpenBit pages compose domain presets rather than raw foundation shapes.

### Home

- `openbit.page-header`
- `openbit.summary-grid`
- `openbit.active-work-strip`
- `openbit.runtime-snapshot`
- `openbit.actor-panel`
- `openbit.artifact-list`
- `openbit.attention-panel`

### Project Overview

- `openbit.page-header`
- `openbit.summary-grid`
- `openbit.narrative-panel`
- `openbit.requirement-list`
- `openbit.task-strip`
- `openbit.participant-panel`
- `openbit.runtime-activity`

### Requirement Detail

- `openbit.page-header`
- `openbit.problem-panel`
- `openbit.context-panel`
- `openbit.participant-panel`
- `openbit.task-list`
- `openbit.resource-list`
- `openbit.latest-execution-signal`

### Task Detail

- `openbit.page-header`
- `openbit.definition-of-done`
- `openbit.assignment-panel`
- `openbit.run-summary`
- `openbit.attempt-timeline`
- `openbit.evaluation-summary`
- `openbit.artifact-list`

### Agent Profile

- `openbit.page-header`
- `openbit.capability-panel`
- `openbit.model-binding-panel`
- `openbit.assignment-list`
- `openbit.latest-runs`
- `openbit.owned-resources`
- `openbit.artifact-list`

### Run Detail

- `openbit.page-header`
- `openbit.step-timeline`
- `openbit.attempt-stack`
- `openbit.cost-summary`
- `openbit.evaluation-panel`
- `openbit.io-artifact-list`
- `openbit.related-context`

## Example OpenBit Composition

```json
{
  "id": "page.project-overview",
  "themeRef": {
    "theme": "foundation.dark",
    "domainTheme": "openbit.dark"
  },
  "root": {
    "component": "layout.section",
    "slots": {
      "children": [
        {
          "component": "openbit.page-header",
          "bind": {
            "entity": "$data.project"
          }
        },
        {
          "component": "openbit.summary-grid",
          "bind": {
            "stats": "$data.summary"
          }
        },
        {
          "component": "openbit.requirement-list",
          "bind": {
            "items": "$data.requirements"
          }
        },
        {
          "component": "openbit.runtime-activity",
          "bind": {
            "items": "$data.runs"
          }
        }
      ]
    }
  }
}
```

## Data-Binding Principle

OpenBit views should bind to normalized view models rather than raw backend objects.

```text
domain entity
  ↓
view-model mapper
  ↓
page spec bindings
  ↓
renderer
```

This keeps the UI system independent from storage or API shape changes.
