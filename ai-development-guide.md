# AI Development Guide

This document defines how AI coding agents must work when contributing to the PayrollAI project.

The purpose of this guide is to ensure that development is:

* structured
* maintainable
* architecture driven
* not influenced by legacy mistakes

All AI generated code must follow this guide.

---

# Core Development Rule

Legacy code exists only for **analysis**.

Never copy legacy architecture.

Only extract:

* business logic
* domain rules
* integration details

All implementation must follow the **new architecture**.

---

# Development Workflow

AI must follow the development phases below.

Do not skip steps.

---

# Git Workflow Requirement

Before starting a new task, the AI must check whether the relevant repository has completed local changes waiting to be synchronized.

Required action before new work begins:

* commit completed changes
* push them to GitHub

If backend and frontend use separate repositories, this rule applies to each repository separately.

If the task changes root-level documentation such as project rules, guides or architecture notes, the root repository must be committed and pushed as well.

The root repository is only for root-level documentation.

The AI must not add nested repositories like NewProject/ or OldProject/ into the root repository tracking.

The AI should avoid starting a fresh implementation on top of completed but unpushed work unless the user explicitly asks otherwise.

---

# Phase 1 — Legacy Analysis

Analyze all projects inside:

OldProject/

Projects:

BordroMainApiRestService-master
BordroServiceRestApi-master
BS-Ebordro-Fronted-main

Goals:

Understand the system.

Identify:

* payroll business rules
* domain entities
* integration endpoints
* API contracts
* payroll calculations

Output:

Document findings before writing new code.

---

# Phase 2 — Domain Modeling

Define the payroll domain.

Identify entities such as:

Employee
Payroll
PayrollItem
Deduction
Payment
SocialSecurityRecord

Create domain models based on **business logic**, not database schema.

---

# Phase 3 — Architecture Design

Design the backend architecture.

Required structure:

```id="sm6m6a"
backend/

Domain
Application
Infrastructure
API
```

Ensure dependency flow follows Clean Architecture.

---

# Phase 4 — Backend Initialization

Create the backend solution using **.NET 10**.

Required packages:

* MediatR
* EntityFrameworkCore
* Dapper
* Serilog
* FluentValidation
* JWT Authentication
* Swagger

Generate base structure for:

* commands
* queries
* handlers
* repositories

---

# Phase 5 — ERP Integration

Analyze:

BordroServiceRestApi-master

Identify:

* SOAP endpoints
* request/response structures
* authentication mechanisms

Create an **ERP Integration Client** inside Infrastructure layer.

ERP models must remain isolated from Domain.

---

# Phase 6 — Frontend Integration

Frontend is located in:

NewProject/frontend

The project already contains a **Vercel template**.

Rules:

Do not replace the template.

Extend the template with payroll functionality.

---

# Phase 7 — Feature Development

Develop features one module at a time.

Example order:

1. Authentication
2. Employee module
3. Payroll module
4. Payroll detail module
5. Reporting

Each feature must include:

Backend API
Application handlers
Frontend components

---

# Coding Guidelines

All generated code must follow:

SOLID principles
Clean Architecture
CQRS pattern

Controllers must be thin.

Business logic must exist only inside **Application layer**.

---

# Database Guidelines

Use:

Entity Framework Core for write operations.

Use:

Dapper for read-heavy queries.

Avoid complex logic inside SQL.

---

# Logging Guidelines

Use **Serilog**.

Log important events such as:

PayrollGenerated
PayrollUpdated
ERPIntegrationFailed

Do not log sensitive information.

---

# Security Guidelines

Authentication must use:

JWT tokens

Authorization must support:

role based access

Employees must only access their own payroll data.

---

# Frontend Development Rules

Frontend must follow:

React
TypeScript
Feature-based architecture

Example:

```id="82mpb9"
features/

auth
employees
payroll
```

Each feature must contain:

components
api services
hooks
types

Responsive support is mandatory.

When AI changes frontend code it must:

* design mobile first, then scale to tablet and desktop
* verify that layouts do not overflow horizontally
* ensure tables, cards, filters and forms remain usable on narrow screens
* keep buttons, links and interactive controls touch friendly
* treat responsive validation as part of done criteria, not an optional polish step

Localization support is also mandatory for all user-visible text.

When AI changes frontend code it must:

* route all user-facing copy through the localization system
* never leave hardcoded UI text inside components, pages, modals, menus, or validation flows
* update Turkish and English locale resources in the same task
* treat missing translation coverage as an incomplete implementation

---

# AI Output Format

When generating new code the AI must always provide:

1. Architecture explanation
2. Folder structure
3. Implementation plan
4. Generated code

Development must be incremental.

Never generate the entire system at once.

---

# Refactoring Rule

If legacy patterns appear in generated code:

Stop and refactor.

Do not allow legacy architecture to influence the new system.

---

# AI Behavior Expectations

AI must behave as:

Senior Software Architect
Senior .NET Engineer
System Designer

Focus on:

long term maintainability
clean architecture
clear module boundaries
