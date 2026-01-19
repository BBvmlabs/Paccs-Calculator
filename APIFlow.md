# API Flow & Structure

## Overview
The API is versioned (currently `v1`) and organized by domain resources. It follows RESTful principles using JSON for data exchange.

## Base URL
`/v1`

## API Modules

### 1. Authentication (`/auth`)
Handles user identity and session management.
*   **Login**: Validates credentials and issues JWT tokens.
*   **Refresh**: Refreshes expired access tokens.
*   **Logout**: Invalidates the current session.

### 2. Administrator (`/admin`)
Endpoints for system administrators.
*   **Dashboard**: aggregating system-wide metrics.
*   **Settings**: Global configuration updates.

### 3. Master Access (`/master`)
Likely for super-admin or "Master" level controls.
*   **Configuration**: High-level system toggles.

### 4. Office Management (`/office`)
Manages the organizational hierarchy.
*   **Create/Read/Update/Delete (CRUD)** operations for office branches.
*   **Listing**: Retrieving offices with filters.

### 5. Employee Management (`/employee`)
Manages staff members within offices.
*   **Onboarding**: Registering new employees.
*   **Profile**: Updating employee details and permissions.

### 6. Client/Member (`/client`)
Endpoints for the end-users (members).
*   **Profile**: Client personal information.
*   **Status**: Checking membership status.

### 7. Plans (`/plans`)
Defines the financial products available.
*   **Loan Plans**: configuration of interest rates, tenure, and limits.
*   **Investment Plans**: (If applicable) configuration of deposit schemes.

### 8. License & Device (`/license`)
Manages the software licensing and security.
*   **verify**: Checks if the current installation is valid.
*   **Register Device**: Links a hardware ID to a license.
*   **History**: Tracks usage log.

### 9. Report Issue (`/report_issue`)
Feedback loop.
*   **Submit**: Allows users/apps to report bugs or issues.

## Typical Request Flow

1.  **Client Request**:
    ```http
    POST /v1/auth/login
    Content-Type: application/json
    {
      "username": "user",
      "password": "***"
    }
    ```

2.  **Server Validation**:
    *   `Pydantic` schema validates the JSON body.
    *   If invalid -> `422 Unprocessable Entity`.

3.  **Controller Logic**:
    *   Hashes password.
    *   Queries `employee` or `admin` table.

4.  **Response**:
    ```json
    {
      "access_token": "ey...",
      "token_type": "bearer"
    }
    ```
