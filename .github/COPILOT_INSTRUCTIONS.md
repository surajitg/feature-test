# Copilot Code Review Instructions for C# Clean Architecture Project

## Project Structure
- **Domain Layer**: Contains core business entities, value objects, enums, and domain services. Must remain free of external dependencies.
- **Business Layer (Application)**: Contains use cases, commands, queries, and business logic. Should depend only on Domain layer. Implements vertical slice architecture for pages.
- **Infrastructure Layer**: Contains persistence, external services, and framework-specific implementations. Depends on Business and Domain layers but never the other way around.

## Review Guidelines

### ✅ Architecture & Layering
- Ensure **no direct dependencies** from Domain → Infrastructure or Domain → Business.
- Verify **Dependency Injection** is used for all external services, repositories, and handlers.
- Check that **vertical slice architecture** is respected:
  - Each feature (command/query/page) is self-contained.
  - Handlers, DTOs, and validators are grouped per slice.

### ✅ Coding Best Practices
- Follow **C# coding conventions** (naming, spacing, async/await usage).
- Ensure **SOLID principles** are applied:
  - Single Responsibility: Each class has one clear purpose.
  - Open/Closed: Classes are extendable without modification.
  - Dependency Inversion: High-level modules depend on abstractions.
- Validate **exception handling** and proper use of `ILogger<T>` for logging.
- Confirm **unit tests** exist for business logic and domain rules.

### ✅ Dependency Injection
- All services, repositories, and handlers must be registered in DI container.
- Avoid **service locator anti-pattern**.
- Ensure scoped vs singleton lifetimes are correctly applied.

### ✅ Vertical Slice Pages
- Each page/feature should:
  - Have its own command/query + handler.
  - Keep controllers thin (delegate to handlers).
  - Use MediatR or equivalent for request/response handling.
- Ensure **validation** is implemented via FluentValidation or similar.

### ✅ Infrastructure
- Repository implementations must follow **interface contracts** defined in Business layer.
- Database context should be injected, not instantiated directly.
- External API calls should be abstracted behind interfaces.

### ✅ Security & Performance
- Ensure **input validation** and **null checks** are present.
- Avoid **blocking calls** in async code.
- Confirm **EF Core queries** are optimized (no N+1 issues).
- Sensitive data must not be logged.

---

## Copilot Review Prompts
When reviewing pull requests, Copilot should:
1. Check adherence to Clean Architecture boundaries.
2. Flag violations of dependency rules (e.g., Domain referencing Infrastructure).
3. Suggest improvements for DI registration and lifetimes.
4. Recommend refactoring if vertical slice boundaries are blurred.
5. Ensure code readability, maintainability, and performance best practices.
