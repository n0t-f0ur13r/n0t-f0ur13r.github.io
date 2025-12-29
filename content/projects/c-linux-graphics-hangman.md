---
title: "Native C/X11 Hybrid Game Engine"
date: 2025-06-15
tags: ["C", "Linux", "X11", "Memory Management"]
author: "Josué Leiva"
showToc: true
TocOpen: false
draft: false
cover:
    image: "" # Déjalo vacío por ahora o pon una captura de tu terminal
    alt: "Game running in Linux Terminal"
    caption: "Hybrid Console/GUI Interface"
    relative: false
---

### 🔗 [View Code on GitHub](https://github.com/n0t-f0ur13r/c-linux-graphics-hangman)

## The Problem
Standard terminal games lack visual engagement, while full GUI frameworks hide the low-level complexities. The goal was to build a "Hangman" style game that runs primarily in the **Linux Console** for input logic but renders progressive images in a separate **X11 window**, without relying on modern game engines.

## The Solution
I engineered a native C application that bridges standard I/O with the X Window System.
* **Hybrid Architecture:** The core logic runs in the terminal (stdin/stdout), while the X11 display handles graphical rendering using **Imlib2**.
* **Algorithmic richness:** Implemented various classic sorting algorithms to add learning experience in the comparison of their performance (time based).
* **Resource Auditing:** The application was built with a strict focus on resource management, avoiding memory leaks typical in raw C development.
Side note: Imlib2 has it's own memory leaks; out of the scope of the project.

## Tech Stack
* **Language:** C (Standard C99).
* **Graphics:** XLib & Imlib2 (Direct library interfacing).
* **QA & Performance:** Valgrind (Memory leak detection), GDB.
* **Build System:** GNU Make.

## Engineering Challenge
The biggest hurdle was **Manual Memory Management** and ensuring stability.
* *The Issue:* Interfacing string manipulation algorithms with graphical buffers in C is prone to segmentation faults and memory leaks.
* *Solution:* I implemented a rigorous allocation/deallocation pattern and used **Valgrind** to audit the execution, identifying and patching pointers that were not being freed correctly, ensuring a leak-free runtime.

---
> *Note: Developed for the Data Structures & Algorithms course (3rd Semester).*
