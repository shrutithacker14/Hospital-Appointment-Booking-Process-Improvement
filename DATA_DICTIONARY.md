# Data Dictionary — Zydus Hospitals Synthetic Appointment Dataset (`n = 5,000`, 26 Columns)

All records in `Zydus_Hospital_Appointment_Dataset_5000.csv` (and `Indian_Hospital_Appointment_Dataset_5000.csv`) are synthetic and constructed for Business Analysis portfolio practice.

| Col # | Field Name | Data Type | Permitted Values / Format | Business Definition & Governance Notes |
| :---: | :--- | :--- | :--- | :--- |
| 1 | `Appointment_ID` | String (PK) | `APT-100001` to `APT-105000` | Unique synthetic appointment key (zero duplicates). |
| 2 | `Patient_UHID` | String | `ZYD-UHID-XXXXXX` | Synthetic Zydus Unique Hospital Identification Number. |
| 3 | `Phase` | Category | `Pre-Implementation (As-Is)`, `Post-Implementation (To-Be)` | Balanced 2,500-row synthetic scenario cohorts. |
| 4 | `Booking_Date` | Date (ISO) | `YYYY-MM-DD` (`2025-09-24` to `2026-03-31`) | Date the booking request was initiated. |
| 5 | `Appointment_Date` | Date (ISO) | `YYYY-MM-DD` (`2025-10-01` to `2026-03-31`) | Scheduled OPD consultation date (`Q4 2025` As-Is; `Q1 2026` To-Be). |
| 6 | `Lead_Time_Days` | Integer | `0` to `7` days | Days between `Booking_Date` and `Appointment_Date` (`0` for Walk-Ins). |
| 7 | `Slot_Time` | String | `09:00 AM` to `05:30 PM` | Scheduled 30-minute OPD consultation slot window. |
| 8 | `OPD_Session` | Category | `Morning OPD`, `Evening OPD` | Clinic session classification based on `Slot_Time`. |
| 9 | `State` | Category | `Gujarat`, `Maharashtra`, `Delhi NCR`, `Karnataka`, `Tamil Nadu`, `Rajasthan` | Regional Indian state of the Zydus hospital unit. |
| 10 | `Facility_City` | Category | `Ahmedabad`, `Bhuj`, `Mumbai`, `New Delhi`, `Bengaluru`, `Chennai`, `Jaipur` | Municipal city of the hospital facility. |
| 11 | `Hospital_Unit` | Category | `Zydus Hospitals - <City> (<Locality>)` | Specific facility unit across the 7-unit hypothetical network. |
| 12 | `Department` | Category | `Cardiology`, `Neurology`, `Orthopedics`, `Pediatrics`, `ENT`, `Dermatology`, `Gynecology & Obstetrics`, `General Medicine` | Outpatient clinical specialty department. |
| 13 | `Visit_Type` | Category | `Initial Consultation`, `Follow-Up Visit` | Consultation type (`62%` Initial / `38%` Follow-Up). |
| 14 | `Booking_Channel` | Category | `Phone Call`, `Walk-In Desk`, `Mobile App`, `Web Portal`, `WhatsApp Bot` | Booking channel (`74.04%` digital self-service in To-Be). |
| 15 | `ABHA_ID_Linked` | Boolean Flag | `Yes`, `No` | Whether patient linked Ayushman Bharat Health Account ID (`18.08%` -> `84.08%`). |
| 16 | `Reminder_Status` | Category | `No Automated Reminder`, `Confirmed via WhatsApp/SMS`, `Cancelled via 1-Click Reminder`, `Cancelled via App/Portal`, `Reminder Delivered - No Reply`, `Reminder Delivered - Unresponsive` | Interaction status with automated T-24h / T-2h reminders. |
| 17 | `Appointment_Status` | Category | `Completed`, `Cancelled`, `No-Show` | Terminal outcome of the appointment record. |
| 18 | `Waitlist_Slot_Reallocated` | Category | `Yes`, `No`, `Not Applicable` | Whether a `Cancelled` slot was refilled via the dynamic waitlist (`4.83%` -> `78.17%`). |
| 19 | `Double_Booking_Conflict` | Boolean Flag | `Yes`, `No` | Concurrent slot booking conflict flag (`14.76%` As-Is -> `0.00%` To-Be). |
| 20 | `Payment_Mode` | Category | `Cash at OPD`, `UPI (Pre-Paid)`, `Card at OPD`, `Card/NetBanking`, `UPI at OPD` | Simulated payment instrument. |
| 21 | `Consultation_Fee_INR` | Integer (₹) | `₹500` to `₹1,200` | Specialty-specific standard OPD consultation tariff in INR. |
| 22 | `Realized_Revenue_INR` | Integer (₹) | `₹0` or `Consultation_Fee_INR` | Simulated revenue realized from `Completed` appointments. |
| 23 | `No_Show_Revenue_Loss_INR` | Integer (₹) | `₹0` or `Consultation_Fee_INR` | Simulated unbilled slot value from `No-Show` appointments. |
| 24 | `Booking_Turnaround_Mins` | Float (Mins) | `0.5` to `24.0` mins | Time taken to complete appointment reservation (`11.36m` -> `1.79m`). |
| 25 | `OPD_Waiting_Hall_Mins` | Float (Mins) | `0.0` to `115.0` mins | Lobby waiting time for `Completed` visits (`48.52m` -> `14.25m`). |
| 26 | `Patient_CSAT_Score_1to5` | Integer (1–5) | `1`, `2`, `3`, `4`, `5` | Simulated post-appointment satisfaction rating (`2.61` -> `4.19`). |
