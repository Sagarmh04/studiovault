# Enterprise Marketing Engine

## 1. Context & Goal
* **Goal:** Turn the passive "Client Database" into an active "Revenue Generator".
* **Architecture:** Uses the **Hybrid WhatsApp Routing** logic (Transaction = System Key, Marketing = User Key).
* **Compliance:** Strictly enforces "Opt-in" rules to prevent WhatsApp bans.

## 2. The Campaign Manager (Broadcasts)
* **Function:** Bulk messaging for offers/announcements.
* **Workflow:**
    1.  **Select Audience:** (e.g., "All Weddings from 2024").
    2.  **Compose Message:** Supports Variables (`Hi {{Name}}...`) and Media Templates (Images/Video).
    3.  **Cost Estimate:** System calculates: `Audience Size * Meta Per-Msg Cost`.
    4.  **Send/Schedule:** User confirms payment via their linked card (Direct to Meta).
* **Safety Rail:**
    * System checks if the User has a connected WABA (WhatsApp Business Account).
    * If No WABA -> Block Broadcast.

## 3. The Automation Builder (Drip Sequences)
* **Function:** "Set and Forget" triggers to increase Lifetime Value (LTV).
* **Trigger Types:**
    * `Project_Completed`: Send "Review Request" after 2 days.
    * `Birthday`: Send "Discount Voucher" on Client's Birthday.
    * `Inquiry_Stalled`: Send "Portfolio Highlight" if lead status is "Pending" for >3 days.
* **Logic:**
    * If Client replies -> Stop Sequence (Handover to Human Agent).

## 4. Audience Segmentation (Smart Filters)
* **Dynamic Lists:** Lists update automatically based on data.
* **Filter Parameters:**
    * **Spend:** "VIP Clients (>₹1L Lifetime Spend)".
    * **Category:** "Maternity Clients" (Target for Baby Shoot after 6 months).
    * **Location:** "Clients in Mumbai" (For local studio offers).
* **Static Lists:** Manual CSV upload (e.g., "Leads from Wedding Expo").

## 5. ROI Tracking
* **The "Attribution" Problem:** How do we know if a campaign worked?
* **Solution:** "Campaign-Linked Inquiries".
    * Every link in a campaign has a `?utm_source=campaign_id`.
    * If a Booking is created from that link -> Revenue is attributed to the Campaign.
    * **Report:** "Diwali Offer: Cost ₹500 -> Revenue ₹50,000 (100x ROI)".