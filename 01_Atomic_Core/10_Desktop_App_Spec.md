# Desktop Application Specification (Electron/Vite)

## 1. Why Desktop?
* **Access Control:** Native access to OS File System (for Smart Select) and OS Print Spooler (for POS).
* **Performance:** Offline-first capability for POS features.

## 2. Feature: Smart Select (Local-Cloud Bridge)
* **The Problem:** Preventing upload of 100GB RAW files.
* **The Workflow:**
    1.  Photographer points App to Local Folder (RAWs).
    2.  App locally compresses to 1080p Proxies + Thumbnails.
    3.  App uploads *only* Proxies to Cloud (R2).
    4.  **Reverse Sync:** When client selects photos on Web:
        * App downloads `selection.json`.
        * App matches filenames to Local RAWs.
        * App moves selected RAWs to a "Finals" folder on the user's hard drive.

## 3. Feature: POS Printing
* **Capability:** Direct integration with Windows/Mac Print dialogs for immediate passport/stamp photo generation.

## 4. Distribution
* **Channel:** Microsoft Store / Direct Download Link.
* **Web behavior:** If user accesses POS/Smart-Select on Web, show: "Download App to use this feature."