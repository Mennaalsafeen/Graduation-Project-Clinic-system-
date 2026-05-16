# Business Requirements Document (BRD) - Dental Clinic System

## 1. Project Overview
**Project Name:** Dental Clinic Appointment Management System
**Description:** A professional digital solution to automate dental clinic workflows.
**Target Language:** The System Interface (UI) will be fully in **Arabic**.

## 2. Problem Statement
* Conflict in appointments due to manual logs.
* Difficulty in tracking patient medical history and dental charts.
* Lack of organized financial reporting and inventory alerts.

## 3. Project Objectives
* **Full Automation:** Eliminate manual scheduling errors.
* **Digital EHR:** Provide a visual dental map for precise diagnosis.
* **Localization:** Deliver a user-friendly Arabic interface for local clinic staff and patients.

## 4. Project Scope
* **In-Scope:** User Roles, Smart Dashboard, Appointment Engine, Visual Dental Chart (EHR), Billing & Financial Reports, Inventory Tracking, and Patient Feedback.
* **Out-of-Scope:** Mobile Apps (System is Responsive Web), Third-party Insurance API.

## 5. Stakeholders & User Roles
* **Admin:** Full system control and financial oversight.
* **Doctor:** Clinical management and patient records.
* **Receptionist:** Operations, check-ins, and manual scheduling overrides.
* **Patient:** Booking, viewing history, and feedback.

## 6. Functional Requirements
### A. Appointment Management
* **Working Hours:** System strictly allows bookings only between **9:00 AM and 8:00 PM**.
* **Smart Cancellation Policy:**
    * Patients can cancel automatically if the appointment is more than **24 hours** away.
    * If less than 24 hours remains, the patient must contact the **Receptionist** for manual cancellation.

### B. Financial Reporting (Admin Only)
* **Daily/Monthly Income:** Total revenue tracking.
* **Doctor Productivity:** Revenue generated per doctor and number of cases.
* **Debt Tracking:** List of outstanding balances/unpaid invoices.
* **Service Analytics:** Statistics on the most requested dental services.

### C. Clinical Features
* **Visual Dental Chart:** Interactive map to document procedures per tooth.
* **Inventory Alerts:** Notifications for low medical supplies.

## 7. Non-Functional Requirements
* **Language:** UI must be localized in **Arabic**.
* **Performance:** Page load time under 2 seconds.
* **Security:** Role-based access control (RBAC).

## 8. Technical Constraints
* **Design:** Google Stitch.
* **Conversion:** Antigravity to Razor Views.
* **Frontend:** HTML, CSS, Bootstrap, Vanilla JS (No Frameworks like React/Vue).
* **Backend:** ASP.NET Core MVC.
* **Database:** SQLite with Entity Framework Core.

## 9. Business Rules
1. **No Overlapping:** Doctors cannot have two patients in the same time slot.
2. **UI Integrity:** The system must be fully RTL (Right-to-Left) compatible for Arabic.
3. **Data Privacy:** Only Doctors and Admins can view detailed medical diagnoses.

## 10. Success Criteria
* 100% elimination of double-booked appointments.
* Successful generation of accurate monthly financial reports.
* Full system adoption with the Arabic interface.
