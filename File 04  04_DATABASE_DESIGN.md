# 📁 File 04: Database Design (DATABASE_DESIGN.md)

## 1. Technical Stack Overview
* Database Engine: SQLite (Serverless, self-contained, and lightweight).
* ORM (Object-Relational Mapper): Entity Framework Core utilizing the Code-First Approach.
* Naming Convention: PascalCase for all Tables and Columns (e.g., PatientId, StartTime).
* Localization Strategy: Text fields are configured to support UTF-8 encoding to ensure seamless storage and retrieval of multilingual strings, specifically optimized for Arabic Right-to-Left (RTL) display in the user interface.

## 2. Entity Relationship Logic
The database architecture follows a Relational Model to ensure data consistency, enforce integrity constraints, and eliminate redundancy:
* Identity & Profiles (Slide Correction): The Users table serves as the primary authentication and identity contract. To prevent architecture anti-patterns, DoctorProfiles and PatientProfiles are separate entities linked to the Users table via a One-to-One relationship. This decouples core credentials from role-specific clinical or operational attributes.
* One-to-Many Relationships: A patient has multiple appointments and clinical records; a doctor has multiple operational availabilities and assigned appointments.
* One-to-One Relationships: Each completed appointment maps directly to exactly one digital invoice.
* Audit Tracking: A centralized ledger table logs all high-sensitivity transactions to preserve E-Business audit integrity.

## 3. Data Tables Definition (Schema)

### A. Identity & User Management (Identity & Profiles)

| Table Name | Columns | Data Type | Constraints |
| :--- | :--- | :--- | :--- |
| Users | Id, Email, PasswordHash, Role, IsActive, Is2FAEnabled | Int, String, String, String, Boolean, Boolean | Primary Key, Unique Email |
| DoctorProfiles | Id, UserId, Specialty, IsApproved | Int, Int, String, Boolean | Primary Key, FK (Users) [One-to-One] |
| PatientProfiles | Id, UserId, NationalID, FullName_AR, Phone, DOB, Gender | Int, Int, String, String, String, DateTime, String | Primary Key, Unique NationalID, FK (Users) |

### B. Clinical Operations & Scheduling

| Table Name | Columns | Data Type | Constraints |
| :--- | :--- | :--- | :--- |
| DoctorAvailabilities | Id, DoctorId, DayOfWeek, StartTime, EndTime | Int, Int, Int, TimeSpan, TimeSpan | Primary Key, FK (DoctorProfiles) |
| Appointments | Id, PatientId, DoctorId, StartTime, EndTime, Status | Int, Int, Int, DateTime, DateTime, String | FK (PatientProfiles, DoctorProfiles), No Overlap Validation |
| ClinicalRecords | Id, PatientId, DoctorId, Diagnosis, TreatmentPlan | Int, Int, Int, Text, Text | FK (PatientProfiles, DoctorProfiles) |
| DentalCharts | Id, PatientId, ToothNumber, Condition, Notes | Int, Int, Int, String, String | FK (PatientProfiles), Tooth Scope (1-32) |

### C. Financials & Services

| Table Name | Columns | Data Type | Constraints |
| :--- | :--- | :--- | :--- |
| Services | Id, ServiceName_AR, Category, Price | Int, String, String, Decimal | Primary Key |
| Invoices | Id, AppointmentId, TotalAmount, PaidAmount, Status | Int, Int, Decimal, Decimal, String | FK (Appointments) |

### D. System Intelligence & E-Business Features

| Table Name | Columns | Data Type | Constraints |
| :--- | :--- | :--- | :--- |
| Inventory | Id, ItemName, Quantity, MinimumThreshold | Int, String, Int, Int | Smart Alert triggered if (Qty <= Threshold) |
| AuditLogs | Id, UserId, Action, TableName, Timestamp, Details | Int, Int, String, String, DateTime, Text | FK (Users) |
| Feedbacks | Id, PatientId, Rating, Comment, SubmittedAt | Int, Int, Int, Text, DateTime | FK (PatientProfiles), Rating Range (1-5) |
## 4. Business Rules & Constraints (Database Level)
* No Overlapping Appointments: A custom validation engine at the database layer blocks transactions if a new record intersects with an existing appointment window (StartTime to EndTime) for the same DoctorId.
* Soft Deletion: To preserve compliance with medical archives and financial retention policies, critical structural data like PatientProfiles and Invoices utilize an IsDeleted flag instead of hard deletion.
* Automated Audit Triggers: Any mutation, price adjustment, or status override within the Invoices or Services schema automatically streams an execution snapshot into the AuditLogs ledger.
* Navigation Properties: As instructed in the architectural design specifications, foreign keys are fully mapped into Navigation Properties within the ORM code to generate a seamless Entity Relationship Diagram (ERD).

## 5. Antigravity & Razor View Integration
* Data Flow Architecture: ASP.NET Core MVC controllers utilize dedicated ViewModels to safely bind and project raw relational records into user interface modules.
* Visual Dental Chart Rendering: Data stored within the DentalCharts entity is dispatched to the client-side UI asynchronously as a JSON payload. Vanilla JS executes a DOM transformation engine to parse this structural data and dynamically colorize an interactive, standalone SVG map of the human jaw inside the Razor View.
* Performance Indexes: High-frequency relational lookup query components (NationalID, Phone, AppointmentDate) are structurally indexed, optimizing overall page execution load latencies below 2 seconds.
