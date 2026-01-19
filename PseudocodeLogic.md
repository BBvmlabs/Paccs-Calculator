# Logic & Pseudocode Explanations

This document explains the core algorithms and logical flows within the PACCS ecosystem conceptually.

## 1. Loan Calculation Logic

The loan calculator determines the payable amount based on principal, interest rate, and duration.

**Pseudocode:**
```plaintext
FUNCTION CalculateLoan(principal, annual_rate, duration_months):
    monthly_rate = annual_rate / 12 / 100
    
    IF monthly_rate == 0:
        monthly_repayment = principal / duration_months
    ELSE:
        // Amortization Formula using Standard Method
        numerator = principal * monthly_rate * POW(1 + monthly_rate, duration_months)
        denominator = POW(1 + monthly_rate, duration_months) - 1
        monthly_repayment = numerator / denominator
    
    total_payable = monthly_repayment * duration_months
    total_interest = total_payable - principal
    
    RETURN {
        "monthly_emi": monthly_repayment,
        "total_amount": total_payable,
        "total_interest": total_interest
    }
END FUNCTION
```

## 2. License Verification Flow

The Master App and Server allow operations only if a valid license is present.

**Logic Flow:**
1.  **Client/App Startup**: App reads the locally stored `license_key`.
2.  **API Call**: App sends `license_key` + `device_id` to server `/v1/license/verify`.
3.  **Server Check**:
    *   Query Database for `license_key`.
    *   IF not found -> Return `INVALID`.
    *   IF found but `expiry_date` < `current_date` -> Return `EXPIRED`.
    *   IF `device_id` does not match registered device -> Return `DEVICE_MISMATCH`.
    *   ELSE -> Return `VALID`.

## 3. Authentication (JWT)

Standard Bearer Token authentication is used.

**Login Process:**
1.  User submits credentials.
2.  Server verifies hash(`password`) == stored_hash.
3.  Server generates a JSON Web Token (JWT) containing:
    *   `sub`: user_id
    *   `role`: admin / employee / client
    *   `exp`: expiration time (e.g., 24 hours)
4.  Client stores this token (e.g., in SecureStorage).
5.  **Subsequent Requests**: Client adds header `Authorization: Bearer <token>`.
6.  **Server Middleware**: Decodes token, checks `exp`, and injects user context into the request.

## 4. Office & Hierarchy Management

The system manages a tree-like structure of offices (e.g., Head Office -> Regional Office -> Branch).

**Logic:**
*   **Create Office**: An office must have a `parent_id` (unless it is the Root).
*   **Deletion**: An office cannot be deleted if it has active child offices or active employees/loans linked to it. Soft deletion (`is_active = false`) is preferred.
