  # SwiftTask Mobile App — Comprehensive QA Test Specification Suite

## Project Overview
SwiftTask is a high-velocity, on-demand mobile application designed to connect clients with local service providers (Taskers) for task and errand management.
The platform features an integrated FinTech escrow wallet, live-chat messaging, real-time proximity-based job boards, and automated task lifecycle transitions.

This repository serves as a professional manual testing portfolio piece. It showcases an exhaustive, 
**47-scenario master regression test suite** designed to isolate critical application bugs, edge cases, financial race conditions, and security vulnerabilities before production release.

---

##  Testing Scope & Architecture
To align with elite engineering standards, every test script in this repository avoids passive language (such as *"observe"* or *"monitor"*) and
instead relies on **explicit, directive physical actions** coupled with **immediate, objective defect assertions**.

The suite is structured systematically into the following functional domains:

| Module Category | Test Case IDs | High-Impact Scope Covered |
| :--- | :--- | :--- |
| **FinTech & Escrow Wallet** | `TC-ST-FIN-001` to `012` | Escrow locks, payment gateway webhook failures, database double-refund race conditions, and localized multi-currency conversion math.|
| **Security & Access Control** | `TC-ST-SEC-013` to `016` | Token deactivation blocks, zero-input account deletion bypass exploits, and phone-string data validation. |
| **Task Lifecycle Engine** | `TC-ST-ENG-017` to `024` | Websocket live-refresh synchronization, private direct-hire data leaks, and state machine status regressions. |
| **Messaging & Trust Safety** | `TC-ST-MSG-025` to `032` | PII chat history auto-purges upon task completion, chat-block routing bypasses, and form validation bypasses. |
| **Notifications & Proximity** | `TC-ST-NOT-033` to `043` | Native iOS/Android OS intent handling (GPS), proximity calculation tracking fluctuations, and badge counter synchronization. |
| **UI/UX Design System** | `TC-ST-UIX-044` to `047` | Multi-device text-wrapping container overflows, Dark Mode typographic contrast ratios, and copy typos. |

---

##  Key Critical Defects Isolated
During the execution of this suite, several business-critical defects were isolated and documented. Highlighting these demonstrating real-world QA impact:

### 1. The Escrow Double-Refund Race Condition (`TC-ST-FIN-003`)
* **The Issue:** When an Administrator initiates a manual task cancellation inside the Admin Portal, the database triggers two parallel balance write adjustments sequentially.
* **The Impact:** This creates a critical race condition that rewards the Client with an unauthorized double-credit refund directly out of platform escrows. 

### 2. Password Challenge Account Deletion Bypass (`TC-ST-SEC-013`)
* **The Issue:** The interface allows a user to trigger a permanent account deletion request with a blank or unverified password confirmation input.
* **The Impact:** The system completely bypasses the security challenge layer and clears out the live user profile data block via the API,
* leaving accounts highly vulnerable to session hijacking destructive exploits.

### 3. Messaging PII Leaks Post-Task Completion (`TC-ST-MSG-026`)
* **The Issue:** Upon transitioning a task's status marker to `Completed`, historical live-chat messaging logs and media files fail to purge.
* **The Impact:** Users maintain full interactive chat history access indefinitely, leaving sensitive client location coordinates, phone numbers,
*  and images exposed long after the contract concludes.

---

## 📁 Repository Structure
```text
├── manual-testing/
│   └── https://docs.google.com/spreadsheets/d/1tB8tjQtjMzq1J8VIcJXLVsy1w0mqsH6lkIfYyo2yTrU/edit?usp=sharing  <- Master 47 Test Case Spreadsheet
└── README.md                                              <- Project Summary & Scope Documentation
