# 📁 File 07: UI/UX & Page Inventory Requirements (07_UI_UX_REQUIREMENTS.md)

## 1. Antigravity Prompt (Developer Instruction)
> Instruction: Read 07_UI_UX_REQUIREMENTS.md. Generate the complete physical Razor View (.cshtml) file inventory grouped by their respective ASP.NET Core MVC Folder Areas. 
> Layout Mandate: Implement a unified dynamic layout system that reads claims tokens to toggle sidebar navigational modules based on the authenticated identity contract (Admin, Doctor, Receptionist, Patient). Ensure all analytics components are mapped to use Chart.js configurations.

---

## 2. Complete Razor View Inventory & Folder Structure

### A. Shared Layout Layer (Global Context)
*Path: Views/Shared/*
* [File-01] `_Layout.cshtml`: The master web presentation shell optimized for native Arabic typography and Right-to-Left (RTL) structural rendering.
* [File-02] `_Sidebar.cshtml`: Dynamic partial view executing role-based visibility evaluation (@User.IsInRole()) to render secure operational links.
* [File-03] `_TopNav.cshtml`: Top utility bar displaying active notifications, session states, and 2FA credential profile controls.

### B. Public & Account Security Views
*Path: Views/Home/ & Views/Account/*
* [File-04] `Views/Home/Index.cshtml`: Professional clinic homepage outlining dental fields, office timings, and localized introductory data.
* [File-05] `Views/Home/Services.cshtml`: Publicly accessible catalog showcasing treatment classifications mapped to clinic base prices.
* [File-06] `Views/Account/Login.cshtml`: Centralized secure portal handling user credential evaluation and mandatory Admin/Senior-Doctor 2FA tokens.
* [File-07] `Views/Account/Register.cshtml`: Public registration portal allowing new clinic patients to instantiate system credentials.

### C. Patient Portal Area (Self-Service Matrix)
*Path: Areas/Patient/Views/Home/*
* [File-08] `Dashboard.cshtml`: Customer cockpit displaying real-time updates on active appointments and post-care medical alerts.
* [File-09] `Book.cshtml`: Fast-loading, single-page tabbed booking wizard designed to optimize slot allocation and reduce drop-off thresholds.
* [File-10] `MyHistory.cshtml`: Comprehensive archive listing personal clinical histories, downloadable digital billing invoices, and treatment feedback statuses.
* [File-11] `Feedback.cshtml`: Interactive assessment engine for logging visit ratings and reviews to drive clinic quality data metrics.

### D. Doctor Portal Area (Clinical Management Suite)
*Path: Areas/Doctor/Views/Clinical/*
* [File-12] `Dashboard.cshtml`: Private physician screen visualizing monthly caseload trends and productivity metrics using customized Chart.js components.
* [File-13] `Schedule.cshtml`: Chronological tracking queue sorting assigned patient appointments for the active calendar date.
* [File-14] `PatientDetails.cshtml`: Central clinical record workspace aggregating archived medical summaries, medications, and historical entries.
* [File-15] `DentalChart.cshtml`: High-precision graphical interface loading the interactive Arabic SVG map for charting teeth-specific procedures (1–32).

### E. Receptionist Portal Area (Front-Desk Operations)
*Path: Areas/Receptionist/Views/Operations/*
* [File-16] `Dashboard.cshtml`: Front-desk stream tracker illustrating current waiting-room volume and today's scheduling pipeline.
* [File-17] `ManagePatients.cshtml`: Administrative portal for rapid customer lookups (National ID/Phone), onboarding new rows, and indexing patient profiles.
* [File-18] `QuickBook.cshtml`: Optimized internal reservation screen allowing rapid scheduling for walk-in patients and manual overrides.
* [File-19] `Billing.cshtml`: Direct invoice processing module for calculating costs, managing balances, and logging transactional methods.
* ### F. Administrative Portal Area (Enterprise Architecture)
*Path: Areas/Admin/Views/Control/*
* [File-20] `Dashboard.cshtml`: Comprehensive business control deck utilizing Chart.js to map revenue aggregates, service popularity ratios, and operational metrics.
* [File-21] `ManageStaff.cshtml`: Master workspace for executing staff credential CRUD configurations, 2FA states, and doctor shift boundaries.
* [File-22] `Inventory.cshtml`: Logistics control screen tracking core consumables alongside real-time threshold alert status tags.
* [File-23] `Reports.cshtml`: Deep financial reporting interface displaying monthly clinical balance evaluations and active Debt Tracking sheets.
* [File-24] `AuditLogs.cshtml`: Read-only system ledger detailing data modification actions mapped to User context hashes.

---

## 3. UI/UX Technical Specifications
* Localization: 100% Arabic presentation layout with complete Right-to-Left (RTL) style rendering and UTF-8 script compatibility.
* Performance Control: Interface actions utilize native Vanilla JS components to guarantee peak view load tracking under 2.0 seconds.
* Analytical Graphics: Chart.js library wrappers are implemented for rendering administrative dashboard intelligence feeds.
* Layout Adaptability: Built on mobile-first Bootstrap 5 frameworks to ensure visual layout coherence across varying device screen scopes.
