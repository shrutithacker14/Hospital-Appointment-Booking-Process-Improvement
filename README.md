# Zydus Hospitals — Outpatient Appointment Booking & Queue Optimization

**Portfolio Case Study | Business Analysis (BABOK v3 Aligned) | Healthcare Operations & Digital Transformation**  
**Author:** Shruti Thacker ([@shrutithacker14](https://github.com/shrutithacker14))

---

## 1. Project Overview

This repository presents an end-to-end **Business Analysis portfolio case study** modeled hypothetically around **Zydus Hospitals** across a 7-unit multispecialty regional footprint in India (**Gujarat [Ahmedabad & Bhuj], Maharashtra [Mumbai], Delhi NCR [New Delhi], Karnataka [Bengaluru], Tamil Nadu [Chennai], and Rajasthan [Jaipur]**).

It demonstrates how a Business Analyst structures operational discovery, models `As-Is` and `To-Be` BPMN/swimlane workflows, authors a **Business Requirements Document (BRD v2.1)**, conducts **Mendelow Power-Interest & RACI governance mapping**, writes **Agile Epics and User Stories with Gherkin Acceptance Criteria**, establishes a **bi-directional Requirements Traceability Matrix (RTM) & UAT Test Plan**, and evaluates **synthetic cohort KPIs** in Excel.

> **Portfolio Governance & Disclaimer:** This is a self-directed, hypothetical portfolio case study created for Business Analysis demonstration. It is not commissioned, endorsed, or supplied by Zydus Hospitals. The 5,000-row dataset is synthetic and contains zero real patient or operational records. All UAT scenarios are documented test plans (`Status: Not Run`), and cohort metrics represent descriptive comparisons of constructed scenarios rather than causal post-implementation proof.

---

## 2. Business Problem & Scenario Context

In the baseline (`Pre-Implementation As-Is`) scenario, outpatient department (OPD) scheduling relies on fragmented telephone lines (`60.40%`) and walk-in reception desks (`39.60%`) supported by local spreadsheets and paper registers. Key operational pain points modeled in the baseline cohort include:
- **High Booking Turnaround Time:** `11.36 minutes` mean booking turnaround across manual channels.
- **Elevated OPD No-Show Rate:** `23.92%` (`598 / 2,500` records), representing `₹4,45,250` in simulated unutilized slot value.
- **Concurrent Double-Booking Conflicts:** `14.76%` (`369 / 2,500` records) caused by simultaneous reception and phone entries without real-time slot locking.
- **Minimal Cancelled Slot Recovery:** Only `4.83%` (`18 / 373`) of cancelled appointments are re-allocated manually.
- **Severe OPD Lobby Congestion:** `48.52 minutes` mean waiting hall time among completed visits, resulting in a `2.61 / 5.00` synthetic patient CSAT score.

---

## 3. Synthetic Cohort KPI Comparison (`n = 5,000` Records)

| KPI ID | Operational & Patient Experience Metric | Pre-Implementation (`As-Is` Cohort) | Post-Implementation (`To-Be` Cohort) | Net Variance / Shift | Target (BRD Proposal) |
| :--- | :--- | ---: | ---: | ---: | :--- |
| **KPI-01** | **Synthetic Cohort Sample Size** | 2,500 records | 2,500 records | 5,000 total records | Balanced cohort design |
| **KPI-02** | **Completed OPD Consultation Share (%)** | 61.16% (1,529) | 84.84% (2,121) | **+23.68% pts** | >= 82.0% |
| **KPI-03** | **OPD Patient No-Show Share (%)** | 23.92% (598) | 7.28% (182) | **-16.64% pts** | < 8.0% |
| **KPI-04** | **OPD Cancellation Share (%)** | 14.92% (373) | 7.88% (197) | **-7.04% pts** | < 10.0% |
| **KPI-05** | **Double-Booking Slot Conflict Share (%)** | 14.76% (369) | 0.00% (0) | **-14.76% pts** | 0.0% (Redis 300s lock) |
| **KPI-06** | **Digital Self-Service Booking Share (%)** | 0.00% (0) | 74.04% (1,851) | **+74.04% pts** | >= 70.0% |
| **KPI-07** | **Cancelled Slot Waitlist Re-Fill Rate (%)** | 4.83% (18 / 373) | 78.17% (154 / 197) | **+73.34% pts** | >= 75.0% |
| **KPI-08** | **ABHA Health ID Linkage Rate (%)** | 18.08% (452) | 84.08% (2,102) | **+66.00% pts** | >= 80.0% |
| **KPI-09** | **Mean Booking Turnaround Time** | 11.36 min | 1.79 min | **-84.24% rel.** | < 2.0 min |
| **KPI-10** | **Mean OPD Waiting Hall Time (Completed)** | 48.52 min | 14.25 min | **-70.63% rel.** | < 15.0 min |
| **KPI-11** | **Mean Synthetic Patient CSAT (1–5)** | 2.61 / 5.00 | 4.19 / 5.00 | **+1.58 pts** | >= 4.00 / 5.00 |
| **KPI-12** | **Simulated Realized OPD Revenue (INR)** | ₹11,70,000 | ₹16,03,250 | **+37.03% (+₹4,33,250)** | Illustrative sample total |
| **KPI-13** | **Simulated Unrecovered No-Show Loss (INR)** | ₹4,45,250 | ₹1,39,700 | **-68.62% (-₹3,05,550)** | Illustrative sample total |

---

## 4. Repository Structure & Deliverables

- `01_Business_Requirements_Document/`
  - [`BRD_Hospital_Appointment_Booking_v2.1.md`](./01_Business_Requirements_Document/BRD_Hospital_Appointment_Booking_v2.1.md) — Complete Business Requirements Document (`FR-01` to `FR-12`, `NFR-01` to `NFR-04`, KPI targets, and scope governance).
  - [`BRD_Hospital_Appointment_Booking_v2.1.docx`](./01_Business_Requirements_Document/BRD_Hospital_Appointment_Booking_v2.1.docx) — Executive Word version formatted for stakeholder review.
- `02_Process_Maps_AsIs_ToBe/`
  - [`As_Is_Manual_Booking_Flow.png`](./02_Process_Maps_AsIs_ToBe/As_Is_Manual_Booking_Flow.png) — Baseline manual appointment booking swimlane diagram.
  - [`To_Be_Automated_Booking_Flow.png`](./02_Process_Maps_AsIs_ToBe/To_Be_Automated_Booking_Flow.png) — Proposed omnichannel booking, Redis slot lock, and waitlist promotion swimlane diagram.
  - [`Process_Architecture_Documentation.md`](./02_Process_Maps_AsIs_ToBe/Process_Architecture_Documentation.md) — Process comparison table and Mermaid.js workflow architecture.
- `03_Stakeholder_Analysis/`
  - [`Stakeholder_Register_and_RACI_Matrix.xlsx`](./03_Stakeholder_Analysis/Stakeholder_Register_and_RACI_Matrix.xlsx) — 8 healthcare stakeholder personas (`SH-01` to `SH-08`), Mendelow Power-Interest classification, and RACI governance matrix.
  - [`Stakeholder_Analysis_Summary.md`](./03_Stakeholder_Analysis/Stakeholder_Analysis_Summary.md) — Markdown summary of stakeholder governance.
- `04_Agile_User_Stories_and_AC/`
  - [`Agile_User_Stories_and_Acceptance_Criteria.xlsx`](./04_Agile_User_Stories_and_AC/Agile_User_Stories_and_Acceptance_Criteria.xlsx) — 5 Epics, 12 User Stories (`US-01` to `US-12`, 70 Story Points across 4 Sprints), MoSCoW prioritization, and Gherkin (`Given/When/Then`) acceptance criteria.
  - [`Agile_User_Stories_Backlog.md`](./04_Agile_User_Stories_and_AC/Agile_User_Stories_Backlog.md) — Backlog documentation in Markdown.
- `05_UAT_Test_Cases_and_RTM/`
  - [`UAT_Test_Cases_and_Traceability_Matrix.xlsx`](./05_UAT_Test_Cases_and_RTM/UAT_Test_Cases_and_Traceability_Matrix.xlsx) — 14 end-to-end UAT test cases (`UAT-TC-01` to `UAT-TC-14`, status `Not Run`) and complete Requirements Traceability Matrix (`FR-01` to `FR-12`).
  - [`UAT_Plan_and_RTM_Summary.md`](./05_UAT_Test_Cases_and_RTM/UAT_Plan_and_RTM_Summary.md) — UAT governance plan, entry/exit criteria, and open pre-implementation decisions.
- `06_Data_Analysis_and_KPI_Impact/`
  - [`Zydus_Hospital_Appointment_Dataset_5000.csv`](./06_Data_Analysis_and_KPI_Impact/Zydus_Hospital_Appointment_Dataset_5000.csv) (and [`Indian_Hospital_Appointment_Dataset_5000.csv`](./06_Data_Analysis_and_KPI_Impact/Indian_Hospital_Appointment_Dataset_5000.csv)) — 5,000-row, 26-column synthetic dataset in INR (`₹`) across 7 Zydus facility units.
  - [`KPI_Impact_and_ROI_Analysis_Dashboard.xlsx`](./06_Data_Analysis_and_KPI_Impact/KPI_Impact_and_ROI_Analysis_Dashboard.xlsx) — Multi-tab formula-driven workbook (`Executive_KPI_Comparison`, `State_Wise_Performance_INR`, `Department_and_Channel_Mix`) with embedded openpyxl bar chart.
  - [`DATA_DICTIONARY.md`](./06_Data_Analysis_and_KPI_Impact/DATA_DICTIONARY.md) & [`DATASET_AND_KPI_METHODOLOGY.md`](./06_Data_Analysis_and_KPI_Impact/DATASET_AND_KPI_METHODOLOGY.md) — Field-level schema definitions and calculation methodology.

---

## 5. Quick Start & Repository Clone Instructions

```bash
git clone https://github.com/shrutithacker14/Hospital-Appointment-Booking-Process-Improvement.git
cd Hospital-Appointment-Booking-Process-Improvement
```

## 6. Author

**Shruti Thacker**  
Business Analyst Portfolio | GitHub: [@shrutithacker14](https://github.com/shrutithacker14)
