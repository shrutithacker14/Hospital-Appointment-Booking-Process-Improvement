# Process Architecture: As-Is vs. To-Be Appointment Lifecycle (Zydus Hospitals Case Study)

## 1. Executive Summary of Process Transformation

> **Portfolio Scenario Note:** This process architecture models a hypothetical Business Analysis case study for **Zydus Hospitals** across 7 multispecialty facilities in **Gujarat (Ahmedabad & Bhuj), Maharashtra (Mumbai), Rajasthan (Jaipur), Delhi NCR (New Delhi), Karnataka (Bengaluru), and Tamil Nadu (Chennai)**. Metrics reflect the 5,000-row synthetic practice dataset.

| Process Dimension | As-Is State (Manual Baseline Cohort) | To-Be State (Omnichannel Cohort) | Cohort Variance |
| :--- | :--- | :--- | :--- |
| **Booking Channels** | Phone Call (60.40%), Walk-In Desk (39.60%) | Mobile App (28.88%), Web Portal (22.76%), WhatsApp Bot (22.40%), Walk-In (15.32%), Phone (10.64%) | **74.04% Digital Self-Service** |
| **Mean Booking Turnaround** | 11.36 minutes | 1.79 minutes | **-84.24% Relative Reduction** |
| **OPD Patient No-Show Share** | 23.92% (598 / 2,500) | 7.28% (182 / 2,500) | **-16.64 Percentage Points** |
| **Double-Booking Conflict Share** | 14.76% (369 / 2,500) | 0.00% (0 / 2,500; Redis 300s TTL Lock) | **100% Conflict Elimination** |
| **Cancelled Slot Re-Fill Rate** | 4.83% (18 / 373 refilled manually) | 78.17% (154 / 197 refilled via Waitlist Engine) | **+73.34 Percentage Points** |
| **Mean OPD Waiting Hall Time** | 48.52 minutes (Completed visits) | 14.25 minutes (Completed visits) | **-70.63% Relative Reduction** |

---

## 2. As-Is Process Map (Mermaid Flowchart)
```mermaid
flowchart TD
    subgraph Patient["Patient"]
        P1([Start: Needs Zydus OPD Consultation]) --> P2[Calls Hospital Reception or Visits Walk-In Desk]
        P2 --> P3[Experiences Manual Booking Turnaround: Mean 11.36 Mins]
        P6[Receives Verbal Slot Confirmation - Zero Automated Reminders] --> P7{Needs to Reschedule or Cancel?}
        P7 -->|Phone Line Busy / No Self-Service| P8[Fails to Notify Hospital -> 23.92% No-Show Share]
        P7 -->|Attends OPD| P9[Waits in Congested Hall: Mean 48.52 Mins Delay]
    end

    subgraph Reception["Zydus Front-Desk Receptionist"]
        R1[Answers Phone / Greets Walk-In] --> R2[Checks Physical Register or Standalone Excel]
        R2 --> R3{Slot Available?}
        R3 -->|No| R4[Negotiates Alternate Date Manually]
        R3 -->|Yes| R5[Logs Patient Details Manually]
        R5 --> R6[14.76% Double-Booking Conflict Across Concurrent Staff]
    end

    subgraph Doctor["OPD Specialist / Clinical Coordinator"]
        D1[Updates Emergency OT / Leave Verbally] --> D2[Sync Lag with Front Desk]
        D3[Experiences Unfilled No-Show Slots or Overbooked Queue]
    end

    P3 --> R1
    R4 --> P3
    R5 --> P6
    D2 -.->|Conflict| R2
    P8 --> D3
    R6 --> P9
```

---

## 3. To-Be Process Map (Mermaid Flowchart)
```mermaid
flowchart TD
    subgraph Patient["Patient (Zydus App / Web Portal / Multilingual WhatsApp Bot)"]
        TB_P1([Start: Initiates Booking]) --> TB_P2[Selects Zydus Facility Unit, Specialty, Doctor & Live Slot]
        TB_P2 --> TB_P3[Enters Mobile OTP -> Auto-Links ZYD-UHID & ABHA ID]
        TB_P3 --> TB_P4[Completes Pre-Paid UPI / Card Payment or Pay-at-OPD]
        TB_P5[Receives Instant WhatsApp/SMS Pass + Calendar Invite] --> TB_P6{T-24h / T-2h Smart Reminder Action?}
        TB_P6 -->|Confirms Attendance| TB_P7[Scans QR at Zydus Lobby Express Check-In Kiosk]
        TB_P6 -->|1-Click Reschedule / Cancel| TB_P8[Modifies Slot at ₹0 Fee or Triggers Instant UPI Refund]
    end

    subgraph System["Zydus CareConnect Engine & HIS Integration"]
        TB_S1[Applies 5-Min Redis Concurrency Lock on Slot] --> TB_S2[Validates Doctor Roster & Leave Calendar]
        TB_S2 --> TB_S3[Generates Booking ID & Updates Master HIS Database]
        TB_S3 --> TB_S4[Dispatches Multilingual Notification via WhatsApp/SMS Gateway]
        TB_S5[Releases Cancelled Slot & Triggers 15-Min Waitlist Auto-Promotion]
        TB_S6[Assigns Smart Queue Token & Alerts OPD Nursing Station]
    end

    subgraph Staff["Front-Desk & Doctor Console"]
        TB_D1[Doctor Marks Emergency OT / Leave on Mobile App] --> TB_D2[Bulk Priority Reschedule Links Sent to Affected Patients]
        TB_D3[Doctor Views Real-Time OPD Queue & Linked EHR Summary]
    end

    TB_P2 --> TB_S1
    TB_P4 --> TB_S3
    TB_S4 --> TB_P5
    TB_P8 --> TB_S5
    TB_P7 --> TB_S6
    TB_S6 --> TB_D3
    TB_D2 --> TB_S4
```
