# 🧭 SmartStack User Flows

This file documents the high-level user flows for the initial SmartStack MVP. These flows visualize the main journey a user takes to interact with the product and accomplish meaningful outcomes.

---

## 🔐 0. User Authentication

### Goal:

Let users securely access their SmartStack workspace.

### Steps:

1. User visits SmartStack login page
2. Logs in with email + password (or Google OAuth if available)
3. Redirected to their SmartStack dashboard

---

## 📥 1. Task Ingestion Flow

### Goal:

Capture tasks from various sources and unify them into a single system.

### Input Options:

- Manual task entry via a quick add form
- Forward or tag an email (for AI parsing)
- Connect external tool (Trello, Google Sheets)

### Steps:

1. User enters or sends a task through any supported method
2. Task is captured and stored in the user’s SmartStack workspace
3. AI service is triggered to process task contents

---

## 🧠 2. AI-Powered Task Parsing Flow

### Goal:

Automatically organize tasks with minimal manual input.

### Steps:

1. AI analyzes task content
2. Assigns project/client based on text
3. Suggests or sets:
   - Due date
   - Priority (High, Medium, Low)
4. Flags unclear tasks as “Needs Review”

---

## 📋 3. Smart Taskboard Review Flow

### Goal:

Give users visibility and control over their tasks.

### Steps:

1. User opens the Taskboard
2. Views tasks grouped by:
   - Project/client
   - Due date
   - Status
3. Can take actions per task:
   - Edit task
   - Mark complete
   - Mark as “Needs Clarification”
4. Can sort or filter by due date, project, or priority

---

## 🔔 4. Notifications & Nudges Flow

### Goal:

Keep users aware of what matters without overwhelming them.

### Steps:

1. SmartStack checks for:
   - Tasks due today
   - Unreviewed/flagged tasks
   - Clients with no recent communication
2. System sends:
   - Daily digest email (optional)
   - Reminder alert on login
3. Nudges may include:
   - “You have 3 tasks due today”
   - “2 tasks are flagged as unclear – want to review them?”
   - “No follow-up logged for Client X in 10 days”

---

## 🔁 5. Continuous Use Loop

### Goal:

Create a simple daily cycle of capture, review, and follow-through.

### Typical Day:

1. Log in
2. Check daily summary
3. Add new tasks via quick entry or email
4. Review Smart Taskboard
5. Update or follow up on client comms
6. Act on top priorities or flagged items
7. Repeat the next day

---

## 🧾 6. Client Communication & Profile Flow

### Goal:

Track project context and client interactions without leaving the workspace.

### Steps:

1. User creates a new client profile (name, contact info, notes)
2. Links tasks to the appropriate client
3. Adds client-facing notes or follow-up reminders to tasks
4. SmartStack logs last interaction date per client
5. User views a “Client Profile” with:
   - Basic info
   - Linked tasks
   - Communication history and notes

---

## 🤖 7. Client-Facing AI Assistant Flow

### Goal:

Let clients self-serve simple project questions without needing to contact the freelancer directly.

### Steps:

1. Client accesses SmartStack's AI assistant via a shared link or widget
2. Enters a natural language question (e.g., “When is my next deliverable?”)
3. AI uses task metadata to generate a response
4. Client sees answer in the interface
5. (Optional for MVP) Logs question + response for user visibility
