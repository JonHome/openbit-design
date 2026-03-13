# Foundation-Domain Boundary v1

## Intent

Keep the lower layers reusable across products.

```text
If it still makes sense outside OpenBit, it can live below the domain layer.
If it depends on OpenBit semantics, it must stay above the domain boundary.
```

## Boundaries

```text
Kernel
Foundation
Domain Pack
App Composition
```

## Kernel Boundary

Kernel owns pure expression mechanics only.

Allowed:

- node tree
- slots
- variants
- state
- binding
- conditions
- actions
- theme references

Forbidden:

- `agent`
- `project`
- `requirement`
- `task`
- `run`
- `artifact`

## Foundation Boundary

Foundation owns reusable visual and structural capability.

Allowed component families:

- `layout.stack`
- `layout.inline`
- `layout.grid`
- `layout.split`
- `layout.section`
- `content.text`
- `content.icon`
- `content.image`
- `surface.box`
- `surface.card`
- `surface.panel`
- `surface.row`
- `feedback.badge`
- `feedback.banner`
- `feedback.empty`
- `feedback.skeleton`
- `navigation.tabs`
- `navigation.breadcrumb`
- `navigation.nav-rail`
- `data.list`
- `data.table`
- `data.timeline`
- `data.property-list`

Allowed tokens:

- `primitive.*`
- `semantic.surface.*`
- `semantic.text.*`
- `semantic.border.*`
- `semantic.icon.*`
- `semantic.focus.*`
- `semantic.feedback.*`

Forbidden:

- `domain.agent.*`
- `runtime.cost.*`
- `artifact.lineage.*`
- page-specific presets

## Domain Boundary

Domain packs own business semantics, but not concrete product pages.

Allowed in `ui-domain-openbit`:

- domain vocabulary
- domain token overlays
- domain presets
- domain-specific list and card contracts
- domain-specific binding helpers

Examples:

- `openbit.object-card`
- `openbit.object-row`
- `openbit.page-header`
- `openbit.run-attempt-card`
- `openbit.artifact-chip`
- `openbit.evaluation-badge`
- `openbit.runtime-timeline-row`

## App Boundary

App composition owns:

- page definitions
- flow definitions
- route binding
- navigation structure
- composition-level visibility rules

Examples:

- `page.home`
- `page.project-overview`
- `page.requirement-detail`
- `page.task-detail`
- `page.agent-profile`
- `page.run-detail`

## Classification Examples

| Artifact | Layer | Reason |
|---|---|---|
| `surface.card` | Foundation | generic structural capability |
| `data.timeline` | Foundation | generic chronology pattern |
| `openbit.run-attempt-card` | Domain | OpenBit runtime semantics |
| `openbit.artifact-chip` | Domain | OpenBit artifact lineage meaning |
| `page.project-overview` | App | product-specific composition |
| `page.run-detail` | App | product-specific composition |

## Anti-Patterns

Do not place these in foundation:

- `ProjectCard`
- `TaskCard`
- `RunHeader`
- `AgentCapabilityPanel`
- `RequirementAcceptancePanel`

Do not place these in kernel:

- domain entity ids
- product navigation rules
- renderer-specific props

## Variant Discipline

Variants belong in variant fields, not component ids.

Preferred:

```text
surface.card + tone=raised
openbit.object-card + objectType=task
```

Avoid:

```text
RaisedCard
TaskCard
RunFailedCard
```
