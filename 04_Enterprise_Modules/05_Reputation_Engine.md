# Reputation Engine (Reviews & Testimonials)

## 1. Context
* **Goal:** Automate the collection of 5-Star Google Reviews to boost SEO and Trust.
* **Strategy:** The "Gatekeeper" Logic (Filter bad reviews internally, push good reviews publicly).

## 2. The Feedback Loop
* **Trigger:** Project Status changes to `Completed` OR `delivered`.
* **Action:** System sends a WhatsApp/Email: *"Hi [Name], how was your experience with [Studio Name]?"*
* **Interface:** Simple 1-5 Star selector.

## 3. The Gatekeeper Logic
* **Scenario A: High Rating (4-5 Stars)**
    * **System Response:** "Thank you! Please share this on our Google Profile for a 5% discount on your next shoot."
    * **Action:** Redirects user to the Studio's specific **Google Maps Review Link**.
    * **Portfolio:** Auto-adds the text to the "Testimonials" section of the website (pending Admin approval).
* **Scenario B: Low Rating (1-3 Stars)**
    * **System Response:** "We are sorry! Please tell us what went wrong so we can fix it."
    * **Action:** Opens a private "Feedback Form".
    * **Alert:** Manager receives an "Unhappy Client" notification immediately.
    * **Benefit:** Prevents the bad review from going public on Google.