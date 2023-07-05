# CleanArchitecture-Basic

Clean Architecture | Setup Project Structure | Part 1

my Channel 
https://www.youtube.com/@poddarkktrickstech7988

Clean Architecture repo
https://github.com/kartik786-git/CleanArchitecture-Basic

Create minimal api .net 7 | Get | Post | Delete | Put | CURD Operation
https://youtu.be/iQ_IiO0-BqE

Create web api .net 7 (Controller-based) | Create | Update | Read | Delete | Operation
https://youtu.be/2eIOqoFpnWw


Clean Architecture is a software design pattern that aims to create a modular and maintainable codebase by separating concerns and dependencies. It promotes the separation of concerns through multiple layers and enforces boundaries between them. In this response, I'll provide an overview of Clean Architecture principles and show you a sample code structure in .NET 7.

Clean Architecture Principles:

Separation of Concerns: The codebase is divided into distinct layers, each with its own responsibilities and concerns.
Dependency Rule: Dependencies flow inward, meaning outer layers do not depend on inner layers. This allows for easy replacement or modification of components.

Abstraction over Implementation: Interfaces and abstractions are used to define contracts, decoupling high-level modules from low-level details.
Testability: The architecture facilitates unit testing by enabling isolated testing of components at different levels.
Independence of Frameworks: The core business logic is not dependent on any specific framework or library, making it more portable and maintainable.

Sample Code Structure:

Here's an example of a sample code structure in .NET 7 based on Clean Architecture principles:

Presentation Layer (Web/API)

This layer interacts with the user and handles HTTP requests and responses.
It depends on the Application layer.
It contains controllers, view models, and other UI-related components.

Application Layer

This layer contains application-specific business logic and coordinates interactions between the Presentation and Domain layers.
It depends on the Domain layer.
It contains use cases, application services, and mappers.

Domain Layer

This layer represents the core business logic of the application.
It is independent of other layers and contains domain models, entities, interfaces, and domain services.

Infrastructure Layer

This layer provides implementations for external dependencies, such as databases, external services, or third-party libraries.
It depends on the Domain and Application layers.
It contains data access implementations, repositories, external service clients, and other infrastructure-specific components.

