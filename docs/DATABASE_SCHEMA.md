# DATABASE_SCHEMA.md

# EduNexus Database Schema

## Overview

This document defines all database tables, fields, primary keys (PK), foreign keys (FK), and relationships used throughout EduNexus.

The schema follows relational database principles and normalization standards to ensure scalability, consistency, and maintainability.

---

# CORE FOUNDATION MODULE

## schools

Purpose:
Stores school information.

| Field          | Type      | Key |
| -------------- | --------- | --- |
| school_id      | INT       | PK  |
| school_name    | VARCHAR   |     |
| school_type    | VARCHAR   |     |
| school_motto   | VARCHAR   |     |
| school_email   | VARCHAR   |     |
| school_phone   | VARCHAR   |     |
| school_address | TEXT      |     |
| county         | VARCHAR   |     |
| country        | VARCHAR   |     |
| website        | VARCHAR   |     |
| created_at     | TIMESTAMP |     |
| updated_at     | TIMESTAMP |     |

---

## users

Purpose:
Stores all platform users.

| Field         | Type      | Key |
| ------------- | --------- | --- |
| user_id       | INT       | PK  |
| school_id     | INT       | FK  |
| first_name    | VARCHAR   |     |
| middle_name   | VARCHAR   |     |
| last_name     | VARCHAR   |     |
| email         | VARCHAR   |     |
| phone         | VARCHAR   |     |
| password_hash | VARCHAR   |     |
| gender        | VARCHAR   |     |
| date_of_birth | DATE      |     |
| profile_photo | TEXT      |     |
| status        | VARCHAR   |     |
| created_at    | TIMESTAMP |     |
| updated_at    | TIMESTAMP |     |

FK:

* school_id → schools.school_id

---

## roles

Purpose:
Stores system roles.

| Field            | Type    | Key |
| ---------------- | ------- | --- |
| role_id          | INT     | PK  |
| role_name        | VARCHAR |     |
| role_description | TEXT    |     |

Examples:

* Principal
* Deputy Principal
* Teacher
* Student
* Parent
* Librarian
* Bursar

---

## permissions

Purpose:
Stores available system permissions.

| Field           | Type    | Key |
| --------------- | ------- | --- |
| permission_id   | INT     | PK  |
| permission_name | VARCHAR |     |
| description     | TEXT    |     |

---

## user_roles

Purpose:
Links users to roles.

| Field        | Type | Key |
| ------------ | ---- | --- |
| user_role_id | INT  | PK  |
| user_id      | INT  | FK  |
| role_id      | INT  | FK  |

FK:

* user_id → users.user_id
* role_id → roles.role_id

---

## role_permissions

Purpose:
Links roles to permissions.

| Field              | Type | Key |
| ------------------ | ---- | --- |
| role_permission_id | INT  | PK  |
| role_id            | INT  | FK  |
| permission_id      | INT  | FK  |

FK:

* role_id → roles.role_id
* permission_id → permissions.permission_id

---

# STUDENT INFORMATION SYSTEM

## students

Purpose:
Stores student-specific information.

| Field                    | Type    | Key |
| ------------------------ | ------- | --- |
| student_id               | INT     | PK  |
| user_id                  | INT     | FK  |
| admission_number         | VARCHAR |     |
| current_class_id         | INT     | FK  |
| house_id                 | INT     | FK  |
| dormitory_id             | INT     | FK  |
| admission_date           | DATE    |     |
| expected_graduation_year | INT     |     |
| status                   | VARCHAR |     |

---

## parents

Purpose:
Stores parent-specific information.

| Field             | Type    | Key |
| ----------------- | ------- | --- |
| parent_id         | INT     | PK  |
| user_id           | INT     | FK  |
| occupation        | VARCHAR |     |
| employer          | VARCHAR |     |
| relationship_type | VARCHAR |     |

---

## student_parents

Purpose:
Links students and parents.

| Field             | Type | Key |
| ----------------- | ---- | --- |
| student_parent_id | INT  | PK  |
| student_id        | INT  | FK  |
| parent_id         | INT  | FK  |

---

## staff

Purpose:
Stores employee information.

| Field           | Type    | Key |
| --------------- | ------- | --- |
| staff_id        | INT     | PK  |
| user_id         | INT     | FK  |
| employee_number | VARCHAR |     |
| employment_date | DATE    |     |
| department_id   | INT     | FK  |
| qualification   | VARCHAR |     |
| specialization  | VARCHAR |     |

---

# ACADEMIC MODULE

## departments

| Field           | Type    | Key |
| --------------- | ------- | --- |
| department_id   | INT     | PK  |
| department_name | VARCHAR |     |
| description     | TEXT    |     |

---

## classes

| Field            | Type    | Key |
| ---------------- | ------- | --- |
| class_id         | INT     | PK  |
| class_name       | VARCHAR |     |
| stream           | VARCHAR |     |
| academic_year    | INT     |     |
| class_teacher_id | INT     | FK  |

---

## subjects

| Field         | Type    | Key |
| ------------- | ------- | --- |
| subject_id    | INT     | PK  |
| subject_name  | VARCHAR |     |
| subject_code  | VARCHAR |     |
| department_id | INT     | FK  |

---

## teacher_subjects

Purpose:
Links teachers and subjects.

| Field              | Type | Key |
| ------------------ | ---- | --- |
| teacher_subject_id | INT  | PK  |
| staff_id           | INT  | FK  |
| subject_id         | INT  | FK  |

---

# ATTENDANCE MODULE

## attendance

| Field           | Type    | Key |
| --------------- | ------- | --- |
| attendance_id   | INT     | PK  |
| student_id      | INT     | FK  |
| class_id        | INT     | FK  |
| attendance_date | DATE    |     |
| status          | VARCHAR |     |
| recorded_by     | INT     | FK  |

---

# LIBRARY MODULE

## books

| Field     | Type    | Key |
| --------- | ------- | --- |
| book_id   | INT     | PK  |
| isbn      | VARCHAR |     |
| title     | VARCHAR |     |
| author    | VARCHAR |     |
| publisher | VARCHAR |     |
| category  | VARCHAR |     |
| quantity  | INT     |     |

---

## book_loans

| Field       | Type | Key |
| ----------- | ---- | --- |
| loan_id     | INT  | PK  |
| book_id     | INT  | FK  |
| student_id  | INT  | FK  |
| issued_by   | INT  | FK  |
| issue_date  | DATE |     |
| due_date    | DATE |     |
| return_date | DATE |     |

---

# FINANCE MODULE

## fee_structures

| Field            | Type    | Key |
| ---------------- | ------- | --- |
| fee_structure_id | INT     | PK  |
| class_id         | INT     | FK  |
| amount           | DECIMAL |     |
| academic_year    | INT     |     |

---

## payments

| Field                 | Type      | Key |
| --------------------- | --------- | --- |
| payment_id            | INT       | PK  |
| student_id            | INT       | FK  |
| amount                | DECIMAL   |     |
| payment_method        | VARCHAR   |     |
| transaction_reference | VARCHAR   |     |
| payment_date          | TIMESTAMP |     |

---

# COMMUNICATION MODULE

## conversations

| Field             | Type    | Key |
| ----------------- | ------- | --- |
| conversation_id   | INT     | PK  |
| conversation_type | VARCHAR |     |

---

## messages

| Field           | Type      | Key |
| --------------- | --------- | --- |
| message_id      | INT       | PK  |
| conversation_id | INT       | FK  |
| sender_id       | INT       | FK  |
| message_content | TEXT      |     |
| created_at      | TIMESTAMP |     |

---

# HOSTEL MODULE

## hostels

| Field       | Type    | Key |
| ----------- | ------- | --- |
| hostel_id   | INT     | PK  |
| hostel_name | VARCHAR |     |
| hostel_type | VARCHAR |     |

---

## rooms

| Field     | Type    | Key |
| --------- | ------- | --- |
| room_id   | INT     | PK  |
| hostel_id | INT     | FK  |
| room_name | VARCHAR |     |
| capacity  | INT     |     |

---

## room_assignments

| Field         | Type | Key |
| ------------- | ---- | --- |
| assignment_id | INT  | PK  |
| student_id    | INT  | FK  |
| room_id       | INT  | FK  |
| assigned_date | DATE |     |

---

# CLUBS & ACTIVITIES

## clubs

| Field     | Type    | Key |
| --------- | ------- | --- |
| club_id   | INT     | PK  |
| club_name | VARCHAR |     |
| patron_id | INT     | FK  |

---

## club_memberships

| Field         | Type | Key |
| ------------- | ---- | --- |
| membership_id | INT  | PK  |
| club_id       | INT  | FK  |
| student_id    | INT  | FK  |

---

# OPPORTUNET MODULE

## opportunities

| Field          | Type    | Key |
| -------------- | ------- | --- |
| opportunity_id | INT     | PK  |
| title          | VARCHAR |     |
| category       | VARCHAR |     |
| provider       | VARCHAR |     |
| deadline       | DATE    |     |
| description    | TEXT    |     |

---

## applications

| Field              | Type      | Key |
| ------------------ | --------- | --- |
| application_id     | INT       | PK  |
| opportunity_id     | INT       | FK  |
| student_id         | INT       | FK  |
| application_status | VARCHAR   |     |
| submitted_at       | TIMESTAMP |     |

---

# AI MODULE

## ai_interactions

| Field          | Type      | Key |
| -------------- | --------- | --- |
| interaction_id | INT       | PK  |
| user_id        | INT       | FK  |
| prompt         | TEXT      |     |
| response       | TEXT      |     |
| created_at     | TIMESTAMP |     |

---

# FUTURE MODULES

Future schema expansions:

* Inventory Management
* Health Records
* Transportation
* Learning Management System (LMS)
* Video Conferencing
* Digital Content Repository
* Predictive Analytics Engine

---

# Database Design Principles

1. Third Normal Form (3NF)
2. Role-Based Access Control (RBAC)
3. Multi-School Architecture
4. Auditability
5. Scalability
6. Security by Design
7. AI Integration Ready
8. Mobile & Offline Ready

---

Version: 1.0
Project: EduNexus
License: Proprietary (All Rights Reserved)

