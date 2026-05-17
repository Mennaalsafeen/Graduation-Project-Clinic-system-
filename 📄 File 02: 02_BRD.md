# 📁 File 02: Business Requirements Document (02_BRD.md)

## 1. Project Overview
* Project Name: Dental Clinic Appointment Management System
* Description: A professional, integrated digital solution designed to streamline and automate the daily clinical, operational, and financial workflows of dental clinics. The system replaces traditional paper-based logs with a smart, fully responsive web interface that connects patients, doctors, and front-desk staff while delivering comprehensive administrative insights.
* Target Language: The System Interface (UI) is fully localized in Arabic, supporting native Right-to-Left (RTL) rendering.

## 2. Problem Statement
* Appointment Conflicts: Manual scheduling logs cause critical overlapping, double-bookings, and human errors.
* Clinical Tracking Complexities: Difficulty in seamlessly archiving and retrieving historical patient medical records and diagnostic dental charts.
* Operational Blind Spots: Lack of automated financial analytics, data-driven revenue visibility, and low-inventory tracking/alerts.

## 3. Project Objectives
* Full Automation: Implement a strict scheduling engine to 100% eliminate manual time-slot conflicts.
* Digital EHR Enrichment: Deliver an interactive, visual dental map for high-precision charting and diagnosis archiving.
* Localization: Deliver a user-friendly, fully native Arabic UI to eliminate technical barriers for local medical staff and patients.

## 4. Project Scope
* In-Scope: Identity Architecture, Smart Dashboard, Advanced Appointment Engine, Visual Dental Chart (EHR), Invoicing & Payments, Materials Inventory Logs, and Patient Feedback Collection.
* Out-of-Scope: Native Mobile Applications (the system is built exclusively as a fully Responsive Web Application), and Third-party Insurance Provider API Integrations.

## 5. Stakeholders & User Roles
The system structures authorization via a Role-Based Access Control (RBAC) model, establishing clear separation between account credentials (Identity) and functional data files:
* Admin: The business owner/clinic manager. Holds full system authority and oversight over clinic performance and financial reports.
* Doctor: Medical practitioners. Manages personal calendars, reads historical patient data, documents diagnoses, and charts surgical/cosmetic teeth operations.
* Receptionist: The operational center. Manages physical clinic check-ins, inputs new patient profiles, overrides schedules manually when required, and processes billing invoices.
* Patient: Clinic consumers. Uses self-service tools to explore available slots, request/cancel appointments, and review personal invoices and history.

## 6. Functional Requirements

### A. Appointment Engine & Scheduling Rules
* Working Hours Boundary: The booking matrix strictly restricts reservation entries to between 9:00 AM and 8:00 PM.
* Smart Cancellation Policy:
  * Patients can execute automated cancellations if the targeted appointment is more than 24 hours away.
  * Within the 24-hour window, the self-service cancellation option is locked; the patient must explicitly contact a Receptionist for a manual operational override.

### B. Financial Reporting & Analytics (Admin Only)
* Revenue Tracking: Real-time generation of daily, monthly, and cyclical gross income.
* Clinical Productivity Metrics: Statistical evaluation of revenue generated per doctor against total active cases processed.
* Debt / Outstanding Balances Ledger: A clean, automated list of all unpaid or partially settled patient invoices.
* Service Market Share: Analytics displaying charts on the most requested dental services (e.g., Orthodontics, Surgery, Cosmetic).

### C. Clinical Record Modules
* Visual Dental Charting: An interactive visual dental component mapping procedures explicitly to any of the 32 adult teeth.
* Inventory Management & Supply Alerts: Real-time deduction of medical tools and consumables, throwing dashboard warnings if quantity falls below defined minimum thresholds.
* ## 7. Non-Functional Requirements
* Language Compatibility: The presentation layer must fully support native Arabic translation and RTL layouts.
* Performance Benchmark: Page load times must remain strictly under 2.0 seconds under peak operational data queries.
* Security Matrix: Implementation of secure, role-based access controls (RBAC) preventing unauthorized endpoint exploration.

## 8. Technical Constraints
* Design Prototype Mapping: Google Stitch layout schema.
* Conversion Target: Translating design views into native .NET Razor Views.
* Frontend Components: Built using standard HTML, CSS, Bootstrap, and Vanilla JS (Strictly No Frontend Frameworks like React, Angular, or Vue).
* Backend Architecture: ASP.NET Core MVC framework.
* Database Management Engine: SQLite utilizing Entity Framework Core as the Object-Relational Mapper (ORM).

## 9. Business Rules
* Time-Slot Overlap Prevention: The core database pipeline acts as an atomic checker, blocking a DoctorId from saving two concurrent intersecting appointment intervals.
* UI Structural Integrity: All pages must dynamically adapt to an RTL structure, preventing graphical distortion when rendering Arabic typography.
* Medical Record Privacy Boundary: Receptionists have operational clearance to see appointment states but are strictly blocked from reading detailed diagnostic annotations or interactive dental chart histories. Only Doctors and Admins can view health summaries.
* Financial Integrity: Once an invoice status transitions to "Paid", hard deletion is permanently blocked at the database level. Financial adjustments can only occur via a formal "Refund" triggered by an Admin, which automatically logs an entry in the audit trail.

## 10. Use Cases Summary
To ensure smooth translation to code, the system maps operations via the following core functional use cases:

| Use Case ID | Use Case Name | Primary Actor | Description |
| :--- | :--- | :--- | :--- |
| UC-01 | Register New Patient Profile | Receptionist | Creates a system User credential linked to a distinct PatientProfile record. |
| UC-02 | Schedule Appointment | Patient / Receptionist | Searches available doctor timeslots within working hours and reserves an open slot. |
| UC-03 | Cancel Appointment | Patient / Receptionist | Cancels a slot automatically if >24 hours, or triggers manual override via Receptionist if <24 hours. |
| UC-04 | Update Visual Dental Chart | Doctor | Interacts with the SVG jaw map to log a medical condition or treatment against specific teeth. |
| UC-05 | Generate Digital Invoice | Receptionist | Automatically creates a billing invoice tied 1:1 with a completed appointment file. |
| UC-06 | Track Low Inventory Stocks | Admin | Monitors consumable counts and receives real-time alerts if counts dip below the threshold. |
| UC-07 | Review Financial Dashboard | Admin | Reviews monthly clinic income statements, doctor productivity metrics, and unpaid debts. |

## 11. Success Criteria
* 100% Elimination of Scheduling Errors: Zero overlapping appointments or double-booked time windows allowed into the production database.
* Automated Financial Reporting: Flawless generation of accurate monthly financial sheets without manual math aggregation.
* System Adoption: Full workflow execution by clinic staff and patients using the localized Arabic interface.
