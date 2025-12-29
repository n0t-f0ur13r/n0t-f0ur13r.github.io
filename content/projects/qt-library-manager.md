---
title: "C++/Qt Library Management System"
date: 2025-07-20
tags: ["C++17", "Qt6", "SQLite", "Desktop App"]
author: "Josué Leiva"
showToc: true
TocOpen: false
draft: false
cover:
    image: "" # Pendiente: Una captura de la interfaz de Qt (con los botones y listas)
    alt: "Qt Desktop Interface"
    caption: "Cross-platform Desktop GUI managing SQLite Data"
    relative: false
---

### 🔗 [View Code on GitHub](https://github.com/n0t-f0ur13r/qt-library-manager) 

## The Problem
Small to medium-sized libraries often rely on spreadsheets or expensive cloud software. 
The requirement was to build a robust, **offline-first** desktop solution that could handle relational data (Books, Readers, Loans) with transactional integrity, ensuring no data loss during power failures or crashes.
Given the library sizes on scope, the software must take care of low computing resources.

## The Solution
Co-developed a desktop application using **Qt 6** for the frontend and **Native C++** for the backend logic.
* **Architecture:** Implemented a custom MVC pattern.
* **Native Database Integration:** Instead of relying on high-level frameworks, we integrated the **raw `sqlite3.h` C library**. This allowed for granular control over SQL execution and memory usage, bypassing the overhead of Qt's SQL module.
* **Business Logic:** Automated penalty calculation algorithms based on date differentials.
* **Simplicity:** Given the size of the libraries, the desktop application is aimed to suffice the needs of a library administrator, not reader.

## Tech Stack
* **Language:** C++17.
* **GUI:** Qt 6 (Widgets).
* **Database:** SQLite 3 (Native C Interface).
* **Debugging:** GDB & Qt Creator Debugger.

## Engineering Challenge
The most critical hurdle was a **"Ghost Signal" & Double Execution Bug**.
* *The Issue:* UI actions (like confirming a book loan) were firing twice, causing data corruption and random behaviour.
* *The Investigation:* Through deep debugging with GDB, traced the issue to a flaw in the class inheritance structure (using `QWidget` instead of `QDialog` for modals), which broke the event loop isolation.
* *The Fix:* Refactored the window hierarchy to enforce strict modal states and implemented a "Safe Slot" mechanism to prevent duplicate signal connections. It was also necessary to rebuild the project configuration to clean corrupted intermediate binaries that were masking the true error.

## Future Improvements (Roadmap)
While the system is stable for local deployment, scaling it for a larger institution would require addressing specific architectural constraints:

* **Migration to Client-Server Architecture:** Currently, the app relies on a local SQLite file, which limits concurrent usage. The next logical step is to abstract the `GestorBaseDeDatos` class to support a **PostgreSQL** connection, enabling multiple librarians to work simultaneously from different terminals.
* **Automated Testing Suite:** As noted in the final report, the project relied on manual functional testing. Integrating **Google Test** or **Qt Test** for automated unit and regression testing would prevent the recurrence of the "double signal" bugs fixed during development.
* **Modern UI/UX:** Migrating the frontend from Qt Widgets to **Qt Quick (QML)** to provide a more fluid, touch-friendly interface suitable for modern kiosks.

---
> *Note: Collaborative Capstone Project for the Object Oriented Design and Programming (3th semester). My primary focus was on the Backend Logic and UI creation.*
