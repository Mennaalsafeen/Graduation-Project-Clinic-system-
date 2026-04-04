# 📋 System Functionality & Use Cases

This section outlines the specific actions each user can perform within the **Dental Clinic Appointment Management System**.

---

## 👥 System Roles
The system supports three primary user roles, each with distinct permissions:
1. **Patient:** The service seeker.
2. **Dentist:** The service provider.
3. **Admin / Receptionist:** The system and clinic orchestrator.

---

## 🎯 Use Case Breakdowns

### 👤 Patient Use Cases
* **Account Management:** Register a new account and log in securely.
* **Booking:** Search for slots and book a dental appointment.
* **Tracking:** View a comprehensive list of upcoming and past appointments.
* **Flexibility:** Cancel or reschedule an existing appointment if needed.

### 🩺 Dentist Use Cases
* **Authentication:** Secure log in to the professional dashboard.
* **Schedule Oversight:** View all appointments assigned specifically to them.
* **Availability Management:** Update daily working hours and set "busy" slots.
* **Patient Prep:** Review specific appointment details and notes before the visit.

### 🛠 Admin / Receptionist Use Cases
* **User Control:** Manage patient and staff accounts (Create/Update/Deactivate).
* **Full Schedule Control:** Oversee, create, and modify all clinic appointments.
* **Resource Allocation:** Assign dentists to specific shifts or update their schedules.
* **Monitoring:** Audit clinic booking activity and daily traffic.

---

## 🗺 System Scope Diagram (Conceptual)

Below is a simplified representation of the interaction between users and the system:

```mermaid
graph LR
    A[Guest/Patient] --> System[Dental Clinic System]
    B[Dentist] --> System
    C[Admin/Receptionist] --> System