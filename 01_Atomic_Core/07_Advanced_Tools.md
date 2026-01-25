# Advanced Tools ("The Luxury Suite")

## 1. "Magic" Mood Board
* **Context:** Replacing WhatsApp image dumps.
* **Feature:** Drag-and-drop "Visual Board" inside a Project.
* **Capabilities:**
    * Upload reference images.
    * Add text notes ("Lighting setup here").
    * Share: Client gets a view-only link to the board.

## 2. Automated Shoot Sheet (Call Sheet)
* **Trigger:** One-click generation inside Job Card.
* **Output:** Professional PDF containing:
    * Logistics: Date, Call Time, Location (Map Link).
    * Environment: Weather Forecast, Golden Hour Time (Auto-fetched).
    * Team: List of assigned Staff & Contact info.
    * Gear: Checklist of "Locked" assets for this shoot.

## 3. Portfolio Customization
* **Scope:** The `subdomain.studiovault.in` page.
* **Builder:**
    * Hero Section: Customizable Banner/Video.
    * Custom Sections: "About Me", "Testimonials", "Awards".
    * Merch Visibility: Toggle to show/hide "Shop" section per Branch.
    * Booking Toggle: Option to Enable/Disable "Book Now" button.

## 4. Automated Watermarking Engine
* **Goal:** Brand protection and payment enforcement.
* **Configuration:**
    * **Upload:** Admin uploads a high-res PNG logo.
    * **Settings:** Opacity (e.g., 30%), Scale (e.g., 50%), Pattern (Center vs. Tiled).
* **Triggers:**
    * **Unpaid Invoices:** Auto-applies "Proof Only" watermark to all gallery downloads.
    * **Public Portfolios:** Auto-applies subtle Brand Logo to public-facing images.
* **Removal:** System instantly regenerates "Clean" versions once Payment Status == `PAID`.