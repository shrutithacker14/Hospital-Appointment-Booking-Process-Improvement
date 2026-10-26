# Dataset and KPI Methodology — Zydus Hospitals Portfolio Case Study

## 1. Dataset Overview & Integrity Checks
`Zydus_Hospital_Appointment_Dataset_5000.csv` (also saved as `Indian_Hospital_Appointment_Dataset_5000.csv` for backward compatibility) is a **5,000-row, 26-column synthetic dataset** divided into two balanced 2,500-row cohorts:
- `Pre-Implementation (As-Is)` (`n = 2,500`, simulated `Q4 2025` baseline window)
- `Post-Implementation (To-Be)` (`n = 2,500`, simulated `Q1 2026` omnichannel window)

### Structural Validation Performed:
- **Zero Missing Values:** All 5,000 rows x 26 columns are 100% populated.
- **Unique Primary Key:** 5,000 unique `Appointment_ID` records (`APT-100001` to `APT-105000`).
- **Regional & Facility Mapping:** Consistent 1-to-1 mapping across 6 Indian states and 7 hypothetical Zydus Hospital units (`Ahmedabad`, `Bhuj`, `Mumbai`, `New Delhi`, `Bengaluru`, `Chennai`, `Jaipur`).
- **Tariff & Revenue Consistency:** `Realized_Revenue_INR = Consultation_Fee_INR` when `Appointment_Status = Completed` (else `₹0`); `No_Show_Revenue_Loss_INR = Consultation_Fee_INR` when `Appointment_Status = No-Show` (else `₹0`).

## 2. KPI Formulas & Definitions
1. **Completed Share (%):** `COUNTIF(Appointment_Status = "Completed") / 2,500` (`61.16%` As-Is vs. `84.84%` To-Be).
2. **No-Show Share (%):** `COUNTIF(Appointment_Status = "No-Show") / 2,500` (`23.92%` As-Is vs. `7.28%` To-Be).
3. **Cancellation Share (%):** `COUNTIF(Appointment_Status = "Cancelled") / 2,500` (`14.92%` As-Is vs. `7.88%` To-Be).
4. **Double-Booking Conflict Share (%):** `COUNTIF(Double_Booking_Conflict = "Yes") / 2,500` (`14.76%` As-Is vs. `0.00%` To-Be).
5. **Digital Self-Service Share (%):** `COUNTIF(Booking_Channel IN {"Mobile App", "Web Portal", "WhatsApp Bot"}) / 2,500` (`0.00%` As-Is vs. `74.04%` To-Be).
6. **Cancelled Slot Waitlist Re-Fill Rate (%):** `COUNTIFS(Appointment_Status = "Cancelled", Waitlist_Slot_Reallocated = "Yes") / COUNTIF(Appointment_Status = "Cancelled")` (`4.83%` [18/373] As-Is vs. `78.17%` [154/197] To-Be).
7. **ABHA Health ID Linkage Rate (%):** `COUNTIF(ABHA_ID_Linked = "Yes") / 2,500` (`18.08%` As-Is vs. `84.08%` To-Be).
8. **Mean Booking Turnaround (Mins):** Arithmetic mean of `Booking_Turnaround_Mins` across all 2,500 cohort records (`11.36 min` As-Is vs. `1.79 min` To-Be).
9. **Mean OPD Waiting Hall Time (Mins):** Arithmetic mean of `OPD_Waiting_Hall_Mins` restricted to `Appointment_Status = "Completed"` records (`48.52 min` As-Is vs. `14.25 min` To-Be).
