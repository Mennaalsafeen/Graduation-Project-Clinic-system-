# 📄 File 06: 06_USE_CASES.md → Antigravity

## 1. Antigravity Prompt (Developer Instruction)
> **Instruction:** Read 06. Map each use case to a controller name, action name, HTTP method, and view file. Ensure all alternative scenarios are handled via validation logic in the controllers.

## 2. Technical Mapping Table
| UC ID | Use Case Name | Controller | Action | Method | View File |
| :--- | :--- | :--- | :--- | :--- | :--- |
| UC-01 | Patient Register | AccountController | Register | GET/POST | Register.cshtml |
| UC-02 | Patient Login | AccountController | Login | GET/POST | Login.cshtml |
| UC-03 | Book Appointment | AppointmentController | Create | GET/POST | Create.cshtml |
| UC-04 | View My Appointments | AppointmentController | MyHistory | GET | MyHistory.cshtml |
| UC-05 | Cancel Appointment | AppointmentController | Cancel | POST | MyHistory.cshtml |
| UC-06 | Doctor View Schedule | DoctorController | Schedule | GET | Schedule.cshtml |
| UC-07 | Update Status & Chart | ClinicalController | UpdateRecord | POST | PatientDetails.cshtml |
| UC-08 | Admin Manage Staff | AdminController | ManageStaff | GET/POST | ManageStaff.cshtml |
| UC-09 | Manage Inventory | InventoryController | Dashboard | GET/POST | Inventory.cshtml |
| UC-10 | Financial Reports | AdminController | Reports | GET | Reports.cshtml |

## 3. Detailed Use Case Scenarios

### UC-01: Patient Register
*   **Main Flow:** User enters National ID, Name, and Phone. System validates and saves to `Patients` table.
*   **Alternative Scenario (Error):** National ID already exists in the database; System returns "ID already registered" error.

### UC-02: Patient Login
*   **Main Flow:** User enters Email/Password. System verifies credentials and creates a session.
*   **Alternative Scenario (Error):** Invalid credentials; System displays "Incorrect Email or Password" message.

### UC-03: Book Appointment
*   **Main Flow:** Patient selects Doctor, Date, and Time. Receptionist confirms the duration.
*   **Alternative Scenario A (Conflict):** Selected time overlaps with another appointment; System blocks the save.
*   **Alternative Scenario B (Time):** Selected time is outside 09:00 AM - 08:00 PM; System prevents booking.

### UC-04: View My Appointments
*   **Main Flow:** Patient logs in and views a list of their upcoming and past visits.
*   **Alternative Scenario:** No records found; System displays "No previous appointments found."

### UC-05: Cancel Appointment
*   **Main Flow:** Patient clicks cancel > 24 hours before the appointment. Status changes to "Cancelled".
*   **Alternative Scenario (Constraint):** Cancellation attempt < 24 hours; "Cancel" button is disabled; System displays "Contact Reception to cancel."

### UC-06: Doctor View Schedule
*   **Main Flow:** Doctor views the daily list of patients assigned to them.
*   **Alternative Scenario:** System is empty for the day; Display "No appointments scheduled for today."

### UC-07: Update Status & Clinical Chart
*   **Main Flow:** Doctor updates status to "Completed" and marks a procedure on the Visual Dental Chart.
*   **Alternative Scenario:** Invalid Tooth ID selected; System prompts for a valid tooth number (1-32).

### UC-08: Admin Manage Staff
*   **Main Flow:** Admin adds a new Doctor or Receptionist and assigns roles.
*   **Alternative Scenario:** Mandatory 2FA is not enabled for a Senior Doctor; System forces 2FA setup.

### UC-09: Manage Inventory
*   **Main Flow:** Admin updates stock quantity. System checks against MinimumThreshold.
*   **Alternative Scenario (Alert):** Quantity <= Threshold; System triggers Dashboard alert AND sends automated Email.

### UC-10: Financial Reports
*   **Main Flow:** Admin generates a monthly revenue report.
*   **Alternative Scenario:** Unpaid invoices detected; System highlights "Debt Tracking" section.
