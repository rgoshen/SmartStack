# Component Diagram: AI Service

**C4 Level**: 3
**Type**: Component
**Scope**: Internal structure of the AI Service container
**Primary Elements**: Components within the AI Service for processing AI requests
**Intended Audience**: Developers, AI/ML engineers
**Last Updated**: 2025-05-11

## Purpose

This diagram shows the internal component structure of the AI Service, illustrating how different AI capabilities are organized and how they interact with Amazon Bedrock and other system components.

## Diagram

```mermaid
graph TB
    %% Styling
    classDef controller fill:#4CAF50,stroke:#43A047,stroke-width:2px,color:#fff
    classDef service fill:#2196F3,stroke:#1976D2,stroke-width:2px,color:#fff
    classDef processor fill:#673AB7,stroke:#5E35B1,stroke-width:2px,color:#fff
    classDef external fill:#999999,stroke:#8a8a8a,stroke-width:2px,color:#fff
    classDef context fill:#FF5722,stroke:#F4511E,stroke-width:2px,color:#fff

    %% External actors
    APIApp["API Application<br/>[Container]"]:::external
    Bedrock["Amazon Bedrock<br/>[External System]"]:::external
    Database["Database<br/>[Container]"]:::external
    FileStorage["File Storage<br/>[Container]"]:::external

    %% Controllers
    AIController["AI Controller<br/>[Component]<br/><br/>Handles AI processing<br/>requests"]:::controller

    %% Core Services
    TaskParsingService["Task Parsing Service<br/>[Component]<br/><br/>Extracts structure from<br/>raw task text"]:::service
    PrioritySuggestionService["Priority Suggestion Service<br/>[Component]<br/><br/>Suggests due dates<br/>and priorities"]:::service
    ClientAssistantService["Client Assistant Service<br/>[Component]<br/><br/>Handles client Q&A<br/>interactions"]:::service

    %% Supporting Services
    ContextService["Context Service<br/>[Component]<br/><br/>Retrieves relevant context<br/>for AI processing"]:::context
    PromptService["Prompt Service<br/>[Component]<br/><br/>Manages prompt templates<br/>and construction"]:::service
    BedrockService["Bedrock Service<br/>[Component]<br/><br/>Interface to Amazon<br/>Bedrock API"]:::service

    %% Processors
    TaskProcessor["Task Processor<br/>[Component]<br/><br/>Orchestrates task<br/>AI processing"]:::processor
    ClientQueryProcessor["Client Query Processor<br/>[Component]<br/><br/>Processes client<br/>questions"]:::processor

    %% Relationships
    APIApp -->|"HTTP/JSON"| AIController

    AIController -->|"Routes to"| TaskProcessor
    AIController -->|"Routes to"| ClientQueryProcessor

    TaskProcessor -->|"Uses"| TaskParsingService
    TaskProcessor -->|"Uses"| PrioritySuggestionService
    TaskProcessor -->|"Uses"| ContextService

    ClientQueryProcessor -->|"Uses"| ClientAssistantService
    ClientQueryProcessor -->|"Uses"| ContextService

    TaskParsingService -->|"Uses"| PromptService
    PrioritySuggestionService -->|"Uses"| PromptService
    ClientAssistantService -->|"Uses"| PromptService

    PromptService -->|"Uses"| BedrockService

    BedrockService -->|"Calls API"| Bedrock

    ContextService -->|"Queries"| Database
    ContextService -->|"Retrieves"| FileStorage

    TaskProcessor -->|"Stores results"| Database
    ClientQueryProcessor -->|"Logs interactions"| FileStorage
```

## Legend

| Shape/Color | Meaning                           |
| ----------- | --------------------------------- |
| Green       | Controller components             |
| Blue        | Service components                |
| Purple      | Processor/Orchestrator components |
| Orange      | Context management components     |
| Gray        | External containers/systems       |

## Key Elements

### Controllers

- **AI Controller**: Single entry point for all AI processing requests from the API Application

### Core Services

- **Task Parsing Service**: Extracts structured information (client, project, dates) from unstructured text
- **Priority Suggestion Service**: Analyzes tasks to suggest priorities and due dates
- **Client Assistant Service**: Handles natural language Q&A for client inquiries

### Supporting Services

- **Context Service**: Retrieves relevant context (client history, project details) for AI processing
- **Prompt Service**: Manages prompt templates and constructs prompts with injected context
- **Bedrock Service**: Wraps Amazon Bedrock API calls, handles retries and error handling

### Processors

- **Task Processor**: Orchestrates the complete task AI processing workflow
- **Client Query Processor**: Manages the client Q&A workflow with appropriate context

## Key Relationships

1. API App → AI Controller: All AI requests come through single controller
1. Controller → Processors: Routes to appropriate processor based on request type
1. Processors → Services: Orchestrate multiple services for complete workflows
1. Services → Prompt Service: All AI services use centralized prompt management
1. Prompt Service → Bedrock: Single point of integration with Amazon Bedrock
1. Context Service → Storage: Retrieves context from both database and files

## Notes and Constraints

- Each AI service is optimized for different model characteristics
- Prompt templates are version controlled and environment-specific
- Context window limits are managed by the Prompt Service
- All AI interactions are logged for auditing and improvement
- Processors handle retry logic and fallback strategies
- Results are cached where appropriate to reduce costs

## Related Documentation

- [ADR-005: AI Integration Architecture](../ADRs/ADR-005.md)
- [Container Diagram](./c4-container-diagram.md)
