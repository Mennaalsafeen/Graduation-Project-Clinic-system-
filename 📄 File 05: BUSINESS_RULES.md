# 📁 File 05: Business Rules Implementation (05_BUSINESS_RULES.md)

## 1. Introduction
This document establishes the core operational logic, financial integrity boundaries, and medical privacy rules governing the Dental Clinic Appointment Management System. 
* Architectural Mandate (Slide 13 Compliance): To ensure clean architecture, all business rules defined below must be encapsulated as validation methods within the Service Layer (`AppointmentService` class) returning a boolean state (bool). No business validation logic shall reside inside the Web Controllers.
* UI Constraint: All backend rules must seamlessly interface with the localized Arabic RTL presentation views.

## 2. Core Appointment & Scheduling Rules (Service Layer Methods)

### Rule 1: No Patient Double-Booking
* Logic: The system must block any transaction attempting to book an appointment for a patient who already has an existing active reservation on the same day with any doctor.
* C# Target: bool IsPatientAvailable(int patientId, DateTime targetDate)

### Rule 2: No Doctor Time-Slot Conflict (Overlapping Prevention)
* Logic: A doctor cannot be assigned to two overlapping patient intervals. The system layer must evaluate that the StartTime and EndTime of a new appointment do not intersect with any confirmed slots for the specified DoctorId.
* C# Target: bool IsDoctorAvailable(int doctorId, DateTime start, DateTime end)

### Rule 3: Booking Within Doctor Operational Availability
* Logic: Appointments can only be saved if the requested window falls entirely within the active shift duration stored in the DoctorAvailabilities schema (Clinic bounds: 09:00 AM to 08:00 PM). The system operates on a rotating shift logic to ensure continuous service without full clinic lockdowns.
* C# Target: bool IsWithinDoctorShifts(int doctorId, DateTime start, DateTime end)

### Rule 4: Smart Cancellation Window (24-Hour Rule)
* Logic: * Self-service cancellation returns true if the delta between DateTime.Now and the appointment StartTime is strictly greater than 24 hours.
  * If the delta is less than 24 hours, self-service is revoked (false), forcing a manual operational override via the Receptionist workflow. No financial penalties are evaluated.
* C# Target: bool CanPatientSelfCancel(DateTime appointmentStart)

---

## 3. Financial & Billing Integrity Rules

### Rule 5: Immutable Paid Transactions
* Logic: Once an Invoice status transitions to "Paid", hard-deletion triggers are permanently blocked at the database pipeline level to ensure total audit transparency.
* C# Target: bool CanModifyInvoice(int invoiceId)

### Rule 6: Admin-Exclusive Refund Boundary
* Logic: Refund operations return false unless the evaluating context identity holds the explicit Admin role contract. Executing a refund automatically commits an interceptor record to the AuditLogs.

### Rule 7: Debt Flagging Automation
* Logic: Upon marking an appointment status as "Completed", if PaidAmount < TotalAmount, the system core automatically streams the record to the administrative Outstanding Balances ledger.

---

## 4. Clinical Mapping & Data Isolation Rules

### Rule 8: Medical Diagnosis Data Isolation (Privacy Contract)
* Logic: Detailed medical charts, historical clinical notes, and the DentalCharts models are encrypted/isolated from front-desk operational scopes. Endpoint evaluation blocks read access if the active role identity is a Receptionist.
* C# Target: bool EnforceClinicalPrivacy(string userRole)

### Rule 9: Structural Clinical Mapping
* Logic: Any treatment ledger insertion inside the DentalCharts module must target a validated structural tooth identifier mapped strictly within the bounds of 1 to 32.

---

## 5. Security & System Intelligence Controls

### Rule 10: Enforced Session Security
* Logic: The system infrastructure drops authentication context states and enforces an auto-logout sequence upon detecting exactly 30 minutes of client inactivity on shared clinical workstation boundaries.
* ### Rule 11: Dual Material Stock Warnings (Inventory Alert)
* Logic: If an inventory deduction causes a material's Quantity to fall below its defined MinimumThreshold, the system concurrently executes a real-time dashboard alert push and fires an automated background notification email to the system administrator.
