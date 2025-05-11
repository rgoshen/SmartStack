# Deployment Diagram: SmartStack

**C4 Level**: 3
**Type**: Deployment
**Scope**: How SmartStack is deployed to AWS infrastructure
**Primary Elements**: AWS services, deployment nodes, and container instances
**Intended Audience**: DevOps engineers, infrastructure team, developers
**Last Updated**: 2025-01-12

## Purpose

This diagram shows how SmartStack containers are deployed to AWS infrastructure across development, staging, and production environments, including the relationships between AWS services.

## Diagram

```mermaid
graph TB
    %% Styling
    classDef node fill:#EC7211,stroke:#CC5200,stroke-width:2px,color:#fff
    classDef container fill:#146EB4,stroke:#0D5295,stroke-width:2px,color:#fff
    classDef db fill:#336791,stroke:#275478,stroke-width:2px,color:#fff
    classDef storage fill:#3F51B5,stroke:#303F9F,stroke-width:2px,color:#fff
    classDef external fill:#999999,stroke:#8a8a8a,stroke-width:2px,color:#fff
    classDef network fill:#4CAF50,stroke:#388E3C,stroke-width:2px,color:#fff

    %% Internet
    Internet["Internet<br/>[External Network]"]:::external

    %% AWS Region
    subgraph AWS_Region["AWS Region (us-east-1)"]

        %% Route 53
        Route53["Route 53<br/>[DNS Service]<br/><br/>smartstack.example.com"]:::network

        %% CloudFront
        CloudFront["CloudFront<br/>[CDN]<br/><br/>Content delivery and<br/>caching"]:::network

        %% API Gateway
        APIGateway["API Gateway<br/>[AWS Service]<br/><br/>REST API endpoints<br/>and throttling"]:::network

        %% VPC
        subgraph VPC["VPC (10.0.0.0/16)"]

            %% Public Subnet
            subgraph PublicSubnet["Public Subnet (10.0.1.0/24)"]
                S3Web["S3 Bucket<br/>[Static Hosting]<br/><br/>Next.js static files"]:::storage
            end

            %% Private Subnet 1
            subgraph PrivateSubnet1["Private Subnet (10.0.2.0/24)"]
                Lambda1["Lambda Function<br/>[Compute]<br/><br/>API Application<br/>(Nest.js)"]:::container
                Lambda2["Lambda Function<br/>[Compute]<br/><br/>AI Service<br/>(Nest.js)"]:::container
            end

            %% Private Subnet 2
            subgraph PrivateSubnet2["Private Subnet (10.0.3.0/24)"]
                RDS["RDS PostgreSQL<br/>[Database]<br/><br/>Primary database<br/>with Multi-AZ"]:::db
            end

            %% Storage Services
            S3Files["S3 Bucket<br/>[Object Storage]<br/><br/>File attachments<br/>and AI logs"]:::storage

            %% Queue Service
            SQS["SQS Queue<br/>[Message Queue]<br/><br/>Task processing<br/>queue"]:::network
        end

        %% External Services
        Bedrock["Amazon Bedrock<br/>[AI Service]<br/><br/>LLM processing"]:::external
        SES["Amazon SES<br/>[Email Service]<br/><br/>Email notifications"]:::external

        %% Secrets and Config
        SecretsManager["Secrets Manager<br/>[AWS Service]<br/><br/>API keys and<br/>credentials"]:::external
        ParameterStore["Parameter Store<br/>[AWS Service]<br/><br/>Configuration<br/>values"]:::external
    end

    %% Relationships
    Internet -->|"HTTPS"| Route53
    Route53 -->|"Routes to"| CloudFront
    Route53 -->|"Routes to"| APIGateway

    CloudFront -->|"Serves static<br/>content"| S3Web
    CloudFront -->|"API requests"| APIGateway

    APIGateway -->|"Invokes"| Lambda1

    Lambda1 -->|"Queries"| RDS
    Lambda1 -->|"Read/Write"| S3Files
    Lambda1 -->|"Sends messages"| SQS
    Lambda1 -->|"Invokes"| Lambda2
    Lambda1 -->|"Sends email"| SES

    Lambda2 -->|"Calls API"| Bedrock
    Lambda2 -->|"Queries"| RDS
    Lambda2 -->|"Stores logs"| S3Files

    SQS -->|"Triggers"| Lambda1

    Lambda1 -->|"Retrieves"| SecretsManager
    Lambda1 -->|"Retrieves"| ParameterStore
    Lambda2 -->|"Retrieves"| SecretsManager
```

## Legend

| Shape/Color | Meaning                          |
| ----------- | -------------------------------- |
| Orange      | AWS infrastructure nodes         |
| Blue        | Application containers/functions |
| Dark Blue   | Database instances               |
| Indigo      | Storage services                 |
| Green       | Network services                 |
| Gray        | External services                |

## Key Elements

### Network Layer

- **Route 53**: DNS management and routing
- **CloudFront**: CDN for static content and API caching
- **API Gateway**: REST API management, throttling, and authentication

### Compute Layer

- **Lambda Functions**: Serverless compute for API and AI services
- **VPC**: Network isolation with public and private subnets

### Storage Layer

- **S3 (Web)**: Static website hosting for Next.�frontend
- **S3 (Files)**: Object storage for attachments and logs
- **RDS PostgreSQL**: Relational database with Multi-AZ for high availability

### Integration Layer

- **SQS**: Message queue for asynchronous task processing
- **Bedrock**: AI/LLM service integration
- **SES**: Email service for notifications

### Security Layer

- **Secrets Manager**: Secure storage for API keys and credentials
- **Parameter Store**: Configuration management
- **VPC**: Network isolation and security groups

## Environment Separation

Each environment (dev, staging, prod) has:

- Separate AWS account or isolated resources
- Independent VPC with same network architecture
- Environment-specific configuration in Parameter Store
- Isolated databases and S3 buckets
- Environment-prefixed resource names

## Key Relationships

1. Internet → CloudFront → S3: Static content delivery path
1. Internet → API Gateway → Lambda: API request path
1. Lambda → RDS: Database operations within VPC
1. Lambda → SQS → Lambda: Asynchronous processing pattern
1. Lambda → Bedrock: External AI service integration

## Notes and Constraints

- Lambda functions are deployed in private subnets for security
- RDS is Multi-AZ for high availability
- All inter-service communication uses IAM roles
- Secrets are never stored in code or environment variables
- CloudFront provides DDoS protection
- API Gateway handles rate limiting

## Related Documentation

- [ADR-007: Environment & Deployment Architecture](../ADRs/ADR-007.md)
- [Container Diagram](c4-container-diagram.md)
