# Technical Stack & Architecture (Cloudflare Edition)

## 1. Core Platforms (Monorepo)
* **Repo Structure:** Turborepo (pnpm workspace).
    * `apps/web`: Next.js (React Framework).
    * `apps/desktop`: Electron + Vite + React (Target: Windows).
    * `packages/db`: Drizzle ORM Schema + D1 Migrations.
    * `packages/api`: Cloudflare Workers (Hono Framework) - Shared Backend logic.
* **Hosting (Web):** Vercel or Cloudflare Pages.

## 2. Data Layer (The "Cheat Code")
* **Primary Database:** **Cloudflare D1** (Serverless SQLite).
    * **Strategy:** Sharded. Small tenants share a DB; Enterprise tenants get a dedicated DB.
    * **ORM:** **Drizzle ORM**. (Reason: Lightweight, runs on Edge, strict SQL typing).
* **Storage:** **Cloudflare R2** (S3 Compatible).
    * **Role:** Storing Images, Videos, and Assets. Zero egress fees.
    * **Upload Strategy:** Signed URLs (Direct Frontend -> R2).
* **Caching/Edge:** Cloudflare Global Network.

## 3. Compute & Backend Logic
* **API Logic:** **Cloudflare Workers**.
    * **Framework:** **Hono** (Fastest standard for Workers).
    * **Queues:** **Cloudflare Queues** for batching high-volume writes (e.g., File Upload counters).
* **Heavy Compute:** AWS Lambda (Only for Video Transcoding/AI processing, triggered via API).

## 4. Authentication & Security
* **Provider:** **Firebase Auth** (Identity Platform).
    * **Methods:** Email/Password, Google OAuth, Phone (OTP).
    * **Verification:** Workers verify Firebase ID Tokens using cached public keys (Offline verification).
* **Role Management:** Custom claims in Firebase Token + `users` table in D1.

## 5. Desktop Specifics (Offline First)
* **Local DB:** **SQLite** (better-sqlite3).
* **Sync Logic:** "Pull-Push".
    * *Pull:* Get diff since `last_sync_timestamp`.
    * *Push:* Send local Transaction Log to Cloudflare Worker.

## 6. Development Tools
* **Package Manager:** pnpm.
* **Database GUI:** Drizzle Studio / Cloudflare Dashboard.
* **AI Context:** Gemini CLI / Cursor.