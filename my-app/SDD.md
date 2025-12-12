# To-Do List (SDD)

## 1. Project Overview & Scope

**Project Name:** To-Do List (SDD)
**Purpose / Goal:** Provide a reliable web application enabling users to efficiently create, view, manage, and track daily tasks.
**Target Users:** Individuals seeking organization and task management assistance.
**Platform(s):** Web (mobile responsive UI required)
**Core Objective:** Implement all Must-Have features detailed below, focusing on robust functionality before optional features.

---

## 2. Data Models & API Endpoints

The API will use JSON for all communication. All requests require authentication (handled by JWT or sessions).

### 2.1 Data Objects

**Task**

| Field Name  | Type     | Constraints             | Description                   |
| ----------- | -------- | ----------------------- | ----------------------------- |
| id          | Integer  | PK, Auto-Inc            | Unique task identifier        |
| title       | String   | NOT NULL, < 255 chars   | Task summary (required input) |
| description | String   | NULL                    | Task details (optional)       |
| completed   | Boolean  | NOT NULL, Default false | Task status                   |
| created_at  | Datetime | NOT NULL                | Creation timestamp            |
| updated_at  | Datetime | NULL                    | Last update timestamp         |

**User**

| Field Name | Type    | Constraints      | Description                      |
| ---------- | ------- | ---------------- | -------------------------------- |
| id         | Integer | PK, Auto-Inc     | Unique user identifier           |
| username   | String  | NOT NULL, Unique | User login name (email/username) |
| password   | String  | NOT NULL         | Hashed password                  |

### 2.2 API Endpoints

| Endpoint   | Method | Purpose                 | Authentication |
| ---------- | ------ | ----------------------- | -------------- |
| /login     | POST   | Authenticate user       | None           |
| /signup    | POST   | Create new user         | None           |
| /tasks     | GET    | Retrieve all user tasks | Required       |
| /tasks     | POST   | Create a new task       | Required       |
| /tasks/:id | PUT    | Update a specific task  | Required       |
| /tasks/:id | DELETE | Delete a specific task  | Required       |

---

## 3. Functional Requirements (User Flow & Acceptance Criteria)

All must-have features are defined below using a BDD style. These criteria must be implemented and tested using React (Frontend) + Node.js/Express (Backend) + SQLite (Database).

### A. Authentication & User Flow

* **AC 3.1 (User Flow):** User opens app, sees login/signup page. Upon successful login, redirected to main task list page (`/tasks`).
* **AC 3.2 (Security):** Passwords must be hashed (e.g., bcrypt). Plain text passwords must never be stored.

### B. Feature 1: Create Task (`POST /tasks`)

| Scenario      | Given                                    | When               | Then                                                                            | Status Code     |
| ------------- | ---------------------------------------- | ------------------ | ------------------------------------------------------------------------------- | --------------- |
| Success       | User authenticated; valid title provided | POST /tasks called | Task created in DB (`completed`: false); returns created task object in UI list | 201 Created     |
| Missing Title | Request body lacks title                 | POST /tasks called | Task creation prevented; UI shows error message "Title cannot be empty"         | 400 Bad Request |

### C. Feature 2 & 5: Update Task / Mark Complete (`PUT /tasks/:id`)

| Scenario       | Given                                           | When                  | Then                                                                           | Status Code     |
| -------------- | ----------------------------------------------- | --------------------- | ------------------------------------------------------------------------------ | --------------- |
| Update Success | Task :id exists; user sends valid updates       | PUT /tasks/:id called | Task data updated in DB; UI updates visually; returns updated task object      | 200 OK          |
| Mark Complete  | Task :id exists; completed status toggled in UI | PUT /tasks/:id called | `completed` status toggled in DB; task visually updated (crossed out/checkbox) | 200 OK          |
| Not Found      | Task :id does not exist                         | PUT /tasks/:id called | Returns error message in UI/API                                                | 404 Not Found   |
| Empty Title    | User updates title to empty string              | PUT /tasks/:id called | Update prevented; UI shows error message "Title cannot be empty"               | 400 Bad Request |

### D. Feature 3: Read/View Tasks (`GET /tasks`)

| Scenario    | Given                            | When              | Then                                                                 | Status Code |
| ----------- | -------------------------------- | ----------------- | -------------------------------------------------------------------- | ----------- |
| Tasks Exist | User authenticated; DB has tasks | GET /tasks called | UI displays list of tasks (title, status, date); sorted newest first | 200 OK      |
| Empty List  | User authenticated; DB empty     | GET /tasks called | UI displays message: “No tasks yet”                                  | 200 OK      |

### E. Feature 4: Delete Task (`DELETE /tasks/:id`)

| Scenario     | Given                        | When                                           | Then                                                                 | Status Code    |
| ------------ | ---------------------------- | ---------------------------------------------- | -------------------------------------------------------------------- | -------------- |
| Success      | Task :id exists              | DELETE /tasks/:id called after UI confirmation | Task permanently removed from DB and UI list                         | 204 No Content |
| Confirmation | User attempts deletion in UI | Confirmation dialog shown                      | User must confirm deletion to proceed (prevents accidental deletion) | N/A (UI Req)   |

---

## 4. Constraints & Folder Structure

* **Tech Stack:** React (frontend) + Node.js / Express (backend) + SQLite (database)
* **Performance:** App loads and API endpoints respond efficiently (target sub 2s load time)
* **UI/UX:** Mobile responsive and user-friendly

### Folder Structure

```
with-sdd/
├─ src/                  # Source code (frontend/react specific structure)
│ ├─ components/         # Reusable UI components
│ ├─ pages/              # Pages like login, task list
│ ├─ api/                # Functions to call backend APIs
│ └─ utils/              # Helper functions
├─ tests/                # Unit and integration tests (must cover all ACs)
├─ backend/              # Node/Express/SQLite implementation
├─ package.json          # For frontend dependencies
├─ backend/package.json  # For backend dependencies
└─ README.md
```
