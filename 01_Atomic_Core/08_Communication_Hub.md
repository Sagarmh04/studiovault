# Communication Hub

## 1. The Scoped Chat System
* **Architecture:** Chat is not global; it is **Context-Aware**.
* **Context A: Lead/Inquiry (Pre-Booking)**
    * *Scope:* Transient. Linked to `Lead_ID`.
    * *Rules:* Regex filters active (if Commission mode is On).
* **Context B: Project (Post-Booking)**
    * *Scope:* Permanent. Linked to `Project_ID`.
    * *Header:* Messages display context: "Regarding: Wedding Package A".
    * *Capabilities:* File sharing enabled.

## 2. Notification Engine
* **Triggers:**
    * **Internal:** "New Inquiry", "Payment Failed", "Storage 90% Full".
    * **External (Client):** "Invoice Due", "Photos Ready", "Contract Signed".
* **Routing:**
    * **High Priority (SMS/WhatsApp):** Booking Confirmations, Payment Reminders (Deducted from Wallet quota).
    * **Low Priority (Email):** Weekly summaries, Marketing.

## 3. Privacy Bridge
* **Marketplace Leads (RealCandid):**
    * System masks phone numbers.
    * Chat relays messages between Client <-> Photographer without revealing contact info until Booking is Confirmed.