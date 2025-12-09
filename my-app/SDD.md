# Project Specification Document (SDD)

## 1. Project Overview
- **Project Name:** To Do List (SDD)
- **Purpose / Goal:** This app allows users to create, edit, and track daily tasks efficiently, helping them stay organized and complete tasks on time.
- **Target Users:** People who have trouble managing or completing their tasks on time. 
- **Platform(s):** Web
- **Main Objective:** Allow users to create, view, and complete tasks quickly and reliably.

---

## 2. Features
For each feature, I’ve marked **Must-have** for the essential CRUD operations and completion features.  

- **Feature 1: Create Task**
  - Description: User can add a new task to the list.
  - Must-have / Nice-to-have: Must-have
  - Inputs: Task title (required), optional description
  - Outputs: Task appears in the list and is saved in the database
  - Edge cases / special notes: Title cannot be empty

- **Feature 2: Update Task**
  - Description: User can edit or update task information.
  - Must-have / Nice-to-have: Must-have
  - Inputs: Updated task title or description
  - Outputs: Task updated in the list and database
  - Edge cases / special notes: Cannot update to empty title

- **Feature 3: Read / View Tasks**
  - Description: User can view all tasks in a list format.
  - Must-have / Nice-to-have: Must-have
  - Inputs: N/A
  - Outputs: List of tasks, showing title, completion status, creation date
  - Edge cases / special notes: Empty list should show a message like “No tasks yet”

- **Feature 4: Delete Task**
  - Description: User can delete a task.
  - Must-have / Nice-to-have: Must-have
  - Inputs: Task selected to delete
  - Outputs: Task removed from list and database
  - Edge cases / special notes: Confirm deletion to avoid accidental removal

- **Feature 5: Mark Task Complete / Cross Out**
  - Description: User can mark a task as complete or incomplete without deleting it.
  - Must-have / Nice-to-have: Must-have
  - Inputs: Task selected to toggle completion
  - Outputs: Task visually updated (crossed out or checkbox), status updated in database
  - Edge cases / special notes: N/A

- **Optional Features (Nice-to-Have)**
  - Filter tasks (all / active / completed)  
  - Search tasks by title or description  
  - Set task priority (High / Medium / Low)  
  - Set task due dates  

---

## 3. User Flow
Step-by-step interaction:

1. User opens the app → sees login/signup page  
2. User logs in → redirected to task list  
3. User clicks "Add Task" → enters title → saves → task appears in list  
4. User clicks task → can edit, delete, or mark as complete/incomplete  
5. Optional: User can filter or search tasks  

---

## 4. Data / API
### Data Objects
- **Task**
  - id: integer (unique task identifier)
  - title: string
  - description: string (optional)
  - completed: boolean
  - created_at: datetime
  - updated_at: datetime (optional)

- **User**
  - id: integer
  - username/email: string
  - password: string (hashed)
  - created_at: datetime

### API Endpoints (if applicable)
- `POST /login` → Input: username/password, Output: token/session  
- `POST /signup` → Input: username/password, Output: success/error  
- `GET /tasks` → Input: user token, Output: list of tasks  
- `POST /tasks` → Input: task data, Output: saved task  
- `PUT /tasks/:id` → Input: updated task data, Output: updated task  
- `DELETE /tasks/:id` → Input: task id, Output: confirmation  

---

## 5. Acceptance Criteria
- **Create Task:** Task is added and appears in list; empty title shows error  
- **Update Task:** Task edits are saved correctly; empty title shows error  
- **View Tasks:** All tasks display correctly; empty list shows “No tasks yet”  
- **Delete Task:** Task removed from list/database; confirmation required  
- **Mark Complete:** Task completion toggles correctly, visual feedback is clear  

---

## 6. Constraints
- Technology stack: React (frontend) + Node.js / Express (backend) + SQLite (database)  
- Performance: App loads in under 2 seconds  
- UI/UX: Must be mobile responsive  
- Security/Privacy: Passwords hashed, no plain text storage  
- Other constraints: Single-user database (optional multi-user for future enhancement)  

---

## 7. Folder / Project Structure
with-sdd/
├─ src/
│ ├─ components/ # reusable UI components
│ ├─ pages/ # pages like login, task list
│ ├─ api/ # functions to call backend APIs
│ └─ utils/ # helper functions
├─ tests/ # unit and integration tests
├─ SDD.md # this spec document
├─ README.md
└─ package.json


---

## 8. Notes / Additional Information
- Start with core CRUD features first, then add optional features later  
- Keep UI simple and user-friendly  
- All features must be **testable and match acceptance criteria**  
- Document any additional decisions during development  

---

### **Explanation of Each Section (for next time)**

1. **Project Overview:** Explain why the app exists, who uses it, and the main objective. Keep it short and focused.  
2. **Features:** List every user action as a feature. Decide if it’s must-have or optional. Include inputs, outputs, and edge cases.  
3. **User Flow:** Step-by-step explanation of how a user interacts with the app. Helps you plan the UI and coding order.  
4. **Data / API:** List all objects, fields, and endpoints. This makes backend and frontend communication clear.  
5. **Acceptance Criteria:** Define how you’ll test each feature. Makes QA and coding easier.  
6. **Constraints:** Technical limits, design rules, performance goals, security.  
7. **Folder / Project Structure:** Suggest how to organize files. Helps developers follow a consistent structure.  
8. **Notes / Additional Information:** Anything else to guide development.  