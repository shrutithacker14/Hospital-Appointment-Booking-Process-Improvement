# UAT Plan and Requirements Traceability Matrix (RTM) — Zydus Hospitals Case Study

## 1. Purpose & Portfolio Scope
This module defines 14 end-to-end User Acceptance Testing (`UAT-TC-01` to `UAT-TC-14`) scenarios and the bi-directional **Requirements Traceability Matrix (RTM)** covering `FR-01` through `FR-12` for the hypothetical **Zydus Hospitals** appointment booking case study.

> **Execution Status (`Not Run`):** Because this repository is a Business Analysis documentation and data-modeling portfolio project rather than a deployed software build, all 14 UAT scenarios are marked **`Not Run`**.

## 2. Requirements Traceability Summary (`FR-01` to `FR-12`)
| BRD Req ID | Requirement Summary | Linked User Story | Linked UAT Test Case | Status |
| :--- | :--- | :--- | :--- | :--- |
| **FR-01** | Mobile OTP Auth & Zydus UHID / ABHA Linking | `US-01` | `UAT-TC-01` | Draft — Not Tested |
| **FR-02** | Multi-Filter Slot Search (Zydus Unit, Specialty, Fee ₹) | `US-01`, `US-03` | `UAT-TC-01`, `UAT-TC-04` | Draft — Not Tested |
| **FR-03** | 5-Minute Redis Concurrency Slot Lock (300s TTL) | `US-02` | `UAT-TC-02`, `UAT-TC-03` | Draft — Not Tested |
| **FR-04** | 1-Click Self-Service Reschedule (>= 2h Prior at ₹0 Fee) | `US-03`, `US-04` | `UAT-TC-05`, `UAT-TC-06` | Draft — Not Tested |
| **FR-05** | Automated Cancellation & Instant UPI Refund Engine | `US-05` | `UAT-TC-07`, `UAT-TC-08` | Draft — Not Tested |
| **FR-06** | Automated T-24h & T-2h WhatsApp/SMS Interactive Reminders | `US-06` | `UAT-TC-09` | Draft — Not Tested |
| **FR-07** | Dynamic Waitlist Queue Auto-Promotion (15-Min Claim Window) | `US-07` | `UAT-TC-10` | Draft — Not Tested |
| **FR-08** | Doctor Emergency OT/Leave Block & Bulk Patient Reschedule | `US-08` | `UAT-TC-11` | Draft — Not Tested |
| **FR-09** | Unified Front-Desk Assisted Booking & Thermal Token Console | `US-09` | `UAT-TC-12` | Draft — Not Tested |
| **FR-10** | Lobby QR Express Check-In Kiosk & Live OPD Queue Token | `US-10` | `UAT-TC-12` | Draft — Not Tested |
| **FR-11** | Video Tele-Consultation Toggle & Encrypted WebRTC Link | `US-11` | `UAT-TC-13` | Draft — Not Tested |
| **FR-12** | Executive BI Analytics Dashboard (7 Zydus Units & INR KPIs) | `US-12` | `UAT-TC-14` | Draft — Not Tested |
