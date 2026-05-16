# 📄 File 07: 07_UI_UX_REQUIREMENTS.md → Antigravity

## 1. Antigravity Prompt (Developer Instruction)
> **Instruction:** Read 07. List all 23 Razor View files (.cshtml) grouped by folder area. Implement a **Dynamic Sidebar** layout that toggles visibility based on User Role (Admin, Doctor, Receptionist, Patient). Use **Chart.js** for Admin and Doctor dashboards to visualize clinic performance and financial trends. For the booking process, implement a **Single-Page Tabbed Wizard** to ensure high performance and fast loading for users with low bandwidth.

## 2. Page Inventory & Folder Structure (Areas Based)

### A. Shared Layout & Components
*Folder: Views/Shared/*
* `_Layout.cshtml`: The main application shell with full **RTL (Arabic)** support.
* `_Sidebar.cshtml`: A dynamic partial view rendering navigation links based on `@User.IsInRole()`.
* `_TopNav.cshtml`: User profile settings, 2FA status, and notifications.

### B. Public & Account Area
*Folder: Views/Home/ & Views/Account/*
1.  `Index.cshtml`: Professional landing page for the clinic.
2.  `Login.cshtml`: Secure login with 2FA verification step.
3.  `Register.cshtml`: Patient-only registration form.
4.  `Services.cshtml`: Public list of treatments and prices.

### C. Patient Area (Self-Service)
*Folder: Areas/Patient/Views/*
5.  `Dashboard.cshtml`: Upcoming appointments and health alerts.
6.  `Book.cshtml`: **Fast-Load Wizard** (Select Doctor > Time > Confirm) in a single page.
7.  `MyHistory.cshtml`: List of past visits, digital invoices, and treatment summaries.
8.  `Feedback.cshtml`: Form for rating services (E-Business integration).

### D. Doctor Area (Clinical Management)
*Folder: Areas/Doctor/Views/*
9.  `Dashboard.cshtml`: Performance metrics (Patients/month) using **Chart.js**.
10. `Schedule.cshtml`: Detailed daily queue for the doctor.
11. `PatientDetails.cshtml`: Central hub for patient history and clinical notes.
12. `DentalChart.cshtml`: **Interactive SVG Visual Dental Map** for procedures.

### E. Receptionist Area (Operations)
*Folder: Areas/Receptionist/Views/*
13. `Dashboard.cshtml`: Real-time clinic flow overview.
14. `ManagePatients.cshtml`: Search, register, and update patient profiles.
15. `QuickBook.cshtml`: Rapid scheduling tool for walk-in patients.
16. `Billing.cshtml`: Invoice generation and payment processing.

### F. Admin Area (Clinic Administration)
*Folder: Areas/Admin/Views/*
17. `Dashboard.cshtml`: Global analytics (Revenue, Popular Services) using **Chart.js**.
18. `ManageStaff.cshtml`: CRUD for staff, 2FA management, and shift assignments.
19. `Inventory.cshtml`: Stock levels and automated reorder alerts.
20. `Reports.cshtml`: Advanced financial reports and Debt Tracking.
21. `AuditLogs.cshtml`: Activity logs for system transparency.

## 3. UI/UX Technical Specifications
* **Localization:** 100% Arabic UI (RTL) with UTF-8 encoding.
* **Performance:** Vanilla JS for all UI interactions to ensure < 2s load time.
* **Visuals:** Chart.js integration for data-driven decision-making (E-Biz).
* **Responsiveness:** Mobile-first approach via Bootstrap 5 for on-the-go booking.
