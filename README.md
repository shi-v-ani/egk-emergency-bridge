# egk-emergency-bridge# eGK Emergency Bridge

An offline-first emergency information station that interfaces with an electronic health card (eGK / synthetic test card) via NFC, securely parses permitted data locally, and combines it with a CNN-based computer vision system to verify physical emergency equipment before triggering an ESP32-controlled hardware response.

---

## Project Overview

The **eGK Emergency Bridge** demonstrates how cryptographic smart-card interactions, edge computer vision, and embedded hardware can work together in a secure, offline environment. Rather than focusing on disease prediction, this project addresses **operational readiness and secure access control**:

1. **Smart Card Handshake:** Reads and parses emergency-related data from an eGK or test smart card using an NFC reader via standard PC/SC protocols.
2. **Computer Vision Verification:** Uses an edge camera and a lightweight CNN model to inspect an emergency kit tray and verify that required medical gear is present and correctly positioned.
3. **Physical Actuator Feedback:** Triggers an ESP32 microcontroller (via local communication) to provide a physical "ready" signal (LED/actuator) only if both patient validation and physical equipment checks pass successfully.

---

## System Architecture

```text
+------------------+      NFC / APDU      +--------------------+
|  eGK / Test Card | -------------------> |   NFC Reader (PC/  |
+------------------+                      |   Raspberry Pi)    |
                                          +---------+----------+
                                                    | Parsed & Verified Data
                                                    v
+------------------+      Serial / GPIO   +--------------------+
| ESP32 Actuator   | <-------------------|  Local Processing  |
| / LED / Buzzer   |                      |  Engine & GUI      |
+------------------+                      +---------+----------+
                                                    ^
                                                    | Inference Result
                                          +---------+----------+
                                          |  Camera / CNN CV   |
                                          |  Verification      |
                                          +--------------------+
