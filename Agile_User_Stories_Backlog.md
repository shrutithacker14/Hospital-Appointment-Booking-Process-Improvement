# Agile Product Backlog: Epics, User Stories & Gherkin Acceptance Criteria (Zydus Hospitals Case Study)

## 1. Epic Summary (5 Epics | 12 User Stories | 70 Story Points)
1. **EP-01:** Omnichannel Patient Self-Service Booking (`US-01`, `US-02`, `US-03` — Web, Mobile App, Multilingual WhatsApp Bot)
2. **EP-02:** Self-Service Rescheduling, Cancellation & Automated UPI Refund Engine (`US-04`, `US-05`)
3. **EP-03:** Multi-Channel Smart Reminders & Dynamic Waitlist Promotion (`US-06`, `US-07`)
4. **EP-04:** Doctor Roster Management, Emergency Bulk-Reschedule, Assisted Console & Lobby QR Check-In (`US-08`, `US-09`, `US-10`)
5. **EP-05:** Video Tele-Consultation & Executive BI Analytics Dashboard (`US-11`, `US-12`)

---

## 2. Detailed User Stories & Gherkin Acceptance Criteria

### US-01: Multi-Filter Slot Discovery & ZYD-UHID / ABHA Linking (Must Have | 5 SP | Sprint 1 | FR-01, FR-02)
* **User Story:** As a patient visiting Zydus Hospitals, I want to search and filter doctors by state hospital unit, specialty, language, and consultation fee (₹) with live slot visibility, so that I can book an appointment without calling reception.
* **Acceptance Criteria (Gherkin):**
  ```gherkin
  Scenario: Patient filters doctors by Zydus facility unit and clinical specialty
    Given the patient is logged into the Zydus CareConnect Web Portal or Mobile App via Mobile OTP
    When the patient selects Facility "Zydus Hospitals - Ahmedabad (SG Highway)", Department "Cardiology", and Date "Tomorrow"
    Then the system auto-links their ZYD-UHID and ABHA ID and returns matching doctors with Consultation Fee in INR (₹1,000), spoken languages, and live 30-minute time slots within 1.2 seconds.
  ```

### US-02: Real-Time 5-Minute Concurrency Slot Lock (Must Have | 8 SP | Sprint 1 | FR-03)
* **User Story:** As a patient, I want my selected appointment slot to be temporarily locked for 5 minutes while I complete UPI/Card payment, so that another user or reception desk cannot double-book my slot.
* **Acceptance Criteria (Gherkin):**
  ```gherkin
  Scenario: Concurrent users attempt to book the exact same doctor slot
    Given Patient A selects the 10:30 AM slot at Zydus Hospitals - Mumbai (Andheri West) and clicks "Proceed to Pay"
    When Patient B (or a Front-Desk Receptionist) views the calendar within the next 300 seconds
    Then the 10:30 AM slot is displayed as "Temporarily Reserved" and cannot be selected
    And if Patient A completes payment within 300 seconds, the slot is permanently booked
    But if Patient A abandons checkout after 300 seconds, the Redis TTL lock expires and the slot returns to "Available".
  ```

### US-03: Multilingual WhatsApp Conversational Booking Bot (Must Have | 8 SP | Sprint 2 | FR-02, FR-04)
* **User Story:** As a patient, I want to book, reschedule, or cancel appointments via a multilingual Zydus WhatsApp Bot (English, Hindi, Gujarati), so that I can manage visits easily without installing an app.
* **Acceptance Criteria (Gherkin):**
  ```gherkin
  Scenario: Patient books an OPD slot via WhatsApp in Gujarati or Hindi
    Given the patient sends "Hi" to the verified Zydus Hospitals WhatsApp Business number
    When the patient selects preferred language (English / हिंदी / ગુજરાતી) and chooses Facility & Specialty
    Then the bot presents interactive list messages for available slots
    And generates an instant UPI payment link or Pay-at-OPD confirmation with a downloadable PDF appointment pass.
  ```

### US-04 & US-05: Self-Service Reschedule & Automated UPI Refund (Must Have | 10 SP | Sprint 2 | FR-04, FR-05)
* **User Story:** As a patient, I want to reschedule up to 2 hours prior at ₹0 fee or cancel >= 4 hours prior for an instant 100% UPI refund, so that I have full flexibility without calling the hospital.
* **Acceptance Criteria (Gherkin):**
  ```gherkin
  Scenario: Patient cancels pre-paid appointment more than 4 hours before slot time
    Given the patient paid ₹800 via UPI for a 04:00 PM Orthopedics consultation at Zydus Hospitals - Bhuj (Kutch)
    When the patient clicks "Cancel Appointment" at 10:30 AM (5.5 hours prior)
    Then the system releases the 04:00 PM slot immediately to the Waitlist Engine
    And triggers a 100% refund (₹800) via Razorpay Refund API with an SMS/WhatsApp transaction reference.
  ```

### US-06 & US-07: Smart Reminders & Dynamic Waitlist Slot Promotion (Must/Should Have | 11 SP | Sprint 2–3 | FR-06, FR-07)
* **User Story:** As a waitlisted patient for a fully booked Zydus specialist, I want to be automatically notified when a slot opens up due to a cancellation, so that I can claim an earlier consultation.
* **Acceptance Criteria (Gherkin):**
  ```gherkin
  Scenario: Cancelled slot is auto-offered to top 3 waitlisted patients
    Given a Neurology specialist's schedule is 100% booked and 3 patients are on the Waitlist
    When a confirmed patient cancels their 03:30 PM slot via the T-24h WhatsApp reminder link
    Then the system dispatches an instant claim link to the top 3 waitlisted patients
    And the first patient to confirm within 15 minutes secures the 03:30 PM slot (Waitlist_Slot_Reallocated = Yes).
  ```

### US-08, US-09 & US-10: Doctor Roster Block, Reception Console & Lobby QR Check-In (Must/Should Have | 18 SP | Sprint 3–4 | FR-08, FR-09, FR-10)
* **User Story:** As an OPD Doctor, Receptionist, or Arriving Patient, I want seamless roster blocks, <45-second walk-in token registration, and self-service lobby QR check-in, so that OPD waiting hall congestion is minimized.

### US-11 & US-12: Video Tele-Consultation & Executive BI Dashboard (Could/Must Have | 10 SP | Sprint 4 | FR-11, FR-12)
* **User Story:** As the Zydus Hospitals COO, I want an interactive executive dashboard displaying state-wise and facility-wise bookings, no-show %, waitlist refill %, channel mix, and realized revenue (₹), so I can monitor operational performance across all 7 regional units.
