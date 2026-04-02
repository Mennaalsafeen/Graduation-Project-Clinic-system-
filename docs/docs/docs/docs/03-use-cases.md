# Use Cases

## Overview
This document describes the main use cases of the Clinic Appointment Management System, showing how different users interact with the system.

---

## Use Case 1: User Registration
**Actor:** Patient / Doctor / Admin  
**Description:** Users can create a new account in the system.  
**Preconditions:** User is not registered.  
**Main Flow:**
1. User enters registration details.
2. System validates the input.
3. System creates a new account.
4. User is redirected to login.

---

## Use Case 2: User Login
**Actor:** All Users  
**Description:** Users log into the system using their credentials.  
**Preconditions:** User must have an account.  
**Main Flow:**
1. User enters username and password.
2. System verifies credentials.
3. User is redirected to dashboard.

---

## Use Case 3: Book Appointment
**Actor:** Patient  
**Description:** Patient books an appointment with a doctor.  
**Preconditions:** User must be logged in.  
**Main Flow:**
1. Patient selects a doctor.
2. Patient selects date and time.
3. System checks availability.
4. Appointment is created.

---

## Use Case 4: Manage Appointments
**Actor:** Patient / Doctor / Admin  
**Description:** Users can view, update, or cancel appointments.  
**Main Flow:**
1. User views appointments list.
2. User selects an appointment.
3. User updates or cancels it.

---

## Use Case 5: Manage Users
**Actor:** Admin  
**Description:** Admin manages system users.  
**Main Flow:**
1. Admin views users list.
2. Admin adds, edits, or deletes users.

---

## Use Case Diagram (Description)
The system includes interactions between:
- Patients booking appointments
- Doctors managing schedules
- Admin managing users and system data
