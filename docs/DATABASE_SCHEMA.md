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

# DATABASE_SCHEMA.md

# EduNexus Database Schema

## Overview

EduNexus is a multi-school education operating system designed to manage the complete lifecycle of a learner, educator, parent, and institution.

The database architecture is organized into eleven interconnected layers, each responsible for a specific domain of the platform.

The schema is implemented using DBML and can be exported to PostgreSQL, MySQL, SQL Server, and other relational database systems.

---

# Database Design Principles

The EduNexus database follows the following principles:

1. Multi-Tenant Architecture
2. Third Normal Form (3NF)
3. Role-Based Access Control (RBAC)
4. Auditability & Traceability
5. Modular Feature Activation
6. School-Type Flexibility
7. AI-Ready Data Structures
8. Scalable Cloud Architecture
9. Security by Design
10. API-First Development

---

# Layer 1 — Core Foundation

Purpose:

Provides the identity and access foundation of the platform.

Core Tables:

* schools
* users
* roles
* permissions
* user_roles
* role_permissions

Responsibilities:

* School registration
* User management
* Authentication
* Authorization
* Role assignment

---

# Layer 2 — Academic Management System

Purpose:

Manages academic operations.

Core Tables:

* academic_years
* terms
* academic_events
* departments
* staff
* classes
* students
* parents
* subjects
* teacher_subjects
* assignments
* exams
* results
* timetables
* timetable_entries
* learning_resources
* student_documents

Responsibilities:

* Academic calendar
* Student records
* Subject management
* Timetable generation
* Examination management
* Performance tracking

---

# Layer 3 — Communication & Collaboration

Purpose:

Provides communication between stakeholders.

Core Tables:

* conversations
* conversation_participants
* messages
* message_reads
* announcements
* notifications
* meetings
* meeting_participants

Responsibilities:

* Messaging
* School announcements
* Parent communication
* Virtual meetings
* Notification delivery

---

# Layer 4 — Finance Management

Purpose:

Manages financial transactions.

Core Tables:

* fee_categories
* fee_structures
* student_invoices
* invoice_items
* payments
* receipts
* scholarships
* student_scholarships
* fee_waivers

Responsibilities:

* Fee management
* Payment tracking
* Scholarships
* Waivers
* Financial reporting

---

# Layer 5 — Knowledge Resource Management

Purpose:

Manages all school learning resources.

Subsystems:

## Library

Reference books and reading resources.

Tables:

* books
* book_copies
* book_loans
* book_reservations
* library_fines

## Book Bank

Curriculum textbooks distributed to students.

Tables:

* book_store_items
* book_store_issues
* syllabus_completion
* book_replacements

## Book Sales Store

Optional school-operated textbook sales.

Tables:

* book_sales_inventory
* book_sales_transactions

## Digital Resources

Tables:

* digital_resources
* media_files

Responsibilities:

* Lending
* Returning
* Inventory control
* Textbook lifecycle tracking
* Digital content management

---

# Layer 6 — Boarding & Student Welfare

Purpose:

Supports boarding schools.

Core Tables:

* hostels
* rooms
* beds
* boarding_students
* bed_assignments
* leave_out_requests
* hostel_roll_calls
* hostel_visitors
* hostel_inspections

Responsibilities:

* Bed allocation
* Roll call management
* Leave requests
* Hostel discipline
* Boarding operations

---

# Layer 7 — Clubs, Sports & Student Life

Purpose:

Manages extracurricular activities.

Core Tables:

* houses
* clubs
* club_memberships
* sports_teams
* sports_team_members
* events
* competitions
* achievements
* certificates

Responsibilities:

* Clubs
* Sports
* Competitions
* Student leadership
* Awards and recognition

---

# Layer 8 — Opportunet Platform

Purpose:

Connects learners to opportunities.

Core Tables:

* opportunity_providers
* opportunities
* opportunity_tags
* applications
* mentors
* recommendation_requests
* student_profiles
* opportunity_matches

Responsibilities:

* Scholarships
* Internships
* Competitions
* Mentorship
* University opportunities

---

# Layer 9 — AI & Analytics Engine

Purpose:

Provides intelligence and predictive insights.

Core Tables:

* student_ai_profiles
* learning_insights
* risk_predictions
* opportunity_recommendations
* learning_paths
* ai_summaries
* ai_chart_datasets
* behavior_patterns

Responsibilities:

* Student analytics
* Performance prediction
* Dropout prediction
* Opportunity matching
* AI reporting

---

# Layer 10 — Governance, Security & Platform Control

Purpose:

Provides enterprise-grade governance.

Core Tables:

* school_features
* policies
* policy_statements
* user_policies
* role_policies
* audit_logs
* user_sessions
* suspicious_activity_logs
* ui_layouts
* ui_components
* ai_next_actions

Responsibilities:

* IAM permissions
* Security monitoring
* Audit trails
* Dynamic UI generation
* Feature management
* AI personalization

---

# Layer 11 — Integration & Infrastructure Layer

Purpose:

Connects EduNexus with external systems.

Core Tables:

* api_integrations
* external_data_sync

Optional Modules:

* Transport Management
* Meal Services
* Inventory Management
* Future Healthcare Module

Responsibilities:

* API connectivity
* Data synchronization
* Third-party integrations
* Future expansion support

---

# Relationship Strategy

The database follows a hub-and-spoke model.

Primary hub tables:

* schools
* users
* students
* staff
* classes

Most modules connect through these entities to maintain consistency across the platform.

---

# Source of Truth

The official database definition is maintained in:

database/edunexus.dbml

Generated SQL schemas must always be produced from the DBML file to ensure consistency across environments.

---

Version: 2.0

Project: EduNexus

Architecture: Multi-School Education Operating System

Database Model: Relational (DBML)

Status: Active Development
