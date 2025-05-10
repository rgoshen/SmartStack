# 🎯 SmartStack MVP Goals

This document outlines the updated goals for the SmartStack Minimum Viable Product (MVP). These goals guide development and ensure the MVP delivers real user value with the smallest usable scope.

---

## ✅ MVP Objective

> Help freelance developers **stay on top of client work** by capturing tasks in one place, organizing project context, and enabling smooth communication—with AI assisting both the developer and their clients.

---

## 🔍 Core MVP Goals

### 1. **Unified Task Capture**

- Users can input tasks manually
- Forward tasks from email
- Connect to Trello or Google Sheets (light integration or stub)

### 2. **AI-Powered Task Organization**

- Group tasks by project or client
- Infer and assign due dates
- Assign priority level (basic: High, Medium, Low)
- Flag tasks that are unclear or need user review

### 3. **Smart Taskboard**

- Central view of all tasks
- Filter/sort by project, due date, priority
- Users can edit, complete, or mark tasks as “Needs Clarification”

### 4. **Client Communication Tracking**

- Each task may include client-facing notes or follow-up reminders
- System tracks last interaction date per client
- Users can view recent touchpoints and overdue follow-ups
- Daily nudges include comms reminders (e.g. "No contact with Client X in 10 days")

### 5. **Project Context & Client Profiles**

- View all tasks grouped under each client
- Lightweight “Client Profile” page:
  - Name, email/contact
  - Linked tasks
  - Notes field
- Add/edit client info directly in UI

### 6. **Client-Facing AI Assistant (Basic)**

- Clients can ask the AI assistant questions (e.g. “When’s my next deliverable?”)
- AI pulls from task/project metadata
- Hosted on a separate public-facing widget or portal (stub if needed for MVP)

### 7. **Notifications & Nudges**

- Daily digest of:
  - Upcoming tasks
  - Overdue tasks
  - Tasks needing review
  - Comms nudges (e.g. “No update sent to Client Z this week”)
- Alert on login
- Optional notification settings

### 8. **Persistence**

- Tasks and client data saved and linked to user account
- State persists across sessions
- Enable task and client info updates and deletion

---

## 📈 MVP Success Metrics

These are the minimum signals we’ll use to determine whether the MVP is delivering value and ready to expand.

| Area                    | Metric                                                                | Target |
| ----------------------- | --------------------------------------------------------------------- | ------ |
| **Adoption**            | First-time users who complete onboarding and create at least one task | ≥ 60%  |
| **Engagement**          | Users who return within 7 days of first login                         | ≥ 40%  |
| **Task Value**          | % of tasks that are reviewed/acted on within 24 hours                 | ≥ 70%  |
| **AI Effectiveness**    | % of AI-suggested priorities/dates accepted by user                   | ≥ 50%  |
| **Comms Visibility**    | % of clients with at least one recorded comms note                    | ≥ 80%  |
| **Client AI Use**       | Clients who ask at least one question to the AI assistant             | ≥ 25%  |
| **Retention (Month 1)** | Users who log in weekly in the first month                            | ≥ 30%  |

---

## ❌ Not in MVP (Saved for Post-Launch)

- Threaded discussions per task
- AI-initiated smart actions (e.g., "Should we update the client?")
- Slack/Asana/voice/mobile app integrations
- Customizable workflows or tags
- Bulk task operations
- Document uploads or advanced file sharing
