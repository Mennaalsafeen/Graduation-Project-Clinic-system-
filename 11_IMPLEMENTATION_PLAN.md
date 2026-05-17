# 📁 File 11: Master Implementation Plan (11_IMPLEMENTATION_PLAN.md)

## 1. Antigravity Prompt (Master Execution Instruction)
> Instruction for Antigravity: Read 11_IMPLEMENTATION_PLAN.md carefully. Execute this implementation plan PHASE BY PHASE in strict linear dependency order. 
> 🚨 CRITICAL COMPLIANCE RULE (Slide 19): Do NOT combine stages, skip steps, or attempt to compile the entire system at once. You must completely finish, validate, and present a strict summary report after each individual phase before receiving authorization to move to the next dependent phase.
> Tech Stack: ASP.NET Core MVC with SQLite Database via Entity Framework Core.

---

## 2. Strict Sequential Implementation Phases

### 🟦 Phase 1: Read & Understand (Context Absorption)
* Action: Scan and align the logic across all prior 10 documentation files (01_PROJECT_OVERVIEW.md through 10_BACKEND_REQUIREMENTS.md). Map out all domain boundaries, application roles, and systemic restrictions.
* Deliverable: Architectural alignment confirmation report.

### 🟦 Phase 2: Project Setup & Baseline Provisioning
* Action: Create the foundation for the ASP.NET Core MVC web application. Install required NuGet packages for Microsoft SQLite Provider and Entity Framework Core tools. Setup baseline wwwroot directory assets.

### 🟦 Phase 3: Relational Data Layer Instantiation
* Action: Translate entity specifications into concrete C# database models and establish the ApplicationDbContext mapped to SQLite. Execute and apply the initial EF Core Migration to build the local database file.
* Seed Requirement: Populate the database with 1 default Admin (admin@clinic.com), 3 sample doctors, and the 5 core dental service categories.

### 🟦 Phase 4: Business Logic Services Layer
* Action: Implement the backend logical core via IAppointmentService. Program the 4 strict verification methods returning boolean flags to catch double-bookings, physician timeline overlaps, shift constraints, and the 24-hour cancellation rule.

### 🟦 Phase 5: Authentication Layer Initialization
* Action: Integrate Microsoft.AspNetCore.Authentication.Cookies middleware inside the program pipeline. Establish explicit user session persistence schemas, isolated completely from controller authorization logic.

### 🟦 Phase 6: UI View Materialization from Google Stitch
* Action: Fetch layout screens via Project ID 7285994045004866023 using the MCP Stitch bridge. Compile all 18 customized Razor Views (.cshtml) structured across Area subfolders (Public, Patient, Doctor, Admin) using the Teal & White theme.

### 🟦 Phase 7: Controller Routing & Authorization Policies
* Action: Build the 5 core controllers (HomeController, AuthController, PatientController, DoctorController, AdminController). Secure controller entry paths using strict role filter parameters: [Authorize(Roles = "...")].

### 🟦 Phase 8: End-to-End Operational Booking Flow
* Action: Connect and orchestrate the unified patient appointment lifecycle. Ensure full structural linking from the UI booking interface down into the IAppointmentService validation pipeline, saving to the SQLite database under "Pending" status.

### 🟦 Phase 9: System Integration Testing & Validation Audit
* Action: Execute comprehensive technical verification checks across all subsystems. Test data isolation borders, fallback interfaces for alternative error-handling scenarios, and final routing stability.

---

## 3. Mandatory Phase-Gate Reporting Contract
After the completion of each individual phase, the development framework must present a structural "Developer Status Update" before proceeding:
1. Tasks Successfully Completed: Structural checklist of achieved milestones.
2. Files Altered/Generated: Precise accounting of codebase modifications.
3. Technical Blockers/Warnings: Active tracking of any compiled deviations.
