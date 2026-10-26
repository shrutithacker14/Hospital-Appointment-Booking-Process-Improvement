# Business Requirements Document (BRD)
**Project Name:** Zydus CareConnect — Omnichannel Hospital Appointment Booking & Queue Optimization System  
**Organization:** Zydus Hospitals (Hypothetical Pan-India Multispecialty Network Case Study)  
**Document Version:** 2.1 (BABOK v3 Aligned Portfolio Draft — Proposed for Validation)  
**Lead Business Analyst:** Shruti Thacker ([@shrutithacker14](https://github.com/shrutithacker14))  

---

## 1. Executive Summary & Business Problem
For this hypothetical business analysis case study, **Zydus Hospitals** is modeled across 7 multispecialty units in 6 regional markets (**Gujarat [Ahmedabad & Bhuj], Maharashtra [Mumbai], Rajasthan [Jaipur], Delhi NCR [New Delhi], Karnataka [Bengaluru], and Tamil Nadu [Chennai]**), handling an assumed baseline volume of approximately 1,250 Outpatient Department (OPD) consultations daily. The scenario models a transition from decentralized telephone lines, physical registers, and standalone spreadsheets to a centralized omnichannel appointment and queue management platform.

### Illustrative Scenario Findings (Calculated from the 5,000-row Synthetic Practice Dataset):
* **23.92% synthetic no-show share (As-Is):** 598 of 2,500 baseline records are marked `No-Show` (accounting for ₹4,45,250 in simulated unbilled slot value), compared to **7.28%** (182 of 2,500; ₹1,39,700) in the To-Be cohort.
* **11.36-minute mean booking turnaround (As-Is):** Baseline bookings via Phone Call (60.40%) and Walk-In Desk (39.60%) average 11.36 minutes, compared to **1.79 minutes** across the omnichannel To-Be cohort.
* **14.76% double-booking conflict share (As-Is):** 369 baseline bookings experienced concurrent slot conflicts, contributing to a **48.52-minute mean OPD waiting hall time** for completed visits (reduced to **14.25 minutes** in the To-Be cohort).
* **4.83% cancelled slot refill rate (As-Is):** Only 18 of 373 cancelled baseline appointments were manually reallocated, compared to **78.17% (154 of 197)** in the To-Be cohort with automated waitlist promotion.

---

## 2. Business Objectives & Target KPIs
| KPI ID | KPI Metric | Baseline (As-Is Cohort) | Target (To-Be Proposal) | To-Be Sample Result | Validation & Measurement Approach |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **KPI-01** | **OPD No-Show Share** | 23.92% (598 / 2,500) | < 8.0% | 7.28% (182 / 2,500) | Measure across 90-day pilot vs. seasonally matched baseline |
| **KPI-02** | **Mean Booking Turnaround** | 11.36 min | < 2.0 min | 1.79 min | Timestamp log from slot selection to Booking ID generation |
| **KPI-03** | **Double-Booking Conflict Share** | 14.76% (369 / 2,500) | 0.0% | 0.00% (0 / 2,500) | Concurrency load testing on Redis 300s TTL slot locks |
| **KPI-04** | **Digital Self-Service Share** | 0.00% (0 / 2,500) | >= 70.0% | 74.04% (1,851 / 2,500) | Combined share of Mobile App, Web Portal, and WhatsApp Bot |
| **KPI-05** | **Cancelled Slot Re-Fill Rate** | 4.83% (18 / 373) | >= 75.0% | 78.17% (154 / 197) | Waitlist-reallocated bookings divided by total cancellations |
| **KPI-06** | **Waiting Time (Completed Visits)** | 48.52 min | < 15.0 min | 14.25 min | QR check-in timestamp to doctor consultation start timestamp |
| **KPI-07** | **ABHA Health ID Linkage Rate** | 18.08% (452 / 2,500) | >= 80.0% | 84.08% (2,102 / 2,500) | Share of UHID profiles verified via ABDM gateway |

---

## 3. Functional Requirements Summary (FR-01 to FR-12)
| Req ID | Module | Requirement Description | MoSCoW Priority | Linked Story | Linked UAT |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **FR-01** | Patient Auth & UHID | Authenticate via Mobile OTP; auto-link existing Zydus UHID (`ZYD-UHID-XXXXXX`) and Ayushman Bharat Health Account (ABHA ID). | **Must Have** | US-01 | UAT-TC-01 |
| **FR-02** | Multi-Filter Discovery | Filter by Zydus State Facility, Specialty, Doctor, Consultation Fee (₹), Language, and Live Availability. | **Must Have** | US-01, US-03 | UAT-TC-01, UAT-TC-04 |
| **FR-03** | Concurrency Slot Lock | Place a 5-minute (300s) temporary Redis lock on selected slots during checkout to prevent double booking across channels. | **Must Have** | US-02 | UAT-TC-02, UAT-TC-03 |
| **FR-04** | Self-Service Reschedule | Allow 1-click rescheduling up to 2 hours prior to appointment via Web, App, or WhatsApp Bot at ₹0 modification fee. | **Must Have** | US-03, US-04 | UAT-TC-05, UAT-TC-06 |
| **FR-05** | Cancellation & Refund | Instant 100% refund to UPI/source for cancellations >= 4 hours prior; configurable 20% deduction for < 4 hours. | **Must Have** | US-05 | UAT-TC-07, UAT-TC-08 |
| **FR-06** | Smart Reminders | Automated WhatsApp & SMS alerts upon booking, at T-24h, and T-2h with interactive Confirm/Reschedule/Cancel buttons. | **Must Have** | US-06 | UAT-TC-09 |
| **FR-07** | Dynamic Waitlist | Auto-notify top 3 waitlisted patients when a slot opens; allocate on a first-to-confirm basis within 15 mins. | **Should Have** | US-07 | UAT-TC-10 |
| **FR-08** | Doctor Leave & Roster | Allow doctors/coordinators to mark emergency OT/leave and trigger bulk priority-reschedule links to affected patients. | **Must Have** | US-08 | UAT-TC-11 |
| **FR-09** | Assisted Desk Console | Unified reception view for walk-ins, cash/UPI collection, thermal QR token printing, and senior citizen assistance. | **Must Have** | US-09 | UAT-TC-12 |
| **FR-10** | QR Express Check-In | Self-service QR scan at Zydus hospital lobby kiosk to generate live OPD queue token and alert nursing desk. | **Should Have** | US-10 | UAT-TC-12 |
| **FR-11** | Tele-Consultation | Option to switch between Physical OPD Visit and Video Consultation with automated WebRTC link and e-prescription upload. | **Could Have** | US-11 | UAT-TC-13 |
| **FR-12** | Executive BI Analytics | Real-time dashboard tracking Zydus State Facility KPIs, Revenue (₹), No-Show %, Channel Mix, and Doctor Utilization. | **Must Have** | US-12 | UAT-TC-14 |

---

## 4. Non-Functional Requirements (NFR)
* **NFR-01 (Performance):** API response < 1.2s (P95) under 5,000 concurrent users during peak morning OPD traffic (08:30 AM – 11:30 AM IST).
* **NFR-02 (Availability):** 99.95% uptime SLA with multi-AZ cloud failover and 15-minute RPO backups.
* **NFR-03 (Compliance & Security):** Alignment with India's Digital Personal Data Protection (DPDP) Act 2023 and Ayushman Bharat Digital Mission (ABDM) health data standards; AES-256 encryption at rest and TLS 1.3 in transit.
* **NFR-04 (Localization):** Full multilingual UI and WhatsApp Bot support in **English, Hindi (हिंदी), and Gujarati (ગુજરાતી)**.

---

## 5. Portfolio Case-Study Disclaimer
This repository presents a **hypothetical Business Analysis portfolio case study** modeled around Zydus Hospitals. It is not commissioned, endorsed, or supplied by Zydus Hospitals, and contains zero real patient or operational records. All metrics are calculated from the 5,000-row synthetic dataset constructed to demonstrate BABOK-aligned requirements engineering, process modeling, backlog refinement, UAT planning, and KPI analysis.
