# 📁 File 09: MCP Stitch Integration Blueprint (09_MCP_STITCH_INTEGRATION.md)

## 1. Google Stitch Project Identity
* Protocol Connector: Model Context Protocol (MCP) Bridge
* Target Project ID: 7285994045004866023
* ⚠️ ARCHITECTURAL MANDATE (Slide 17): This file contains a validated, production-ready Project ID. Leaving a placeholder or empty identity component will cause the MCP infrastructure to disconnect, breaking the bridge between visual assets and backend engines.

---

## 2. Page Mapping Matrix (Stitch UI Components to Razor Views)
The MCP deployment engine must extract the 18 generated UI templates and map them explicitly into the standard ASP.NET Core MVC directory structure:

| Stitch Source Page Name | Target Razor View Path | Auth Role Contract |
| :--- | :--- | :--- |
| Landing Page | Views/Home/Index.cshtml | Public |
| Login | Views/Account/Login.cshtml | Public |
| Register | Views/Account/Register.cshtml | Patient / Public |
| Services | Views/Home/Services.cshtml | Public |
| Contact Us | Views/Home/Contact.cshtml | Public |
| Patient Dashboard | Areas/Patient/Views/Dashboard.cshtml | Patient |
| Booking Wizard | Areas/Patient/Views/Book.cshtml | Patient |
| My Visits | Areas/Patient/Views/MyHistory.cshtml | Patient |
| Feedback | Areas/Patient/Views/Feedback.cshtml | Patient |
| Doctor Dashboard | Areas/Doctor/Views/Dashboard.cshtml | Doctor |
| Work Schedule | Areas/Doctor/Views/Schedule.cshtml | Doctor |
| Clinical Hub (EHR) | Areas/Doctor/Views/PatientDetails.cshtml | Doctor / Senior Doctor |
| Admin Dashboard | Areas/Admin/Views/Dashboard.cshtml | Admin |
| Staff Management | Areas/Admin/Views/ManageStaff.cshtml | Admin |
| Inventory | Areas/Admin/Views/Inventory.cshtml | Admin |
| Financials | Areas/Admin/Views/Reports.cshtml | Admin |
| Audit Trail | Areas/Admin/Views/AuditLogs.cshtml | Admin |
| Receptionist Flow | Areas/Receptionist/Views/Dashboard.cshtml | Receptionist |

---

## 3. Frontend Implementation & Separation Rules
To preserve interface integrity and guarantee page rendering speeds under 2.0 seconds, compliance with the following static file division rules is mandatory:
* Style Sheeting (CSS): Extract compilation layouts. Place primary elements inside wwwroot/css/site.css and dedicated localized configurations inside wwwroot/css/rtl-clinical.css.
* Scripting Interaction (JS): Enforce pure Vanilla JS standards. All client-side validation, UI triggers, and event loops must reside natively within wwwroot/js/clinic-logic.js (Strictly no Angular, React, or Vue compilation bundles).
* Graphic Assets & Models: Package all visual icons, medical imagery, and custom standalone SVG adult dental jaw maps (Teeth 1–32) directly inside wwwroot/assets/.
* Grid Controls: Retain adaptive Bootstrap 5 layouts, ensuring complete validation with Right-to-Left (RTL) Arabic typography.

---

## 4. Antigravity Prompt (Execution Directive)
> Execution Directive: Read 09_MCP_STITCH_INTEGRATION.md. Initialize the MCP bridge tool and query Google Stitch project token 7285994045004866023. 
> 1. Download and list all 18 visual design assets recognized within the design interface.
> 2. Automatically transform every static visual component into a fully responsive .NET Razor View mapped to the folder configuration array above.
> 3. Perform file separation, parsing HTML blocks into views, styles into wwwroot/css/, and scripts into wwwroot/js/.
> 4. Guard and preserve the Premium Clinical Light DNA (Indigo brand codes paired with Mint interaction anchors).
> 5. Review the final view code output and call out any missing fields or functional gaps against the Service validation rules defined in File 05.
