# High-Level Architecture Overview

## Introduction
The PACCS (likely "Primary Agricultural Credit Cooperative Society" or similar) ecosystem is a comprehensive solution designed to manage credit and loan operations. It consists of a centralized backend server and two distinct frontend applications targeting different user personas.

## core Components

The ecosystem is built upon three main pillars:

1.  **PACCS Server (Backend)**
    *   **Role**: The central nervous system of the platform. It handles data persistence, business logic, authentication, and API services.
    *   **Tech Stack**: Python, FastAPI, SQLAlchemy (ORM), Alembic (Migrations).
    *   **Key Responsibilities**:
        *   User Authentication & Authorization (Admin, Employee, Client).
        *   Data management for Offices, Plans, Licenses, and Loans.
        *   Serving static web assets.
        *   Handling reporting and dashboard metrics.

2.  **PACCS Master App (Admin Interface)**
    *   **Role**: The administrative dashboard for managing the system.
    *   **Tech Stack**: Flutter (Mobile/Web/Desktop).
    *   **Key Responsibilities**:
        *   Full system configuration.
        *   Management of Offices, Employees, and Plans.
        *   License generation and management.
        *   Dashboard analytics and reporting.

3.  **PACCS Loan Calculator (Client Interface)**
    *   **Role**: A customer-facing application for loan details and calculations.
    *   **Tech Stack**: Flutter (Mobile/Web).
    *   **Key Responsibilities**:
        *   Loan eligibility and repayment calculation.
        *   Client authentication.
        *   Viewing loan details and history.

## Architecture Diagram (Conceptual)

```mermaid
graph TD
    User[End User / Admin] -->|Interacts with| ClientApp[Loan Calculator App]
    Admin[System Admin] -->|Interacts with| MasterApp[Master Admin App]
    
    ClientApp -->|REST API (JSON)| API_Gateway[FastAPI Server /v1]
    MasterApp -->|REST API (JSON)| API_Gateway
    
    subgraph "Backend Infrastructure"
        API_Gateway --> AuthLayer[Auth Middleware]
        AuthLayer --> Controllers[Route Controllers]
        Controllers --> Services[Business Logic Services]
        Services --> ORM[SQLAlchemy ORM]
        ORM --> DB[(Relational Database)]
    end
```

## Data Flow
1.  **Request**: The Flutter apps (Master or Loan Calc) initiate HTTP requests to the FastAPI server.
2.  **Processing**: The server validates the request via Pydantic schemas and checks authentication.
3.  **Logic**: Service layers execute the business rules (e.g., calculating interest, validating license).
4.  **Persistence**: Data is read from or written to the database using SQLAlchemy.
5.  **Response**: The server returns JSON responses to the client apps, which update the UI.
