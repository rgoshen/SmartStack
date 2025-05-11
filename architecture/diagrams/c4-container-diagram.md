# Container Diagram: SmartStack

**C4 Level**: 2
**Type**: Container
**Scope**: The SmartStack system internals
**Primary Elements**: Applications, databases, and services within SmartStack
**Intended Audienc**e: Technical stakeholders, developers, DevOps
**Last Updated**: 2025-01-12

## Purpose

This diagram shows the high-level containers (applications and data stores) that make up SmartStack, along with the major technology choices and communication patterns between them.

## Diagram

```mermaid
graph TB
    %% Styling
    classDef webapp fill:#438DD5,stroke:#2E6DA4,stroke-width:2px,color:#fff
    classDef api fill:#1E88E5,stroke:#1565C0,stroke-width:2px,color:#fff
    classDef db fill:#336791,stroke:#275478,stroke-width:2px,color:#fff
    classDef storage fill:#FF9800,stroke:#F57C00,stroke-width:2px,color:#fff
    classDef queue fill:#7B1FA2,stroke:#6A1B9A,stroke-width:2px,color:#fff
    classDef external fill:#999999,stroke:#8a8a8a,stroke-width:2px,color:#fff
    classDef person fill:#08427b,stroke:#073b6f,stroke-width:2px,color:#fff

    %% External actors
    Freelancer["Freelancer<br/>[Person]"]:::person
    Client["Client<br/>[Person]"]:::person
    Admin["Administrator<br/>[Person]"]:::person

    %% Containers
    WebApp["Web Application<br/>[Container: Next.js]<br/><br/>Delivers static content and<br/>handles client-side routing"]:::webapp

    API["API Application<br/>[Container: Nest.js + Lambda]<br/><br/>Provides REST API endpoints<br/>and business logic"]:::api

    AIService["AI Service<br/>[Container: Nest.js + Lambda]<br/><br/>Handles AI processing<br/>and Bedrock integration"]:::api

    TaskQueue["Task Queue<br/>[Container: AWS SQS]<br/><br/>Manages async task<br/>processing queue"]:::queue

    Database["Database<br/>[Container: PostgreSQL/RDS]<br/><br/>Stores user data, tasks,<br/>and client information"]:::db

    FileStorage["File Storage<br/>[Container: S3]<br/><br/>Stores attachments and<br/>AI conversation logs"]:::storage

    %% External Systems
    Bedrock["Amazon Bedrock<br/>[External System]"]:::external
    EmailProvider["Email Provider<br/>[External System]"]:::external

    %% Relationships
    Freelancer -->|"Uses HTTPS"| WebApp
    Client -->|"Uses HTTPS via<br/>share link"| WebApp
    Admin -->|"Uses HTTPS"| WebApp

    WebApp -->|"Makes API calls<br/>[HTTPS/JSON]"| API

    API -->|"Reads/writes<br/>[SQL/TLS]"| Database
    API -->|"Reads/writes<br/>[HTTPS]"| FileStorage
    API -->|"Sends async tasks<br/>[HTTPS/JSON]"| TaskQueue
    API -->|"Calls for AI<br/>[HTTPS/JSON]"| AIService
    API -->|"Sends emails<br/>[SMTP/TLS]"| EmailProvider

    TaskQueue -->|"Triggers processing<br/>[HTTPS/JSON]"| API

    AIService -->|"Processes with AI<br/>[HTTPS/JSON]"| Bedrock
    AIService -->|"Reads/writes context<br/>[SQL/TLS]"| Database
    AIService -->|"Stores logs<br/>[HTTPS]"| FileStorage
```

## Legend

| Shape/Color    | Meaning                   |
| -------------- | ------------------------- |
| Blue (darker)  | Person/User               |
| Blue (medium)  | Web application container |
| Blue (lighter) | API/Service containers    |
| Blue (dark)    | Database                  |
| Orange         | File storage              |
| Purple         | Message queue             |
| Grey           | External systems          |

## Key Elements

### Applications

- **Web Application**: Next.js application serving the user interface, handles routing and client-side logic
- **API Application**: Nest.js application deployed on AWS Lambda, provides REST endpoints and core business logic
- **AI Service**: Separate Nest.js Lambda function for AI operations, interfaces with Amazon Bedrock

### Data Stores

- **Database**: PostgreSQL on AWS RDS storing all structured data (users, tasks, clients, projects)
- **File Storage**: Amazon S3 for storing files, attachments, and AI conversation logs

### Infrastructure

- **Task Queue**: AWS SQS for asynchronous task processing, enabling resilient AI processing

### External Systems

- **Amazon Bedrock**: AI/LLM service for intelligent features
- **Email Provider**: External email service for notifications and task ingestion

## Key Relationships

1. Web App → API: All data operations go through the API (REST/JSON over HTTPS)
1. API → Database: Persistent data storage with encrypted connections
1. API → Task Queue: Asynchronous processing for AI tasks
1. API → AI Service: Dedicated service for AI operations
1. AI Service → Bedrock: External AI processing
1. Both API and AI Service → File Storage: Shared file access

## Notes and Constraints

- All containers are deployed to AWS infrastructure
- API and AI Service run as AWS Lambda functions behind API Gateway
- Database connections use connection pooling for Lambda
- All inter-service communication is encrypted
- Task Queue ensures AI processing doesn't block user operations
- AI Service is separate to allow independent scaling

## Related Documentation

- [ADR-001: Task Processing Architecture](../ADRs/ADR-001.md)
- [ADR-005: AI Integration Architecture](../ADRs/ADR-005.md)
- [ADR-007: Environment & Deployment Architecture](../ADRs/ADR-007.md)
- [System Context Diagram](c4-system-context.md)
- Component Diagram - API
