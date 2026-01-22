# Agency Production Engine (Workflow & Events)

## 1. The Production Pipeline (Kanban)
* **Goal:** managing multi-stage projects (Video/High-End Photo).
* **Interface:** Drag-and-Drop Board.
* **Default Lanes (Customizable):**
    * `Pre-Production` (Scripting, Moodboarding).
    * `Shooting` (Active capture).
    * `Post-Production` (Editing, Color).
    * `Review` (Client Feedback).
    * `Delivery` (Final Output).
* **Automation Hooks:**
    * *Trigger:* Drag Card to "Review".
    * *Action:* Auto-send email to Client: "Your draft is ready for review."

## 2. Multi-Day / Sub-Event Logic
* **Context:** Indian Weddings / Corporate Summits.
* **Structure:**
    * **Parent Project:** "Sharma Wedding" (Holds the Invoice & Contract).
    * **Sub-Events (Children):**
        1.  *Haldi:* Oct 20, 10 AM, Home, Crew: A + B.
        2.  *Sangeet:* Oct 20, 7 PM, Hotel, Crew: C + D + Drone.
        3.  *Wedding:* Oct 21, 6 AM, Temple, Crew: All Hands.
* **Calendar View:** Displays 3 distinct blocks, not one giant 2-day block.
* **Financial View:** One single Invoice for the Parent Project.