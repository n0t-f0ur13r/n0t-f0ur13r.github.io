---
title: "UBike: IoT Biometric Security System"
date: 2025-06-15
tags: ["C++", "ESP32", "Django", "IoT"]
author: "Josué Leiva"
showToc: true
TocOpen: false
draft: false
cover:
    image: "https://raw.githubusercontent.com/n0t-f0ur13r/UBike/master/images/circuit_diagram.png" # OJO: Aquí pondremos una foto real después
    alt: "UBike System Architecture"
    caption: "ESP32 Node connected to Django Backend"
    relative: false
---

### 🔗 [View Code on GitHub](https://github.com/n0t-f0ur13r/UBike)

## The Problem
University campuses lack automated parking solutions for bicycles. 
Traditional locks are vulnerable, and manual registration is slow (crucial when the flow of students is high). 
We needed a system that authenticated users and mechanically secured the bike without human intervention.

Provide fast and easy to use interface for both campus guards and bicycle owners to administrate 
the bicycles on the campus and their own bicycle respectively.

## The Solution
Co engineered a **distributed IoT network** where each parking node operates autonomously using an **ESP32** microcontroller.
* **Hardware:** Custom circuit interfacing RC522 RFID readers and solenoids for physical locking.
* **Connectivity:** Nodes communicate via secure HTTP requests to a central **Django** server.
* **Feedback:** LED status indicators and fail-safe mechanisms for power outages.
* **Interface:** Guards and Bicycle owners can access a Web Application that allows them to control and obtain information for the bicycles.

## Tech Stack
* **Firmware:** C++ (Arduino Framework) with manual memory management for the ESP32.
* **Backend:** Python (Django) & PostgreSQL for user/device management.
* **Protocol:** REST API over WiFi.

## Engineering Challenge
The biggest hurdle was **handling network latency** on the microcontroller. The solenoid had to unlock instantly upon card scan.
* *Solution:* Implemented an asynchronous state machine on the ESP32 that caches valid IDs locally for offline operation, syncing with the database only when the network is idle.


## Future Improvements (Roadmap)
Given the maturity of a first semester course, it can certainly improve in many areas.

* **Physical lock:** Given the field of engineering, the lock was not properly designed for physical aggression or security, only a working concept with solenoid.
* **Hardware:** Lacking knowledge in electronics produced several solenoid failures.
* **Firmware:** Managing concurrency between WiFi and Server (Django Backend) connection within an embedded environment, produces deadlock.

---
> *Note: This project was developed as a Capstone for the first semester course Introduction to Engineering.*
