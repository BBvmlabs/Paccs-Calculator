# System Design & Diagrams

## Container Diagram

This diagram visualizes the high-level containers that make up the software architecture.

```mermaid
C4Context
    title System Context Diagram for PACCS

    Person(admin, "Administrator", "Manages the system, employees, and plans.")
    Person(client, "Client / Member", "Checks loan details and performs calculations.")
    
    System_Boundary(paccs_system, "PACCS Ecosystem") {
        Container(web_server, "FastAPI Server", "Python, Uvicorn", "Handles API requests and business logic.")
        Container(db, "Database", "Relational SQL", "Stores application data.")
        
        Container(master_app, "Master App", "Flutter", "Admin interface for system management.")
        Container(loan_app, "Loan Calculator", "Flutter", "Client interface for loan operations.")
    }

    Rel(admin, master_app, "Uses")
    Rel(client, loan_app, "Uses")
    
    Rel(master_app, web_server, "API Calls (HTTPS/JSON)")
    Rel(loan_app, web_server, "API Calls (HTTPS/JSON)")
    
    Rel(web_server, db, "Reads/Writes (SQL)")
```

## Component Diagram (Backend)

Architecture of the FastAPI Server `app` folder.

```mermaid
graph TD
    subgraph "FastAPI Application"
        Main[main.py Entry Point]
        
        subgraph "API Layer"
            Router[Routes /api/v1]
            AuthRouter[Auth Routes]
            AdminRouter[Admin Routes]
            LoanRouter[Loan Routes]
        end
        
        subgraph "Service Layer"
            AuthService[Auth Service]
            LoanService[Loan Calculation Logic]
            LicenseService[License Validation]
        end
        
        subgraph "Data Layer"
            Models[SQLAlchemy Models]
            Schemas[Pydantic Schemas]
            DB_Session[Database Session]
        end
    end

    Main --> Router
    Router --> AuthRouter & AdminRouter & LoanRouter
    
    AuthRouter --> AuthService
    LoanRouter --> LoanService
    
    AuthService --> Models
    LoanService --> Models
    
    Models --> DB_Session
```

## Entity Relationship Diagram (ERD) - Conceptual

Abstracted view of the data model based on codebase analysis.

```mermaid
erDiagram
    ADMIN ||--o{ OFFICE : manages
    OFFICE ||--o{ EMPLOYEE : employs
    EMPLOYEE ||--o{ LOAN : processes
    
    MASTER_CONFIG ||--|{ PLAN : defines
    PLAN ||--o{ LOAN : governs
    
    LICENSE ||--|{ DEVICE : authorizes
    LICENSE {
        string key
        date expiry
        string status
    }
    
    LOAN {
        float amount
        float interest_rate
        int duration
    }
```
