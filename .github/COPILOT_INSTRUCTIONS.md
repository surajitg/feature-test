# Copilot Instructions for C# Clean Architecture Project

This file defines unified guidance for Copilot across **code review**, **code completion**, **documentation**, **testing**, and **unit test generation**.

## Project Structure
- **Domain Layer**: Contains core business entities, value objects, enums, and domain services. Must remain free of external dependencies.
- **Business Layer (Application)**: Contains use cases, commands, queries, and business logic. Should depend only on Domain layer. Implements vertical slice architecture for pages.
- **Infrastructure Layer**: Contains persistence, external services, and framework-specific implementations. Depends on Business and Domain layers but never the other way around.

## Code Review

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

## ✍️ Code Completion
- Generate C# code that respects **Domain, Business, Infrastructure layering**.
- Always use **Dependency Injection** for external services and repositories.
- Apply **Vertical Slice Architecture** for pages:
  - Self-contained features (command/query/handler).
  - Use MediatR or equivalent for request/response.
- Follow **C# conventions**:
  - Async/await for asynchronous operations.
  - Meaningful naming conventions.
  - Classes small and focused (SRP).
- Ensure generated code is **testable and maintainable**.

---

## 📖 Documentation
- Add **XML comments** for all public methods, classes, and interfaces.
- Summaries must explain **purpose, parameters, and return values**.
- Provide **usage examples** where relevant.
- Document **Clean Architecture responsibilities**:
  - Domain: core business rules/entities.
  - Business: use cases, commands, queries.
  - Infrastructure: persistence, external services.
- Clarify **Dependency Injection setup** and **vertical slice features**.

---

## 🧪 Testing
- Ensure **unit tests** exist for:
  - Domain entities and value objects.
  - Business logic (commands, queries, handlers).
- Use **mocking frameworks** (e.g., Moq) for external dependencies.
- Follow **AAA pattern** (Arrange, Act, Assert).
- Validate **edge cases and error handling**.
- Ensure **integration tests** for Infrastructure (repositories, API calls).
- Maintain **high coverage** without sacrificing readability.

---

## 🧩 Unit Test Generation
When generating unit tests, Copilot should:
- Create **xUnit or NUnit tests** (consistent with project setup).
- Follow **AAA pattern**:
  - **Arrange**: set up test data and mocks.
  - **Act**: call the method under test.
  - **Assert**: verify expected outcomes.
- Use **Moq** (or equivalent) for mocking dependencies.
- Cover:
  - Happy path scenarios.
  - Edge cases (nulls, empty collections, invalid inputs).
  - Exception handling and logging.
- Ensure tests are **isolated** (no reliance on external state).
- Name tests clearly (`MethodName_ShouldExpectedBehavior_WhenCondition`).
- Keep tests **fast, deterministic, and independent**.

---

## ✅ Copilot Review Prompts
When assisting, Copilot should:
1. Flag violations of Clean Architecture boundaries.
2. Suggest improvements for DI registration and lifetimes.
3. Recommend refactoring if vertical slice boundaries are blurred.
4. Generate code that is testable, maintainable, and documented.
5. Ensure unit and integration tests are present and meaningful.
6. Generate new unit tests that follow AAA, mocking, and naming best practices.

