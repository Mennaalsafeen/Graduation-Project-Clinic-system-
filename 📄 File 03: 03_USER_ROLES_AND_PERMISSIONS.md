# 📄 File 03: USER_ROLES_AND_PERMISSIONS

## 1. Introduction
The Dental Clinic Appointment Management System utilizes a **Role-Based Access Control (RBAC)** model. This ensures data integrity, patient confidentiality (HIPAA-aligned principles), and operational efficiency. While the documentation is in English, the **System Interface (UI) is fully localized in Arabic (RTL)**.

---

## 2. User Roles Definition

| Role | Description | Access Level |
| :--- | :--- | :--- |
| **System Admin** | The business owner/manager. Oversees finances and staff. | Full System Access |
| **Senior Doctor** | Head of medical staff. Can oversee all clinical records. | Full Clinical Access |
| **Doctor** | General practitioners. Manage assigned patients and charts. | Standard Clinical Access |
| **Receptionist** | Front-desk operations, scheduling, and billing. | Operational Access |
| **Patient** | End-user. Manages personal bookings and history. | Self-Service Access |

---

## 3. Advanced Feature Additions (E-Business Focused)

### A. Audit Trail (Activity Logs)
*   **Traceability:** Every "Create", "Update", or "Delete" action is logged with a timestamp and User ID.
*   **Accountability:** Admins can track who changed a service price, who cancelled a payment, or who modified a medical record.

### B. Two-Factor Authentication (2FA)
*   **Security:** Mandatory for **Admin** and **Senior Doctor** roles due to the sensitivity of financial and medical data.
*   **Implementation:** Secure login via email or SMS verification codes.

### C. Password Recovery Policy
*   **Self-Service:** Patients can reset passwords via registered email.
*   **Assisted:** Receptionists can trigger a "Password Reset Link" for patients in-person.
*   **Staff:** Only the Admin can reset passwords for Doctors and Receptionists.

---

## 4. Detailed Permissions Matrix (CRUD)
*(C: Create, R: Read, U: Update, D: Delete)*

| Feature / Module | Admin | Senior Doctor | Doctor | Receptionist | Patient |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Staff Accounts** | CRUD | R | - | - | - |
| **Clinical Records (EHR)** | R | CRUD | CRU* | R (Status Only) | - |
| **Visual Dental Chart** | R | CRUD | CRU* | - | - |
| **Appointment Engine** | CRUD | R | RU | CRUD | CRU (Self) |
| **Financial Reports** | CRUD | R | - | - | - |
| **Invoicing & Payments** | CRUD | R | - | CRU | R (Self) |
| **Inventory & Alerts** | CRUD | R | R | RU | - |
| **Patient Feedback** | R | R | - | - | CRU |
| **Audit Logs** | R | - | - | - | - |

*\*Doctors can only update records of patients assigned to them.*

---

## 5. Specific Business Rules & Security

1.  **UI Localization:** All roles will interact with an **Arabic RTL Interface**, ensuring zero language barriers for local staff and patients.
2.  **Medical Privacy:** Receptionists can see *that* a patient has an appointment, but cannot view the specific *medical diagnosis* or *dental chart* details.
3.  **Financial Integrity:** Once an invoice is "Paid," it cannot be deleted. It can only be "Refunded" by an Admin, which triggers an Audit Log entry.
4.  **Appointment Conflict Prevention:** The system logic blocks the database from saving two overlapping appointments for the same Doctor ID.
5.  **Session Security:** Automatic logout after 30 minutes of inactivity to protect sensitive data on shared clinic computers.
