# Unity Development Instructions

## Environment
- Game Engine: Unity 6
- Language: C#
- IDE: Visual Studio Code
- AI Agent: OpenAI Codex or Else
- Editor Integration: Unity MCP
- Audio Middleware: Wwise



## Workflow
1. Inspect the relevant project files.
2. Explain the planned changes briefly.
3. Implement the requested feature.
4. Validate the result using Unity MCP.
5. Check compilation errors.
6. Summarize changes and remaining issues.
7. Check Goals.MD



<!-- Starting Technical Rules -->



## Architecture Rules

### 1. Core Architecture
- The project must follow **classical Object-Oriented Programming (OOP)** principles.
- Apply **encapsulation, abstraction, inheritance, and polymorphism** where appropriate.
- Follow **SOLID principles**, while avoiding excessive abstraction and unnecessary architectural complexity.
- Prefer **high cohesion, low coupling, and maximum code reusability**.
- Favor simple, maintainable, and extensible designs over unnecessarily complex architectures.
- **Do not introduce ECS, DOTS, or data-oriented architectures** unless explicitly requested.
- Do not introduce new architectural patterns or frameworks without clear justification.

### 2. Class and Object Design
- Each class must have a clearly defined responsibility.
- Reuse and extend existing classes before creating new ones.
- **Minimize the total number of classes and objects.**
- Do not create a new class for functionality that can reasonably be implemented within an existing class.
- Use inheritance when a genuine *is-a* relationship exists.
- Prefer composition when inheritance would introduce unnecessary coupling.
- Avoid excessive inheritance hierarchies and unnecessary polymorphism.
- Do not create interfaces or abstract classes solely for hypothetical future extensibility.
- Avoid unnecessary wrapper classes, utility classes, and redundant abstractions.

### 3. Manager and Component Restrictions
- **Strictly minimize the creation of Manager classes and MonoBehaviour components.**
- Do not create a new Manager for every gameplay feature or subsystem.
- Before creating a Manager, verify whether an existing class can reasonably handle the responsibility.
- Manager classes are permitted only when centralized coordination or lifecycle management is genuinely necessary.
- Do not introduce unnecessary Singleton instances or global access points.
- **Do not create a separate MonoBehaviour component for every small behavior.**
- Prefer consolidating closely related functionality into existing components when doing so preserves cohesion.
- Avoid excessive fragmentation of gameplay logic across multiple scripts.
- Every new Manager or Component must have a clearly justified responsibility.

### 4. Unity Integration
- Use `MonoBehaviour` only when Unity lifecycle callbacks, scene integration, or component-specific functionality are required.
- Prefer ordinary C# classes for logic that does not require Unity-specific behavior.
- Avoid unnecessary GameObjects, empty parent objects, and redundant components.
- Keep scene hierarchies simple and organized.
- Use `[SerializeField] private` for Inspector-configurable fields when appropriate.
- Avoid unnecessary runtime object searches and repeated component lookups.

### 5. Dependency Management
- Prefer explicit dependencies and direct references when appropriate.
- Avoid circular dependencies.
- Do not introduce dependency injection frameworks without explicit approval.
- Use interfaces only when multiple implementations, testing requirements, or architectural boundaries justify them.
- Avoid unnecessary Service Locator, Factory, Repository, and Event Bus patterns.
- Do not use design patterns merely for the sake of using design patterns.

### 6. Communication and Control Flow
- Prefer direct method calls for simple, closely related object interactions.
- Use events and delegates when loose coupling or asynchronous notifications are genuinely beneficial.
- Avoid introducing an Event Bus for simple communication.
- Do not create excessive layers of event forwarding.
- Keep execution flow explicit, predictable, and easy to trace.

### 7. Performance and Memory Management
- Consider memory allocation, Garbage Collection, and runtime performance.
- Avoid unnecessary allocations in frequently executed methods.
- Cache frequently used references when appropriate.
- Use object pooling only when repeated allocation and destruction justify it.
- Do not introduce multithreading, Jobs, Burst, or other optimization systems without demonstrated need.
- Prefer profiling-driven optimization over speculative optimization.

### 8. Audio and External Systems
- Use Wwise as the primary audio middleware.
- Keep Wwise integration simple and centralized where appropriate.
- Avoid creating unnecessary AudioManager or AudioService abstractions.
- Direct Wwise event calls are permitted when they do not introduce significant coupling or duplication.
- Introduce abstraction layers only when they provide clear practical benefits.

### 9. AI Agent Constraints
- **Before creating any new class, Manager, Component, or Interface, inspect the existing implementation for reusable functionality.**
- **Do not increase the number of scripts, components, or architectural layers without a concrete reason.**
- Prefer modifying existing code over creating additional files when responsibilities remain cohesive.
- Do not refactor working code solely to introduce design patterns.
- Do not split a class merely to satisfy an arbitrary line-count or method-count threshold.
- Avoid speculative extensibility and overengineering.
- Keep implementations as simple as possible while preserving maintainability.
- Request approval before introducing major architectural changes.
- Explain why each newly introduced Manager, Component, or Interface is necessary.
- Preserve existing project structure and conventions unless explicitly instructed otherwise.

### 10. Validation
- Ensure that architectural changes do not introduce unnecessary complexity.
- Verify that existing functionality remains operational.
- Check compilation errors after code modifications.
- Use Unity MCP to validate scene and component changes when available.
- Report any unverified behavior or integration issues explicitly.



## Naming Rules

### 1. Classes
- Class names must follow **camelCase** naming conventions (e.g., `playerController`).
- Classes should be designed with **maximum reusability** in mind, emphasizing high levels of abstraction and compatibility with established design patterns.

### 2. Variables
- Variable names must follow **snake_case** naming conventions (e.g., `is_variable`).
- Variable lifetime and management strategies may be adjusted to accommodate performance optimizations, particularly when using **Unity DOTS, Burst Compiler**, or similar technologies.
- Dynamic memory allocation must always account for potential **Garbage Collection (GC)** overhead.

### 3. Constants
- Constant names must use **UPPER_CASE** conventions (e.g., `const float PI = 3.14f;`).
- Excessive use of preprocessor directives, such as `#define` and `#if`, is prohibited. As a general guideline, limit their usage to approximately **10–20 directives per file**.

### 4. Functions and Methods
- Function and method names must follow **PascalCase** naming conventions (e.g., `GetEven()`).
- Function and method names should generally begin with a **verb** describing their intended behavior.
- Exceptions are permitted when justified, but they must be explicitly documented in the corresponding **SVC comments**.

### 5. Other Language and Unity Structures
- Naming conventions for other constructs, including **structs, delegates, events, and Unity/C#-specific structures**, should follow the conventions of the most closely related category (class, variable, constant, or function).
- If no applicable convention is explicitly defined, **camelCase** should be used as the default.



<!-- Under : ETC Rules -->



## Wwise Rules
- Use Wwise for gameplay audio.
- Do not use Unity AudioSource for new gameplay audio.
- Use descriptive event names like:
  Play_PlayerAttack, Play_EnemyHit, Play_BGM.
- Do not modify Wwise project files without approval.



