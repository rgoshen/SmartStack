# Component Diagram: API Application

**C4 Level**: 3
**Type**: Component
**Scope**: Internal structure of the API Application container
**Primary Elements**: Components, controllers, services, and modules within the API
**Intended Audience**: Developers, technical architects
**Last Updated**: 2025-05-11

## Purpose

This diagram shows the internal component structure of the API Application, illustrating how the Nest.js modules are organized and how they interact to provide the REST API functionality.

## Diagram

```mermaid
graph TB
    %% Styling
    classDef controller fill:#4CAF50,stroke:#43A047,stroke-width:2px,color:#fff
    classDef service fill:#2196F3,stroke:#1976D2,stroke-width:2px,color:#fff
    classDef module fill:#FF9800,stroke:#F57C00,stroke-width:2px,color:#fff
    classDef external fill:#999999,stroke:#8a8a8a,stroke-width:2px,color:#fff
    classDef person fill:#08427b,stroke:#073b6f,stroke-width:2px,color:#fff
    classDef gateway fill:#9C27B0,stroke:#7B1FA2,stroke-width:2px,color:#fff

    %% External actors
    WebApp["Web Application<br/>[Container]"]:::external

    %% API Gateway
    Gateway["API Gateway<br/>[Component]<br/><br/>Routes requests and<br/>handles authentication"]:::gateway

    %% Controllers
    AuthController["Auth Controller<br/>[Component]<br/><br/>Handles authentication<br/>endpoints"]:::controller
    TaskController["Task Controller<br/>[Component]<br/><br/>Manages task CRUD<br/>operations"]:::controller
    ClientController["Client Controller<br/>[Component]<br/><br/>Manages client data<br/>and communications"]:::controller
    ProjectController["Project Controller<br/>[Component]<br/><br/>Handles project<br/>operations"]:::controller
    ShareLinkController["Share Link Controller<br/>[Component]<br/><br/>Manages client<br/>share links"]:::controller

    %% Services
    AuthService["Auth Service<br/>[Component]<br/><br/>JWT handling and<br/>user authentication"]:::service
    TaskService["Task Service<br/>[Component]<br/><br/>Task business logic<br/>and processing"]:::service
    ClientService["Client Service<br/>[Component]<br/><br/>Client management<br/>logic"]:::service
    ProjectService["Project Service<br/>[Component]<br/><br/>Project business<br/>logic"]:::service
    ShareLinkService["Share Link Service<br/>[Component]<br/><br/>Share link generation<br/>and validation"]:::service
    QueueService["Queue Service<br/>[Component]<br/><br/>Task queue<br/>operations"]:::service
    AIProxyService["AI Proxy Service<br/>[Component]<br/><br/>Interface to AI<br/>Service"]:::service

    %% Modules
    AuthModule["Auth Module<br/>[Module]<br/><br/>Authentication and<br/>authorization"]:::module
    TaskModule["Task Module<br/>[Module]<br/><br/>Task management<br/>functionality"]:::module
    ClientModule["Client Module<br/>[Module]<br/><br/>Client relationship<br/>features"]:::module
    ProjectModule["Project Module<br/>[Module]<br/><br/>Project management<br/>features"]:::module

    %% External connections
    Database["Database<br/>[Container]"]:::external
    TaskQueue["Task Queue<br/>[Container]"]:::external
    FileStorage["File Storage<br/>[Container]"]:::external
    AIService["AI Service<br/>[Container]"]:::external

    %% Relationships
    WebApp -->|"HTTPS/JSON"| Gateway

    Gateway -->|"Routes to"| AuthController
    Gateway -->|"Routes to"| TaskController
    Gateway -->|"Routes to"| ClientController
    Gateway -->|"Routes to"| ProjectController
    Gateway -->|"Routes to"| ShareLinkController

    AuthController -->|"Uses"| AuthService
    TaskController -->|"Uses"| TaskService
    ClientController -->|"Uses"| ClientService
    ProjectController -->|"Uses"| ProjectService
    ShareLinkController -->|"Uses"| ShareLinkService

    TaskService -->|"Uses"| QueueService
    TaskService -->|"Uses"| AIProxyService
    ClientService -->|"Uses"| ShareLinkService

    AuthService -->|"Queries"| Database
    TaskService -->|"Queries"| Database
    ClientService -->|"Queries"| Database
    ProjectService -->|"Queries"| Database
    ShareLinkService -->|"Queries"| Database

    QueueService -->|"Sends to"| TaskQueue
    TaskService -->|"Stores files"| FileStorage
    AIProxyService -->|"Calls"| AIService

    %% Module groupings
    subgraph "Auth Module"
        AuthController
        AuthService
    end

    subgraph "Task Module"
        TaskController
        TaskService
        QueueService
    end

    subgraph "Client Module"
        ClientController
        ClientService
        ShareLinkController
        ShareLinkService
    end

    subgraph "Project Module"
        ProjectController
        ProjectService
    end
```

## Legend

| Shape/Color | Meaning                             |
| ----------- | ----------------------------------- |
| Purple      | API Gateway component               |
| Green       | Controller components               |
| Blue        | Service components                  |
| Orange      | Nest.js modules (logical groupings) |
| Gray        | External containers                 |

## Key Elements

### Controllers

- **Auth Controller**: Handles /auth/\* endpoints for login, signup, and token refresh
- **Task Controller**: Manages /tasks/\* endpoints for CRUD operations
- **Client Controller**: Handles /clients/\* endpoints for client management
- **Project Controller**: Manages /projects/\* endpoints
- **Share Link Controller**: Handles /share-links/\* endpoints for client access

### Services

- **Auth Service**: Manages JWT tokens, password hashing, and authentication logic
- **Task Service**: Contains task business logic, validation, and orchestration
- **Client Service**: Handles client data management and communication tracking
- **Project Service**: Manages project lifecycle and relationships
- **Share Link Service**: Generates and validates share links for clients
- **Queue Service**: Interfaces with AWS SQS for async processing
- **AI Proxy Service**: Communicates with the AI Service container

### Modules

- **Auth Module**: Encapsulates authentication functionality
- **Task Module**: Groups task-related components
- **Client Module**: Contains client management components
- **Project Module**: Organizes project functionality

## Key Relationships

1. Gateway → Controllers: All requests routed through controllers
1. Controllers → Services: Business logic separated into services
1. Services → External Containers: Data persistence and external operations
1. Cross-Service Communication: Services can use other services (e.g., TaskService uses QueueService)
1. Module Boundaries: Components grouped by domain

## Notes and Constraints

- All controllers use dependency injection for services
- Guards are applied at controller level for authentication
- Services handle transaction boundaries
- Database access is abstracted through repository pattern
- All external communications go through dedicated services
- Modules enforce separation of concerns

## Related Documentation

- [ADR-009: API Design](../ADRs/ADR-009.md)
- [Container Diagram](./c4-container-diagram.md)
- [Component Diagram - AI Service](./c4-ai-service-component-diagram.md)
