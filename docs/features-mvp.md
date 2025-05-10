# 🧩 SmartStack MVP Features

This file outlines the core features included in the MVP build of SmartStack. These features represent the minimal functionality necessary to deliver value, validate the concept, and support core user flows.

---

## ✅ MVP Feature Set

### 1. 🔐 User Authentication

- Email + password login/signup
- (Optional post-MVP: Google OAuth)
- Session persistence

---

### 2. 📥 Task Ingestion

- Manual task entry via quick-add form
- Email forwarding/tagging with AI parsing
- Basic integrations:
  - Trello
  - Google Sheets (can start as CSV import or webhook stub)

---

### 3. 🧠 AI-Powered Task Parsing

- Categorize by project/client
- Infer due dates
- Assign basic priority (High / Medium / Low)
- Flag unclear tasks as “Needs Review”

---

### 4. 📋 Smart Taskboard UI

- Display all tasks grouped by:
  - Project/client
  - Due date
- Allow user actions per task:
  - ✅ Mark as complete
  - 📝 Edit task
  - ❓ Mark as “Needs Clarification”
- Basic filter and sorting functionality

---

### 5. 🔔 Notifications & Nudges

- Daily digest of:
  - Upcoming tasks
  - Overdue tasks
  - Tasks needing review
  - Client follow-up reminders
- Alert on login
- Toggle reminders on/off

---

### 6. 🗃️ Task & Client Data Persistence

- Store tasks and client info in a user-specific database
- Persist state across sessions
- Enable updates and deletions of tasks and client records

---

### 7. 🧾 Client Communication Tracking

- Add a “Client Note” or “Follow-up” field to tasks
- Track last interaction date per client (auto-updated on task edits)
- Highlight overdue follow-ups via nudge system
- Include comms data in taskboard tooltips or detail views

---

### 8. 🗂️ Client Profiles (Lightweight)

- Create/edit client entries (name, contact info, notes)
- Link tasks to a client
- View all tasks and recent activity per client
- Optional: export client summary (CSV or printable view)

---

### 9. 🤖 Client-Facing AI Assistant (Stub or Live)

- Simple chat interface for clients to ask:
  - “When is my next deliverable?”
  - “What’s the status of Project X?”
- AI answers based on task/project data
- Hosted in standalone page or embedded widget
- Stub with fixed responses OK for MVP validation

---

### 📌 Feature-to-Goal Mapping

| **Feature**                       | **Mapped MVP Goal(s)**                                   |
| --------------------------------- | -------------------------------------------------------- |
| 🔐 User Authentication            | Persistence                                              |
| 📥 Task Ingestion                 | Unified Task Capture                                     |
| 🧠 AI-Powered Task Parsing        | AI-Powered Task Organization                             |
| 📋 Smart Taskboard UI             | Smart Taskboard                                          |
| 🔔 Notifications & Nudges         | Notifications & Nudges, Client Communication Tracking    |
| 🗃️ Task & Client Data Persistence | Persistence, Project Context & Client Profiles           |
| 🧾 Client Communication Tracking  | Client Communication Tracking                            |
| 🗂️ Client Profiles                | Project Context & Client Profiles                        |
| 🤖 Client-Facing AI Assistant     | Client-Facing AI Assistant (Basic), Client Communication |

---

## 🚫 Excluded from MVP (Planned for Later)

- Threaded comments or discussion per task
- AI-initiated smart actions (e.g., “Should we update the client?”)
- Deep integrations with Slack, Asana, Notion, voice, or mobile
- Bulk task operations
- Custom AI prompts or voice interface
- File uploads or document management
- Role-based access (e.g. teams, assistants)
