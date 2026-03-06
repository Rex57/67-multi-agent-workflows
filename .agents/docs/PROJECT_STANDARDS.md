# Project Standards
(Coding and UI quality rules will be documented here)

## Design-to-Code Mapping
- **Stitch**: UI logic is derived from AI-generated components.
- **Pencil**: UI logic is derived from `.pen` file nodes.
    - All dimensions and colors must match `pencil_batch_get` output exactly.
    - Layouts should follow Pencil's flex/auto-layout properties where possible.
