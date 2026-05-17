# 📁 File 06: System Use Cases Mapping (06_USE_CASES.md)

## 1. Antigravity Prompt (Developer Instruction)
> Instruction: Read 06_USE_CASES.md. Map each functional use case to its respective ASP.NET Core Controller, Action name, HTTP Method, and Razor View file. 
> Crucial Architectural Rule: All alternative scenarios and validation errors must be evaluated by invoking the designated Methods inside the Service Layer (e.g., AppointmentService). The Controllers must only handle the orchestration, return appropriate ModelState errors to the Razor View, or execute redirects.

---

## 2. Technical Mapping Matrix
The system maps the 10 core user-system interactions via the following routing blueprint:

| UC ID | Use Case Name | Controller Name | Action Name | HTTP Method | View File (.cshtml) |
| :--- | :--- | :--- | :---: | :---: | :--- |
| UC-01 | Patient Registration | AccountController | Register | GET / POST | Views/Account/Register |
| UC-02 | Patient Authentication | AccountController | Login | GET / POST | Views/Account/Login |
| UC-03 | Book Appointment | AppointmentsController | Create | GET / POST | Views/Appointments/Create |
| UC-04 | View My Appointments | AppointmentsController | Index | GET | Views/Appointments/Index |
| UC-05 | Cancel Appointment | AppointmentsController | Cancel | POST | Views/Appointments/Index (Redirect) |
| UC-06 | Doctor Schedule Tracking | AppointmentsController | DoctorSchedule | GET | Views/Appointments/DoctorSchedule |
| UC-07 | Update Visual Dental Chart | ClinicalRecordsController | UpdateChart | GET / POST | Views/ClinicalRecords/UpdateChart |
| UC-08 | Admin Staff Management | AdminController | ManageStaff | GET / POST | Views/Admin/ManageStaff |
| UC-09 | Materials Inventory Control | InventoryController | Dashboard | GET / POST | Views/Inventory/Dashboard |
| UC-10 | Financial Reporting Metrics | ReportsController | FinancialSummary | GET | Views/Reports/FinancialSummary |

---

## 3. Detailed Operational Flows & Alternative Scenarios

### UC-01: Patient Registration
* Main Flow: Receptionist or Patient inputs National ID, Full Name, Phone, and Credentials. System persists records into Users and PatientProfiles.
* Alternative Scenario (Error Handling): If the input National ID or Email already exists in the ledger database, the pipeline flags a conflict, blocking execution and returning a "This profile is already registered" message to the UI.

### UC-02: Patient Authentication
* Main Flow: User enters Email and Password. System evaluates cryptography hashes and sets up the claims session.
* Alternative Scenario (Error Handling): Invalid password hash or email lookup failure prompts an immediate authentication denial, returning \"Incorrect Email or Password\" without shifting views.

### UC-03: Book Appointment
* Main Flow: Patient selects Doctor, Target Date, and Available Time Window. Receptionist determines procedure scope.
* Alternative Scenario A (Overlap Conflict): System cross-checks slots. If the doctor has a pre-existing commitment intersecting that timeframe, operation blocks, rendering "Selected timeslot is unavailable".
* Alternative Scenario B (Operational Window Error): Request falls outside the 09:00 AM - 08:00 PM clinical boundary; booking engine locks and rejects entry.

### UC-04: View My Appointments
* Main Flow: Authenticated Patient accesses profile, pulling records matched strictly to their specific PatientId.
* Alternative Scenario: Database return is null/empty; UI gracefully renders an Arabic notification: "لا توجد مواعيد سابقة مسجلة" (No records found).

### UC-05: Cancel Appointment
* Main Flow: Patient hits cancel on a slot scheduled for more than 24 hours in the future. Status updates to Cancelled.
* Alternative Scenario (Business Constraint): Time delta to appointment is less than 24 hours. The portal hard-locks the UI cancel interaction, prompting: "يرجى التواصل مع الاستقبال لإلغاء الموعد طارئاً".
* ### UC-06: Doctor Schedule Tracking
* Main Flow: Doctor authenticates and views an active daily agenda showing assigned patients ordered chronologically.
* Alternative Scenario: No scheduled visits exist for the selected working day; UI displays "لا يوجد مواعيد مجدولة لليوم".

### UC-07: Update Visual Dental Chart
* Main Flow: Doctor updates visit state to Completed and colorizes targeted tooth paths on the interactive Arabic SVG template.
* Alternative Scenario (Validation Error): Incoming structural database post references a tooth sequence outside the 1–32 adult scope; application safely interrupts request and returns an invalid identifier error.

### UC-08: Admin Staff Management
* Main Flow: Admin instantiates new corporate accounts, selecting roles (Doctor, Receptionist) and mapping system identities.
* Alternative Scenario: Attempting to build a Senior Doctor profile without setting up mandatory Multi-Factor Authentication (2FA) locks setup flow, forcing a 2FA credential initialization screen.

### UC-09: Materials Inventory Control
* Main Flow: Admin adjusts consumable numbers. System fires checks comparing item count parameters against MinimumThreshold limits.
* Alternative Scenario (Smart Alerts): Balance level drops equal to or below threshold values; the backend asynchronously forces an urgent dashboard icon update AND triggers an SMTP automated notification email.

### UC-10: Financial Reporting Metrics
* Main Flow: Admin triggers revenue ledger aggregation components to view gross clinical and operational income spreadsheets.
* Alternative Scenario: System discovers outstanding balances; the reporting view dynamically isolates and populates these items into a distinct "Debt Tracking" warning ledger.
