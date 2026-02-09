# SwiftUI Patterns

## Structure
- `App` -> `Scene` -> root view with environment objects.
- Keep audio engine in a long-lived model object.

## State
- Use `@StateObject` for the engine controller.
- Debounce UI-driven parameter updates.
