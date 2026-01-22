# Enterprise Production Workflow (Video & Post)

## 1. Context & Goal
* **Goal:** Solve the "Iterative Nightmare" of video projects (Drafts, Revisions, Final Cut).
* **The Shift:** Unlike Photos (which are "Select & Deliver"), Video requires "Review & Refine".
* **Architecture:** Integrated Video Player with time-stamped commenting.

## 2. The "Version Stack" (File Management)
* **Concept:** Instead of cluttering the folder with `Wedding_Final_FINAL_v3.mp4`, we use **Stacks**.
* **Behavior:**
    * User uploads `Draft_1.mp4`.
    * Client feedback leads to `Draft_2.mp4`.
    * **The Stack:** The Dashboard shows **One Project Item** ("Wedding Film").
    * **Selector:** A dropdown allows toggling between `v1`, `v2`, `v3 (Current)`.
* **Locking:** Old versions are effectively "Locked" (Read-Only) to prevent confusion.

## 3. The "Screening Room" (Client Review Interface)
* **Interface:** A clean, branded video player (HLS Streaming via Cloudflare Stream).
* **Interaction:**
    * Client watches video.
    * Pauses at `02:14`.
    * Types comment: "Remove this shaky shot."
* **Result:**
    * Comment is saved with the **Timestamp** (`02:14`).
    * Editor sees a "Marker" on their timeline export list.
* **Approval State:**
    * Buttons: `Request Changes` (Requires text) or `Approve Version`.

## 4. The Post-Production Relay (Task Handoffs)
* **Problem:** Moving a project from "Shooter" to "Editor" to "Colorist".
* **The "Job Card" Flow:**
    1.  **Ingest:** Shooter uploads Proxies. Status -> `Ready for Edit`.
    2.  **Assignment:** Manager assigns "Editor Rahul".
    3.  **Edit Block:** Rahul works. Uploads `v1`. Status -> `Ready for Review`.
    4.  **Feedback Loop:** Client comments. Status -> `Revision Needed`.
    5.  **Finalizing:** Rahul uploads `vFinal`. Status -> `Ready for Color`.
    6.  **Handoff:** Manager re-assigns card to "Colorist Priya".
* **Permission Scope:** "Colorist" only sees the project *after* it is assigned to them.

## 5. Storage Optimization (Proxy vs. Master)
* **The Cost Trap:** Hosting 4K Pro-Res files for review is expensive.
* **The Logic:**
    * **Review Copies:** We transcode uploads to 1080p (Low Bitrate) for the "Screening Room".
    * **Master Delivery:** The actual 50GB file is stored in "Cold Storage" (R2) and only generated/link-shared when the Status is `Approved`.