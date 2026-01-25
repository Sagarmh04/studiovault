# Micro-Task Management (Checklists)

## 1. Context
* **Problem:** A Kanban status like "Post-Production" is too vague. It involves 10 small steps (Backup, Culling, Color, Export, Upload).
* **Goal:** Granular tracking of "Who is doing what" inside a Project.

## 2. Checklists & Templates
* **Feature:** **Task Templates.**
* **Workflow:**
    * Admin creates a Master Template: "Wedding Workflow" (contains 20 items).
    * When a Project is created, Manager applies the template.
    * Result: 20 Checkboxes appear in the "Tasks" tab of the Project.

## 3. Assignment & Due Dates
* **Granularity:** Each checkbox can be assigned to a specific staff member.
* **Example:**
    * `[ ] Copy Cards to NAS` -> Assigned to: *Intern* (Due: Today).
    * `[ ] Select Top 50` -> Assigned to: *Lead Shooter* (Due: Tomorrow).
* **My Tasks View:** Staff members see a personal "To-Do List" aggregated from all active projects.

## 4. Automation Hooks
* **Logic:** Completing a checklist group can trigger a Status Change.
* **Rule:** `IF (All "Editing" tasks == Complete) -> Auto-move Project Status to "Ready for Review".`