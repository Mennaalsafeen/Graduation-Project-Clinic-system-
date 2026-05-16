# 📄 File 05: BUSINESS_RULES.md

## 1. Introduction
This document defines the core logic and constraints governing the **Dental Clinic Appointment Management System**. These rules ensure operational consistency, financial integrity, and medical privacy. While this documentation is in English, all rules must be implemented within the **Arabic RTL (Right-to-Left)** user interface.

## 2. Appointment & Scheduling Rules
*   **A. Operating Hours & Shift Logic:** 
    *   The clinic operates from **09:00 AM** to **08:00 PM**.
    *   **Continuous Service:** There is no total clinic shutdown for breaks. Instead, a shift-based system is implemented where doctors rotate breaks, ensuring at least one doctor is always available to attend to patients.
*   **B. Flexible Appointment Duration:** The duration of each appointment is not fixed. It is manually determined and entered by the **Receptionist** at the time of booking, based on the specific procedure type.
*   **C. Conflict Prevention:** The system logic must prevent overlapping appointments for the same doctor and ensure that room/chair capacity is respected during shifts.
*   **D. Smart Cancellation Policy:** 
    *   Patients can cancel via the portal if the start time is **> 24 hours** away.
    *   If **< 24 hours** remains, patients must contact the Receptionist for manual cancellation.
    *   **No Penalties:** There are no financial penalties or fines for cancellations regardless of the timing.

## 3. Financial & Billing Rules
*   **A. Invoice Generation:** An invoice is automatically generated once an appointment status is marked as "In-Progress" or "Completed".
*   **B. Data Integrity:** Once an invoice is marked as **"Paid"**, it cannot be deleted to ensure financial transparency.
*   **C. Refunds:** Only the **Admin** can process a refund. This action triggers a mandatory entry in the **AuditLogs**.
*   **D. Debt Tracking:** The system automatically flags "Completed" appointments with outstanding balances for the Admin’s review.

## 4. Clinical & Data Privacy Rules
*   **A. Restricted Access:** Detailed medical diagnoses and the **Visual Dental Chart** are strictly viewable only by **Doctors** and **Admins**.
*   **B. Receptionist Privacy:** Staff can view scheduling and billing info but are restricted from viewing private medical charts or clinical notes.
*   **C. Clinical Mapping:** All procedures must be linked to a specific tooth number (1-32) on the interactive Arabic SVG map.

## 5. Security & Access Rules (RBAC)
*   **A. Mandatory 2FA:** Two-Factor Authentication is required for **Admin** and **Senior Doctor** roles due to the sensitivity of data.
*   **B. Session Timeout:** Users are automatically logged out after **30 minutes** of inactivity to protect data on shared clinic computers.
*   **C. Audit Trail:** Every sensitive transaction (e.g., modifying a medical record or changing a service price) is logged with a User ID and Timestamp.

## 6. Inventory & System Alerts
*   **A. Dual Notification System:** When medical supplies fall below the **MinimumThreshold**:
    1.  A real-time alert is displayed on the Admin's **Dashboard**.
    2.  An automated **Email Notification** is sent immediately to the Admin's registered email.
*   **B. E-Business Intelligence:** The system generates productivity reports comparing revenue vs. patient volume per doctor.
