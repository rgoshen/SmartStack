# 🧱 SmartStack – High-Level Architecture Overview

## 📌 Purpose

This document outlines the high-level system architecture for **SmartStack**, a client-centric task and communication management tool enhanced by AI.

The goal is to support a modular, scalable MVP using serverless infrastructure and modern frontend/backend frameworks—prioritizing speed to market and long-term maintainability.

---

## ⚙️ Tech Stack

| Layer         | Choice        | Notes |
|---------------|---------------|-------|
| Frontend      | Next.js       | React-based, SEO-friendly, supports SSR/SSG |
| Backend       | Nest.js       | TypeScript-based, modular API with REST endpoints |
| AI Integration| AWS Lambda + Amazon Bedrock | Handles AI assistant tasks |
| Database      | Amazon RDS (PostgreSQL) | Structured data for users, tasks, comms |
| File Storage  | Amazon S3     | Used for client uploads, AI transcripts |
| Hosting       | AWS (Lambda, API Gateway, S3, CloudFront) | Fully serverless for MVP |
| Auth          | JWT           | Managed in Nest with guards and decorators |
| IaC           | OpenTofu      | Used for all infrastructure (S3, CF, RDS, Lambdas) |

---

### 🔍 Why These Technologies?

#### Frontend: Next.js

Next.js was chosen first and foremost because I wanted to learn it through hands-on, project-based experience. It's one of the fastest-growing frameworks in the React ecosystem and widely used in modern full-stack development.

Beyond personal growth, Next.js offers a strong balance of developer experience, performance, and flexibility. Since SmartStack is a user-facing tool that may grow to include SEO-relevant content (like public landing pages or client portals), Next.js provides static site generation (SSG), server-side rendering (SSR), and client-side routing—all within a unified React-based framework. Its built-in API routes and TypeScript support also make it a powerful and scalable choice.

#### Backend: Nest.js

Nest.js was chosen because it uses TypeScript just like the frontend. I prefer TypeScript because it adds strong typing to JavaScript, which helps reduce bugs, catch issues earlier, and improve developer confidence—especially as a codebase grows.

In addition to being a good personal fit, Nest.js also provides a highly modular and scalable structure for backend development. It follows a convention-over-configuration approach and includes built-in support for dependency injection, guards, interceptors, and decorators. These patterns make it easier to build maintainable, testable APIs.

Because SmartStack includes multiple functional areas (auth, tasks, clients, AI proxying), Nest’s module system is a great match for organizing and separating responsibilities cleanly from the start.

#### Cloud Platform: AWS

AWS was selected because it is the industry standard for cloud infrastructure and offers a wide range of managed services that align perfectly with SmartStack's architecture—such as Lambda for serverless compute, RDS for managed PostgreSQL, S3 for object storage, and Bedrock for AI model integration.

Beyond the technical fit, I also wanted to grow stronger with AWS through project-based learning. Working hands-on with real services like IAM, CloudFront, API Gateway, and OpenTofu will help me build the kind of confidence that only comes from doing. This project is a chance to go deep on cloud infrastructure while still focusing on delivering a usable product.

#### Infrastructure as Code: OpenTofu

I chose OpenTofu because I want to improve my skills in Infrastructure as Code (IaC) and build confidence managing infrastructure in a repeatable, version-controlled way. OpenTofu is open source, community-driven, and fully compatible with Terraform, which is widely used across the industry.

Since this project will involve provisioning multiple environments (testing, staging, production) and managing cloud resources like S3, RDS, Lambda, and CloudFront, using OpenTofu ensures that infrastructure can be automated, consistent, and tracked through Git. It also aligns with modern DevOps practices I want to continue developing.

#### Environment Strategy: Test → Staging → Production

I intentionally chose a multi-environment deployment strategy to reflect the kind of real-world project lifecycle I’ve seen work best in industry settings. I've been on projects that used this flow—and some that didn’t—and I definitely prefer the clarity and control it brings.

Having distinct environments for testing, staging, and production allows me to simulate a professional release process while minimizing the risk of bugs reaching users. It also gives me the opportunity to practice deployment automation and environment management with OpenTofu and CI/CD tools. This setup supports safe iteration, better QA, and the flexibility to validate infrastructure and code changes before pushing them live.

---

## 🧩 Component Overview

### ✅ Frontend (Next.js)
- Hosts the user interface (dashboard, tasks, client chat)
- Sends API requests to the backend
- Displays AI assistant responses

### ✅ Backend (Nest.js)
- Organized by domain modules (auth, tasks, clients, ai)
- Exposes REST endpoints via API Gateway
- Proxies AI requests to Bedrock
- Handles DB persistence

### ✅ AI Layer
- AWS Lambda invokes Amazon Bedrock (e.g., Anthropic or Cohere model)
- Builds prompts using task and comm history
- Returns AI responses for display in frontend

### ✅ Storage & Persistence
- **PostgreSQL (RDS)** for structured app data
- **S3** for file attachments, chat transcripts, prompt logs

---

## 🖼 System Diagram (Mermaid)

```mermaid
graph TD
  A[Next.js Frontend] -->|HTTPS| B[Nest.js Backend (API Gateway)]
  B --> C[Auth Module]
  B --> D[Task Manager Module]
  B --> E[Client Comms Module]
  B --> F[AI Assistant Proxy]
  F --> G[Lambda: Call Amazon Bedrock]
  G --> H[Bedrock (LLM Models)]

  B --> I[(RDS PostgreSQL)]
  B --> J[(S3 Bucket)]

  subgraph AWS Cloud
    B
    G
    I
    J
  end
```

---

## 🚀 Deployment Strategy

- CI/CD via GitHub Actions
- Two workflows:
  - `pr-checks.yml` (on PR): runs tests, lint, Sourcery
  - `deploy.yml` (on main): builds + deploys frontend/backend, applies OpenTofu
- Frontend deployed to S3 + CloudFront
- Backend deployed via AWS Lambda + API Gateway

---

## 🌍 Environment Strategy

SmartStack follows a clean separation of environments to ensure quality, safety, and iterative feedback:

| Environment | Purpose |
|-------------|---------|
| **Testing** | CI-only environment that runs unit and integration tests via GitHub Actions. May use mocks or ephemeral AWS resources. |
| **Staging** | Fully deployed environment that mirrors production. Used for final testing and QA before release. |
| **Production** | Live environment used by real users. Only stable, approved code is promoted here. |

Environments are provisioned using **OpenTofu**, with separate `*.tfvars` files and backend configs per environment.

Each environment has:
- Its own **RDS database**
- Its own **S3 buckets**
- Isolated **API endpoints**
- Independent **Bedrock/Lambda permissions** (if needed)

Supports a safe promotion pipeline:  
**Test → Staging → Production**

---

## 🔐 Security

- JWT-based user auth (via `@nestjs/jwt`)
- Basic CORS setup in API Gateway
- Input validation using Nest pipes + DTOs
- Optional: rate limiting, AI prompt logging for review

---

## 📈 Scalability Plan

SmartStack starts as a modular monolith using AWS Lambda, but is structured to evolve:

- The AI Assistant can be separated into a microservice (e.g., Python + FastAPI)
- Backend modules can split out over time into services
- Event-driven workflows can be introduced with EventBridge or SQS

---

## 📂 Codebase Structure

```
smartstack/
├── frontend/         # Next.js app
├── backend/          # Nest.js app (REST API)
├── infra/            # OpenTofu config: S3, CF, RDS, etc.
│   ├── main.tf
│   ├── variables.tf
│   ├── environments/
│   │   ├── prod.tfvars
│   │   ├── staging.tfvars
│   │   └── test.tfvars
├── .github/
│   └── workflows/
│       ├── pr-checks.yml
│       └── deploy.yml
├── architecture/
│   └── high-level-overview.md
└── product/
    └── backlog.md
```

---

## ✅ Summary

This document defines the full technical architecture for SmartStack’s MVP—balancing clarity, speed, modularity, and future-proofing.

You're ready to build.