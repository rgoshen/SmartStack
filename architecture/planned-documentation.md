# Planned Documentation Tracker

**Purpose**: Track documentation that has been referenced but not yet created
**Last Updated**: 2025-01-12

## Documentation Debt

This file tracks all documentation that has been referenced in existing documents but hasn't been created yet. This helps us maintain documentation integrity and avoid broken links.

### Priority Levels

- 🔴 **High**: Critical for understanding the system
- 🟡 **Medium**: Helpful but not blocking
- 🟢 **Low**: Nice to have, can be created as needed

## Pending Documentation

### Data Flow Diagrams

| Document                                   | Referenced In                | Priority | Description                                      |
| ------------------------------------------ | ---------------------------- | -------- | ------------------------------------------------ |
| `diagrams/data-flow/ai-processing.md`      | AI Service Component Diagram | 🔴       | Shows how AI requests flow through the system    |
| `diagrams/data-flow/task-processing.md`    | Multiple ADRs                | 🔴       | Shows task lifecycle from creation to completion |
| `diagrams/data-flow/auth-flow.md`          | -                            | 🟡       | Authentication and authorization flow            |
| `diagrams/data-flow/client-access-flow.md` | -                            | 🟡       | How clients access via share links               |

### Infrastructure Documentation

| Document                                | Referenced In      | Priority | Description                            |
| --------------------------------------- | ------------------ | -------- | -------------------------------------- |
| `infrastructure/README.md`              | Deployment Diagram | 🔴       | OpenTofu setup and organization        |
| `infrastructure/modules/README.md`      | -                  | 🟡       | Documentation for each OpenTofu module |
| `infrastructure/environments/README.md` | -                  | 🟡       | Environment-specific configurations    |

### Deployment Documentation

| Document                    | Referenced In      | Priority | Description                         |
| --------------------------- | ------------------ | -------- | ----------------------------------- |
| `deployment/ci-cd.md`       | Deployment Diagram | 🔴       | CI/CD pipeline documentation        |
| `deployment/local-setup.md` | -                  | 🟡       | Local development environment setup |
| `deployment/aws-setup.md`   | -                  | 🟡       | AWS account and initial setup       |

### AI Documentation

| Document                   | Referenced In                | Priority | Description                          |
| -------------------------- | ---------------------------- | -------- | ------------------------------------ |
| `ai/prompt-templates.md`   | AI Service Component Diagram | 🟡       | Prompt engineering templates         |
| `ai/model-selection.md`    | -                            | 🟢       | Guide for choosing AI models         |
| `ai/context-management.md` | -                            | 🟢       | How context is built for AI requests |

### API Documentation

| Document                 | Referenced In         | Priority | Description                          |
| ------------------------ | --------------------- | -------- | ------------------------------------ |
| `api/openapi.yaml`       | API Component Diagram | 🟢       | Auto-generated OpenAPI specification |
| `api/examples/README.md` | -                     | 🟢       | API usage examples                   |

### Database Documentation

| Document                        | Referenced In | Priority | Description                 |
| ------------------------------- | ------------- | -------- | --------------------------- |
| `database/erd.md`               | -             | 🔴       | Entity Relationship Diagram |
| `database/migrations/README.md` | -             | 🟡       | Database migration strategy |

## Guidelines for Creating Documentation

1. **Update this tracker** when creating new documentation
2. **Remove entries** when documentation is completed
3. **Add entries** when referencing new documents
4. **Review monthly** to prioritize documentation tasks

## Next Documentation to Create

Based on priority and dependencies:

1. Entity Relationship Diagram (`database/erd.md`)
2. Task Processing Flow (`diagrams/data-flow/task-processing.md`)
3. AI Processing Flow (`diagrams/data-flow/ai-processing.md`)
4. OpenTofu README (`infrastructure/README.md`)
5. CI/CD Pipeline (`deployment/ci-cd.md`)
