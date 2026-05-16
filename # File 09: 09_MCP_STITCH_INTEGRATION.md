# File 09: 09_MCP_STITCH_INTEGRATION.md -> 🛸 Antigravity

> **Bridges Google Stitch design to Antigravity via MCP. Contains the corrected Project ID.**

## 1. Google Stitch Project ID
**REAL_PROJECT_ID:** `7285994045004866023`

## 2. Page Mapping (Stitch UI to Razor Views)
Map the 18 generated pages to the ASP.NET Core MVC Folder structure:

| Stitch Page Name | Razor View Path | User Role |
| :--- | :--- | :--- |
| Landing Page | `Views/Home/Index.cshtml` | Public |
| Login | `Views/Account/Login.cshtml` | Public |
| Register | `Views/Account/Register.cshtml` | Patient |
| Services | `Views/Home/Services.cshtml` | Public |
| Contact Us | `Views/Home/Contact.cshtml` | Public |
| Patient Dashboard | `Areas/Patient/Views/Dashboard.cshtml` | Patient |
| Booking Wizard | `Areas/Patient/Views/Book.cshtml` | Patient |
| My Visits | `Areas/Patient/Views/MyHistory.cshtml` | Patient |
| Feedback | `Areas/Patient/Views/Feedback.cshtml` | Patient |
| Doctor Dashboard | `Areas/Doctor/Views/Dashboard.cshtml` | Doctor |
| Work Schedule | `Areas/Doctor/Views/Schedule.cshtml` | Doctor |
| Clinical Hub (EHR) | `Areas/Doctor/Views/PatientDetails.cshtml` | Doctor |
| Admin Dashboard | `Areas/Admin/Views/Dashboard.cshtml` | Admin |
| Staff Management | `Areas/Admin/Views/ManageStaff.cshtml` | Admin |
| Inventory | `Areas/Admin/Views/Inventory.cshtml` | Admin |
| Financials | `Areas/Admin/Views/Reports.cshtml` | Admin |
| Audit Trail | `Areas/Admin/Views/AuditLogs.cshtml` | Admin |
| Receptionist Flow | `Areas/Receptionist/Views/Dashboard.cshtml` | Receptionist |

## 3. Frontend Implementation Rules
- **CSS:** Extract all styles and place them in `wwwroot/css/site.css` and `wwwroot/css/rtl-clinical.css`.
- **JavaScript:** Use ONLY Vanilla JS. Place scripts in `wwwroot/js/clinic-logic.js`.
- **Assets:** Ensure all icons and medical SVGs (especially the Dental Chart) are mapped to `wwwroot/assets/`.
- **Framework:** Ensure Bootstrap 5 grid is preserved with full RTL support.

## 4. Antigravity Prompt (Instruction)
> **Action:** Read File 09. Connect to Google Stitch via MCP using Project ID: `7285994045004866023`.
> 1. List all 18 pages found in the project.
> 2. Convert each Stitch UI component into a clean ASP.NET Core Razor View.
> 3. Separate HTML/CSS/JS according to the folder structure above.
> 4. Ensure the **Premium Clinical Light Mode** (Indigo & Mint) is perfectly preserved during conversion.
> 5. Identify any functional gaps between the UI and the Business Rules in File 05.

---
> **⚠️ WARNING:** Without the real Project ID, the file is empty and the connection will fail.
