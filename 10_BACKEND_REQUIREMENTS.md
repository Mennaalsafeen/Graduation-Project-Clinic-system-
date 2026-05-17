# 📁 File 10: Backend Structural Requirements (10_BACKEND_REQUIREMENTS.md)

## 1. Antigravity Prompt (Core Backend Instruction)
> Instruction: Read 10. Construct the ASP.NET Core MVC application skeleton using SQLite. Implement a strict architectural boundary by isolating Authentication (Cookie-based Identity) from Authorization (Role-Based Access Control) to eliminate configuration coupling.

---

## 2. Controller Routing Architecture
Build exactly 5 core controllers managing system orchestration:
* HomeController: Public views, index layouts, and dental service catalogs.
* AuthController: Handles identity management, Self-Registration interfaces, and unified Login logic.
* PatientController: Self-service scheduling wizard, patient dashboards, and treatment/invoice history.
* DoctorController: Clinical queue management, work schedule calendar tracking, and Dental Chart updates.
* AdminController: Enterprise control center, corporate staff directories, financial reports, and dental inventory.

---

## 3. Service Layer & Business Logic (Validation Contract)
Encapsulate scheduling validations into a clean service layer interface named IAppointmentService. The implementation must expose 4 core C# methods returning boolean confirmations before saving any entity to the database:
1. Patient Double-Booking Check: Ensure the patient doesn't reserve multiple slots on the same day with the same doctor.
2. Doctor Time Slot Conflict: Prevent overlapping appointments for the same physician.
3. Shift Availability Validation: Verify that the requested appointment falls strictly within the doctor's active working hours.
4. Cancellation Window Enforcement: Restrict appointment cancellations if the remaining time is less than 24 hours.

---

## 4. Security Framework (Authentication vs Authorization)
> ⚠️ Say in Discussion: 'Authentication is the login layer (who you are). Authorization is the resource access contract via the [Authorize] attribute (what you can do). They are completely distinct structural layers.'

* Authentication Layer: Deploy Microsoft.AspNetCore.Authentication.Cookies middleware to handle secure session persistence.
* Authorization Filters: Secure targeted controllers and actions using role-based contracts: [Authorize(Roles = "Admin, Doctor, Patient, Receptionist")].

---

## 5. Data Infrastructure & Storage (SQLite)
* Database Engine: Microsoft SQLite Provider for lightweight deployment.
* DbContext Context: Instantiate ApplicationDbContext managing EF Core models and entity relationships.
* Migrations Framework: Execute Entity Framework Core migrations to programmatically build the underlying relational tables.
* Seed Data Protocol: Auto-populate tables on compilation if empty with:
  * 1 Master Admin Account (admin@clinic.com).
  * Core Dental Services lookup index (Cleaning, Orthodontics, Surgery) matching base fees.

---

## 6. Configuration (appsettings.json)
Configure the data context initialization to source the SQLite local database path:
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Data Source=ClinicDatabase.db"
  }
}
