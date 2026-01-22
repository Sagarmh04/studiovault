# Future Scope: Local AI Culling ("The Blink Detector")

## 1. Context
* **Status:** FUTURE INTEREST (Not in Atomic Phase).
* **Dependency:** Desktop App (Electron) + Local GPU.

## 2. Proposed Feature
* **Pre-Upload Scan:** Before "Smart Select" uploads proxies, a local AI model scans the RAW files.
* **Detection Classes:**
    * `Focus_Score`: Detects blur.
    * `Eye_State`: Detects closed eyes.
    * `Exposure`: Detects underexposed/black frames.
* **UX:** Auto-tags images as "Rejected" or "Review", saving the photographer hours of manual culling.