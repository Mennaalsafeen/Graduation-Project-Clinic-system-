# 📁 File 03: User Roles and Permissions (03_USER_ROLES_AND_PERMISSIONS.md)

## 1. Introduction
The Dental Clinic Appointment Management System implements a strict Role-Based Access Control (RBAC) architecture. This blueprint defines explicit security contracts to safeguard data integrity, maintain patient confidentiality (HIPAA-aligned privacy boundaries), and streamline clinical operations. 
* UI Localization Note: While system documentation is maintained in English, the actual Presentation Layer (UI) is fully localized in Arabic with native Right-to-Left (RTL) layout rendering.

## 2. User Roles Definition & Access Contracts
To eliminate security gray areas, every operational role is governed by an explicit contract defining both its authorizations (CAN DO) and absolute boundary restrictions (CANNOT DO).

### A. System Admin
* Description: The business owner, clinic director, or system manager.
* Access Level: Full System Access.
* CAN DO: Full CRUD capabilities over staff accounts, service price configurations, financial ledgers, and system audit logs.
* CANNOT DO List: * Cannot bypass the mandatory Two-Factor Authentication (2FA) enforcement protocol.

### B. Senior Doctor
* Description: Head of the clinic's medical staff and clinical quality supervisor.
* Access Level: Full Clinical Access.
* CAN DO: Read and update all clinical records and dental charts across the clinic; review aggregated inventory metrics and patient feedback.
* CANNOT DO List:
  * CANNOT modify service base prices or alter clinic financial configurations.
  * CANNOT delete or modify structural staff login credentials.
  * CANNOT delete any invoice marked as "Paid".

### C. Doctor
* Description: General practitioners and assigned dentists.
* Access Level: Standard Clinical Access.
* CAN DO: Create and update clinical records, diagnoses, and visual dental charts ONLY for patients explicitly assigned to their care or appointments.
* CANNOT DO List:
  * CANNOT read or update clinical records/dental charts of patients assigned to other doctors.
  * CANNOT access financial reports, clinic revenue dashboards, or billing structures.
  * CANNOT alter inventory threshold configurations.

### D. Receptionist
* Description: Front-desk operations, patient onboarding, and billing coordinator.
* Access Level: Operational Access.
* CAN DO: Register new patients, manage appointment check-ins, execute scheduling overrides, and issue invoices/collect payments.
* CANNOT DO List:
  * CANNOT view medical diagnoses, clinical descriptions, or detailed visual dental charts (Privacy Boundary).
  * CANNOT delete financial transactions or modify base service rates.
  * CANNOT view system audit logs or administrative dashboards.

### E. Patient
* Description: System end-consumer (Self-Service portal).
* Access Level: Self-Service Access.
* CAN DO: Register accounts, book appointments, self-cancel slots (>24 hours notice), review personal invoice balances, and submit feedback.
* CANNOT DO List:
  * CANNOT view any clinical files, records, or calendars belonging to other patients.
  * CANNOT bypass scheduling restrictions (e.g., booking slots outside 9:00 AM - 8:00 PM).
  * CANNOT view clinic-wide metrics, inventory data, billing systems, or staff registries.

---

## 3. Detailed Permissions Matrix (CRUD)
*(Key: C: Create, R: Read, U: Update, D: Delete, —: Explicitly Locked/Forbidden)*

| Feature / Module | System Admin | Senior Doctor | Doctor | Receptionist | Patient |
| :--- | :---: | :---: | :---: | :---: | :---: |
| Staff Accounts | CRUD | R | — | — | — |
| Clinical Records (EHR) | R | CRUD | CRU* | R (Status Only) | — |
| Visual Dental Chart | R | CRUD | CRU* | — | — |
| Appointment Engine | CRUD | R | R | CRUD | CRU (Self Only) |
| Financial Reports | CRUD | R | — | — | — |
| Invoicing & Payments | CRUD | — | — | CRU | R (Self Only) |
| Inventory & Alerts | CRUD | R | R | RU | — |
| Patient Feedback | R | R | — | — | CR |
| Audit Logs | R | — | — | — | — |
* *Enforced constraint: Standard Doctors are restricted to updating entities bounded to their explicit Patient-Doctor assignment map.*

---

## 4. Advanced E-Business Security Controls
* Traceable Audit Trail: Every structural change (Create, Update, Delete) triggers an automated interceptor that logs the user context, action vector, affected entity, and a UTC timestamp.
* Mandatory Multi-Factor Guard (2FA): Identity endpoints serving System Admin and Senior Doctor accounts explicitly deny access tokens until an out-of-band verification token (SMS/Email) is cleared.
* Hardened Session Timeout: Inactive client sessions are dropped automatically after exactly 30 minutes of mouse/keyboard dormancy to secure open terminals on shared clinic workstations.
* Financial Anti-Tampering Rule: Once an invoice state transitions to Paid, the data pipeline hard-locks the row. Deletions are forbidden. Reversals can only execute via an administrative Refund transaction, which automatically builds a record in the AuditLogs.
