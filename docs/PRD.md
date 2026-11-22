# Product Requirements Document (PRD)

## Music Revenue Manager (MRM)

**Version:** 1.0  
**Project Type:** Academic / Web Application  
**Technology:** Django, Django Templates, Tailwind CSS, HTMX, PostgreSQL

### 1. Project Overview

Music Revenue Manager (MRM) is a web-based platform designed to help independent musicians, music producers, and collaborators manage music-related revenue, expenses, royalty agreements, and financial settlements.

The system provides a centralized platform for tracking music projects, managing contributors, defining royalty splits, calculating earnings, and generating settlement records.

### 2. Problem Statement

Independent musicians often manage their earnings, expenses, royalty agreements, and collaborator payments manually using spreadsheets or separate tools.

This can lead to calculation errors, unclear ownership percentages, payment disputes, and difficulties tracking outstanding expenses.

MRM aims to simplify these processes through a centralized and structured management system.

### 3. Project Objectives

- Centralize music projects, tracks, and contributor information.
- Manage royalty agreements and revenue-sharing percentages.
- Track revenue and expenses for individual projects and tracks.
- Automate royalty calculations and settlement generation.
- Support expense recoupment before applicable profit distributions.
- Maintain transparent financial and agreement records.

### 4. Target Users

| User | Responsibilities |
|---|---|
| Administrator | Manage users and oversee the platform. |
| Project Owner / Manager | Create projects, manage tracks, contributors, agreements, and finances. |
| Contributor | View assigned projects, royalty shares, and settlement information (if they have an MRM account; contributors without an account can still be added to projects). |

### 5. Core Functional Requirements

**5.1 User Management**
- User registration, login, and authentication.
- Role-based access and permissions.
- User profile management.

**5.2 Project & Track Management**
- Create and manage music projects.
- Add individual tracks to projects.
- Assign contributors and their respective roles.
- Track project and track information.

**5.3 Contributor & Royalty Management**
- Add contributors to projects and tracks.
- Define royalty percentages for contributors.
- Validate that applicable royalty splits total exactly 100%.

> In the MVP, each project has one active royalty agreement at a time. Its percentages apply uniformly to all revenue recorded under that project, including revenue associated with individual tracks. Agreements are versioned by effective date: once locked, an agreement is never edited, and corrections create a new version that applies from its effective date. Track-specific agreements will be introduced in Phase 2.

**5.4 Revenue & Expense Management**
- Record revenue from different sources.
- Record project-related expenses.
- Associate financial transactions with projects, optionally tagged to a track.
- View revenue, expenses, and financial summaries.

**5.5 Recoupment & Settlement**
- Calculate contributor earnings based on approved royalty agreements.
- Calculate outstanding recoupable expenses.
- Apply the defined recoupment rules to each contributor's earnings.
- Generate settlement records and payment summaries.

**5.6 Reports & Documentation**
- Generate project-wise financial reports.
- Display contributor earnings and settlement history.
- Generate agreement and settlement documents.

### 6. Non-Functional Requirements

- **Security:** Authentication and role-based authorization.
- **Accuracy:** Reliable financial and royalty calculations.
- **Usability:** Simple, understandable, and responsive interface.
- **Performance:** Efficient handling of project and financial records.
- **Data Integrity:** Proper validation and consistent database relationships.
- **Maintainability:** Modular architecture for future improvements.

### 7. Project Scope

**MVP Features:**
1. User authentication and basic project roles
2. Project and track management
3. Contributor management
4. Project-level royalty agreements with versioning by effective date
5. Revenue recording
6. Single-payer project expenses
7. Royalty calculation and simple expense recoupment
8. Reimbursement tracking
9. Settlement generation and full-payment recording
10. Basic financial summaries

**Phase 2 Features:**
- Track-specific royalty agreements
- Custom expense allocation percentages
- Individual contributor expenses and advances
- Multiple payers for an expense
- Configurable recoupment priority
- Partial settlements and payments
- Advanced reports and document generation
- Certificates, signatures, and compensation claim records
- External platform and payment integrations

**Outside the initial scope:**
- Direct integration with music streaming platforms.
- Automatic collection of streaming royalties.
- Actual bank transfers and payment processing.
- Blockchain-based royalty management.
- Advanced third-party accounting integrations.

### 8. Expected Outcome

The expected outcome is a functional web application that allows independent music creators to organize their projects, manage royalty agreements, track financial activities, and generate accurate and transparent settlement records through a centralized platform.
