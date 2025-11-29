# GitHub Copilot Instructions for .NET Code Review

These instructions guide Copilot (and contributors) to review .NET code using **Clean Architecture** and **Vertical Slice Architecture** principles.

---

## 1. Clean Architecture Principles
- Domain layer contains only business rules and entities.
- Application layer orchestrates use cases, independent of infrastructure.
- Infrastructure layer implements interfaces for persistence/external services.
- Presentation layer depends only on Application layer.
- No direct references from Domain → Infrastructure.
- Business logic must be unit‑testable without external dependencies.

---

## 2. Vertical Slice Architecture Principles
- Each feature/use case is self‑contained:
  - Request/Response models, handler, and validation grouped together.
- CQRS alignment:
  - Commands mutate state; Queries return data.
- Folder structure:
  - Features organized by slice (e.g., `Features/Orders/CreateOrder`).
- Avoid cross‑slice coupling unless explicitly required.

---

## 3. Code Quality Checklist
- Naming conventions follow .NET standards.
- Async/await usage is correct; avoid blocking calls.
- Dependency Injection is consistent.
- Validation logic is explicit, not hidden in controllers.
- Logging and exception handling are consistent across slices.
- Unit and integration tests exist for each vertical slice.

---

## 4. Review Output Expectations
When Copilot reviews code:
- Highlight violations of Clean or Vertical Slice principles.
- Suggest refactoring strategies (e.g., move logic from controller → handler).
- Recommend improvements in readability, maintainability, and testability.
- Provide concise examples of better structure when needed.
