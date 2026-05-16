# 📄 File 04: DATABASE_DESIGN

## 1. Technical Stack Overview
*   **Database Engine:** SQLite (Serverless, self-contained, and lightweight).
*   **ORM:** Entity Framework Core (Code-First Approach).
*   **Naming Convention:** PascalCase for Tables and Columns.
*   **Localization Strategy:** Data storage handles multilingual strings, specifically optimized for **Arabic RTL** display in the UI.

---

## 2. Entity Relationship Logic
The database architecture follows a **Relational Model** to ensure data consistency and eliminate redundancy.
*   **Users & Roles:** Implements RBAC (Role-Based Access Control) as defined in File 03.
*   **One-to-Many:** A Patient has multiple Appointments and Clinical Records.
*   **One-to-One:** Each completed Appointment is linked to exactly one Invoice.
*   **Audit Tracking:** A central table to log every sensitive transaction for E-Business integrity.

---

## 3. Data Tables Definition (Schema)

### A. Identity & User Management
| Table | Column | Data Type | Constraints |
| :--- | :--- | :--- | :--- |
| **Users** | Id, FullName, Email, PasswordHash, Role, Is2FAEnabled | Int, String, String, String, String, Boolean | Primary Key, Unique Email |
| **Patients** | Id, NationalID, FullName_AR, Phone, DOB, Gender | Int, String, String, String, DateTime, String | Primary Key, Unique NationalID |

### B. Clinical Operations
| Table | Column | Data Type | Constraints |
| :--- | :--- | :--- | :--- |
| **Appointments** | Id, PatientId, DoctorId, StartTime, EndTime, Status | Int, Int, Int, DateTime, DateTime, String | FK (Patients, Users), No Overlap |
| **ClinicalRecords**| Id, PatientId, DoctorId, Diagnosis, TreatmentPlan | Int, Int, Int, Text, Text | FK (Patients, Users) |
| **DentalCharts** | Id, PatientId, ToothNumber, Condition, Notes | Int, Int, Int, String, String | FK (Patients), Tooth (1-32) |

### C. Financials & Services
| Table | Column | Data Type | Constraints |
| :--- | :--- | :--- | :--- |
| **Services** | Id, ServiceName_AR, Category, Price | Int, String, String, Decimal | Primary Key |
| **Invoices** | Id, AppointmentId, TotalAmount, PaidAmount, Status | Int, Int, Decimal, Decimal, String | FK (Appointments) |

### D. System Intelligence (E-Business Features)
| Table | Column | Data Type | Constraints |
| :--- | :--- | :--- | :--- |
| **Inventory** | Id, ItemName, Quantity, MinimumThreshold | Int, String, Int, Int | Alert if Qty <= Threshold |
| **AuditLogs** | Id, UserId, Action, TableName, Timestamp, Details | Int, Int, String, String, DateTime, Text | FK (Users) |
| **Feedbacks** | Id, PatientId, Rating, Comment, SubmittedAt | Int, Int, Int, Text, DateTime | FK (Patients), Rating (1-5) |

---

## 4. Business Rules & Constraints (Database Level)

1.  **No Overlapping Appointments:** A database-level check (or Logic Layer validation) ensures that no `DoctorId` has two appointments where the time slots intersect.
2.  **Soft Deletion:** To preserve medical and financial history, records like `Patients` and `Invoices` will use an `IsDeleted` flag instead of hard deletion.
3.  **Audit Trigger:** Any change to the `Invoices` table (Price change or Status update) must automatically create an entry in `AuditLogs`.
4.  **RTL Compatibility:** String fields for names and descriptions are configured to support UTF-8 to ensure **Arabic** text remains uncorrupted.

---

## 5. Antigravity & Razor View Integration
*   **Backend:** ASP.NET Core MVC Controllers will use `ViewModels` to map these tables to the views.
*   **Frontend:** The `DentalCharts` table data will be fetched via JSON to render an interactive SVG map of the teeth in the **Razor View**.
*   **Performance:** Indexed columns on `NationalID`, `Phone`, and `AppointmentDate` to ensure page load times remain under **2 seconds**.
