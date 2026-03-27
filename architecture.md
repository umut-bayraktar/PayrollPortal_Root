# PayrollAI System Architecture

## Overview

PayrollAI is a modern payroll platform rebuilt from legacy systems.

Legacy projects located in **OldProject/** are used only for analysis and business logic extraction.

New development will be implemented in **NewProject/** using a modern architecture.

Primary goals:

* clean and maintainable architecture
* modular backend
* modern frontend
* ERP integration
* scalable system design

---

# System Components

The system consists of three main components.

1. Backend API
2. ERP Integration Layer
3. Frontend Application

```
Frontend (React)
        |
        v
Backend API (.NET 10)
        |
        v
ERP Integration Layer
        |
        v
Logo ERP
```

---

# Repository Structure

```
PayrollAI/

OldProject/
    BordroMainApiRestService-master
    BordroServiceRestApi-master
    BS-Ebordro-Fronted-main

NewProject/
    backend/
    frontend/
```

---

# Backend Architecture

Backend follows **Clean Architecture**.

```
API
Application
Domain
Infrastructure
```

Dependencies flow **inward only**.

```
API -> Application -> Domain
Infrastructure -> Application
```

Domain layer must not depend on any other layer.

---

# Backend Layer Responsibilities

## Domain Layer

Contains the core payroll business model.

Includes:

* entities
* value objects
* domain rules
* domain services

Example entities:

Employee
Payroll
PayrollItem
Deduction
Payment
SocialSecurityRecord

Example structure:

```
Domain/

Entities/
Employee.cs
Payroll.cs
PayrollItem.cs

ValueObjects/
Money.cs
PayrollPeriod.cs

Enums/
PayrollType.cs
DeductionType.cs
```

Domain layer must not contain:

* database logic
* API logic
* framework dependencies

---

## Application Layer

Responsible for business use cases.

Uses **CQRS pattern**.

Contains:

* commands
* queries
* DTOs
* validators
* handlers

Example structure:

```
Application/

Payroll/
Commands/
CreatePayrollCommand
UpdatePayrollCommand

Queries/
GetPayrollQuery
GetPayrollDetailsQuery

Handlers/
CreatePayrollHandler
GetPayrollDetailsHandler

DTOs/
PayrollDto
PayrollDetailDto
```

MediatR is used for command and query dispatching.

---

## Infrastructure Layer

Responsible for external dependencies.

Includes:

* database implementation
* Dapper queries
* ERP integration
* external services

Example structure:

```
Infrastructure/

Persistence/
PayrollDbContext

Repositories/

Integrations/
LogoERPClient

Queries/
PayrollQueries
```

ERP communication must stay in this layer.

---

## API Layer

Responsible for HTTP interface.

Includes:

* controllers
* authentication
* request models
* response models

Example structure:

```
API/

Controllers/
PayrollController
EmployeeController
AuthController

Middleware/
ExceptionHandlingMiddleware
```

Controllers must remain thin.

All business logic must go through **MediatR**.

---

# ERP Integration Architecture

The system integrates with **Logo ERP** through existing middleware.

Legacy service:

BordroServiceRestApi-master

Integration flow:

```
Backend API
      |
      v
ERP Integration Client
      |
      v
BordroServiceRestApi
      |
      v
Logo ERP
```

ERP communication methods may include:

* SOAP services
* XML data structures
* HTTP APIs

ERP models must remain **isolated inside Infrastructure layer**.

---

# Payroll Domain Model

Main entities:

Employee

Represents a company employee.

Fields:

EmployeeId
EmployeeCode
FirstName
LastName
SocialSecurityNumber

---

Payroll

Represents a payroll period for an employee.

Fields:

PayrollId
EmployeeId
Year
Month
GrossSalary
NetSalary

---

PayrollItem

Represents components of payroll.

Examples:

Salary
Bonus
Allowance
Tax
Insurance

---

Deduction

Represents payroll deductions.

Examples:

Tax
Insurance
UnionFee

---

SocialSecurityRecord

Represents government reporting data.

Includes:

SSK days
SSK base amount

---

# Data Flow

Typical payroll data flow:

```
ERP System
   |
   v
ERP Integration Client
   |
   v
Backend API
   |
   v
Application Layer
   |
   v
Domain Logic
   |
   v
Database
```

---

# Database Strategy

Use:

Entity Framework Core for writes.

Use:

Dapper for high performance reads.

Example:

Payroll list queries
Payroll reporting queries
Employee payroll history

---

# Frontend Architecture

Frontend is located in:

NewProject/frontend

A **Vercel template** is already present and must be used as the base system.

Frontend stack:

React
TypeScript
Vite

---

# Frontend Structure

Feature based architecture.

Example:

```
frontend/

features/

auth/
components
api
hooks

employees/
components
api
hooks

payroll/
components
api
hooks
```

---

# Frontend API Layer

All backend communication goes through a centralized API client.

Example:

```
services/

apiClient.ts
payrollApi.ts
employeeApi.ts
```

Responsibilities:

* API requests
* authentication headers
* error handling

---

# Security Architecture

Authentication:

JWT tokens

Authorization:

Role based access

Example roles:

Admin
HR
Employee

Employees must only see **their own payroll data**.

---

# Logging Strategy

Use **Serilog**.

Log:

* errors
* integration failures
* important payroll events

Example events:

PayrollGenerated
PayrollUpdated
ERPIntegrationFailed

---

# Future Expansion

Architecture must support:

* microservices transition
* additional ERP integrations
* payroll reporting services
* analytics modules

---

# AI Development Rule

When generating code:

Never copy legacy architecture.

Only extract business logic from OldProject.
