# `ui-foundation` Schemas

These schemas formalize the reusable foundation layer that sits above `ui-kernel` and below any domain pack.

## Files

- `variant.schema.json`
- `slot.schema.json`
- `prop-contract.schema.json`
- `component-catalog-entry.schema.json`
- `token-hook-map.schema.json`
- `preset-variant-map.schema.json`
- `preset.schema.json`

## Notes

- These schemas describe capability and composition contracts, not final rendered UI.
- Domain packs may consume these contracts but should not weaken them.
