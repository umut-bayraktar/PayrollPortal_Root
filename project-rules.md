# PayrollAI Project Rules

## Project Overview

This repository contains the development of a modern payroll platform.

Root structure:

PayrollAI/

* NewProject/
* OldProject/

The root repository is reserved for project-level documentation and rules.

Nested project repositories inside NewProject/ must remain independent and must not be tracked by the root repository.

OldProject contains legacy systems which must be analyzed but **not copied**.

NewProject will contain the new architecture and implementation.

The goal is to rebuild the entire payroll platform using modern technologies.

---

# Critical Rule

**Never copy legacy architecture. Only extract business logic.**

Legacy code must only be used to:

* understand payroll calculations
* identify domain rules
* understand integrations
* extract business logic

The legacy structure, patterns and architecture must **not** be reused.

---

# Repository Structure

OldProject contains:

### 1. BordroMainApiRestService-master

Legacy payroll backend.

Responsibilities:

* analyze payroll logic
* extract business rules
* identify API endpoints
* identify domain entities

This project will be **fully rewritten using .NET 10**.

---

### 2. BordroServiceRestApi-master

Service responsible for communication with **Logo ERP**.

Rules:

* do not rewrite
* analyze integration logic
* document endpoints
* improve if necessary
* integrate with the new backend architecture

---

### 3. BS-Ebordro-Fronted-main

Legacy Angular frontend.

Rules:

* analyze UI features
* extract functional requirements
* rebuild using **React**

---

# New Project Structure

All new development must be inside:

NewProject/

Structure:

NewProject/
backend/
frontend/

The frontend already contains a **Vercel template** and must be used as the base UI system.

Do not replace this template.

Instead integrate payroll features into the existing structure.

---

# Backend Technology Stack

Backend must be developed using:

.NET 10
ASP.NET Core Web API
MediatR
Entity Framework Core
Dapper
Serilog
JWT Authentication
Swagger / OpenAPI

---

# Backend Architecture

The backend must follow **Clean Architecture**.

Required layers:

Domain
Application
Infrastructure
API

### Domain Layer

Contains:

* Entities
* Value Objects
* Domain logic
* Domain services

No external dependencies allowed.

---

### Application Layer

Contains:

* CQRS commands
* CQRS queries
* Use cases
* DTOs
* Validation

Use **MediatR** for command/query handling.

---

### Infrastructure Layer

Contains:

* Database implementations
* EF Core configuration
* Dapper queries
* ERP integrations
* external services

---

### API Layer

Contains:

* Controllers
* Authentication
* Request models
* Response models

Controllers must remain **thin** and delegate logic to MediatR.

---

# Frontend Rules

Frontend exists in:

NewProject/frontend

The base project already includes a **Vercel template**.

Rules:

* do not replace the template
* extend it
* integrate payroll features into the existing design system
* ship frontend work as responsive by default

Responsive support is a project rule.

Every new or updated frontend surface must:

* work on mobile, tablet and desktop
* avoid horizontal overflow at common viewport widths
* keep primary actions visible and usable on touch devices
* stack grids, cards and tables safely for narrow screens
* preserve readable typography, spacing and hit targets on small screens

No frontend task is considered complete unless responsive behavior has been checked.

Technology stack:

React
TypeScript
Vite

---

# Frontend Architecture

Use a **feature-based structure**.

Example:

frontend/
features/
payroll/
employees/
auth/

Each feature should contain:

* components
* hooks
* api services
* types

---

# Integration Rules

The system must integrate with:

Logo ERP

Integration method:

SOAP services
XML data structures

Integration logic must remain inside the **Infrastructure layer**.

ERP-specific models must **not leak into Domain layer**.

---

# Logging Rules

Use **Serilog** for logging.

Log:

* errors
* warnings
* integration failures
* important business events

Never log sensitive information.

---

# Security Rules

Authentication must use:

JWT tokens

Authorization must support:

role based access

Users must only access their own payroll data.

---

# Database Rules

Use:

Entity Framework Core for write operations.

Use:

Dapper for high performance read queries.

Avoid complex business logic inside database queries.

---

# Code Quality Rules

All generated code must:

Follow SOLID principles
Use clear naming conventions
Avoid large classes
Avoid large methods
Be modular and maintainable

---

# Development Process

All development must follow this order:

Step 1
Analyze legacy projects inside OldProject.

Step 2
Extract business logic and domain rules.

Step 3
Design new architecture.

Step 4
Create backend project structure.

Step 5
Integrate ERP service.

Step 6
Extend frontend template.

Step 7
Implement payroll modules.

---

# Git Workflow Rule

Before starting a new development task, all completed changes in the relevant repository must be:

* committed
* pushed to GitHub

If backend and frontend are separate repositories, each repository must be handled independently.

If the task updates root-level documentation or rules, those root repository changes must also be committed and pushed before the next task starts.

The root repository should contain only root-level documents such as guides, architecture notes and project rules.

The root repository must not track:

* NewProject/
* OldProject/
* local tooling folders such as .dotnet-cli/

No new implementation work should begin while completed local changes are waiting to be committed and pushed.

---

# Output Expectations

When generating code the AI must provide:

1. Architecture explanation
2. Folder structure
3. Implementation plan
4. Generated code

Development must be **step by step**, not all at once.
