# 🗂️ SmartStack Product Backlog

This is the evolving backlog for SmartStack. It tracks user stories, grouped by epics and prioritized into development phases.

Use checkboxes to track progress and reflect weekly to adjust priorities.

---

## 🧭 Project Phases

- **Phase 1**: Core MVP (tasks, client communication, AI assistant)
- **Phase 2**: User auth & onboarding
- **Phase 3**: Client-facing AI portal
- **Phase 4**: Polishing, deployment, feedback loop

---

## 🧱 Epic: Task Management

### User Stories
- [ ] As a user, I can create a new task for a client with a title and description.
- [ ] As a user, I can view a list of all my tasks.
- [ ] As a user, I can update a task’s status (e.g. “in progress,” “done”).
- [ ] As a user, I can delete a task I no longer need.
- [ ] As a user, I can filter tasks by client or status.

---

## 💬 Epic: Client Communication Tracker

### User Stories
- [ ] As a user, I can log a conversation I had with a client.
- [ ] As a user, I can view a history of all communications per client.
- [ ] As a user, I can tag a communication with a purpose or topic.
- [ ] As a user, I can edit or remove a logged conversation.

---

## 🤖 Epic: AI Assistant

### User Stories
- [ ] As a user, I can ask the AI to summarize recent conversations with a client.
- [ ] As a user, I can ask the AI what the next steps are for a client.
- [ ] As a user, I can submit a question to the AI assistant on behalf of a client.
- [ ] As a user, I can view the AI's response in a readable, chat-like format.

---

## 👤 Epic: Authentication & User Management

### User Stories
- [ ] As a new user, I can sign up with email and password.
- [ ] As a returning user, I can log in securely and stay logged in.
- [ ] As a user, I can log out from the app.
- [ ] As a user, I can view and edit my profile information.

---

## 🚀 Epic: Infrastructure & Deployment

### Tasks
- [ ] Set up OpenTofu project structure with base and env-specific configs
- [ ] Create S3 bucket + CloudFront + Route 53 setup
- [ ] Create GitHub Actions for PR checks (tests, lint, Sourcery)
- [ ] Create GitHub Actions for main branch deploy (frontend, backend, infra)
- [ ] Create RDS PostgreSQL config and provision via OpenTofu
- [ ] Define secrets management via SSM Parameter Store

---

## 🧪 Epic: Dev Experience & Testing

### Tasks
- [ ] Add unit test scaffolding to Nest backend
- [ ] Add linting and formatting (e.g. ESLint, Prettier)
- [ ] Add type-checking and build validation to GitHub Actions
- [ ] Create test database for local/staging use
- [ ] Add initial integration test for task creation

---

## 📥 Icebox (Future Ideas)

- [ ] Email summaries of weekly client activity
- [ ] Auto-tag communications using NLP
- [ ] Integrate with Google Calendar or Outlook
- [ ] Assign tasks to multiple team members (future multi-user feature)

---

Track progress here, reflect often, and iterate with purpose. You’re building both product and skill—one slice at a time.