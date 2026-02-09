# Metal Rendering

## Setup
- Use `MTKView` hosted in SwiftUI via `UIViewRepresentable`.
- Keep render pipeline simple, avoid heavy CPU sync.

## Performance
- Prefer triple buffering.
- Avoid per-frame resource creation.
