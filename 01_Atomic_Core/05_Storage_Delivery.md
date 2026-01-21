# Storage & Delivery (The Hybrid Model)

## 1. The "Smart Select" Workflow
* **Desktop Bridge:** Local app installed by photographer.
* **Action:** Compresses RAWs -> Uploads Proxies to R2.
* **Client Selection:** Client likes photos on Web Portal.
* **Reverse Sync:** Bridge app reads selection -> Moves original RAWs on local disk to "Finals" folder.

## 2. Delivery Portal
* **URL:** `studiovault.in/view/[project-id]`
* **Features:**
    * View/Download (Permissions set by photographer).
    * **Watermarking:** Auto-applied if invoice is unpaid. Removed upon full payment.
    * **Timer:** "Link expires in X days".

## 3. Merch Integration
* **Upsell:** Inside the Client Portal, client can select a photo and click "Order Print/Frame".
* **Fulfillment:** Order sent to Photographer's Dashboard. Photographer fulfills manually.