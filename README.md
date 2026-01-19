# PACCS Calculator Ecosystem Documentation

## 📚 Project Overview
The PACCS (Primary Agricultural Credit Cooperative Society) ecosystem is a comprehensive digital solution designed to streamline credit and loan operations for cooperative societies. It bridges the gap between complex financial calculations and user-friendly interfaces, providing robust tools for administrators, employees, and clients.

The ecosystem is built on a modern **Client-Server Architecture** consisting of three core components:
1.  **PACCS Server**: A central FastAPI backend handling logic, data, and authentication.
2.  **PACCS Master App**: An administrative dashboard for total system management.
3.  **PACCS Loan Calculator**: A specialized client-side application for precision loan management.

## 🏗️ System Architecture

### Core Components
-   **PACCS Server (Backend)**:
    -   Built with **Python & FastAPI**.
    -   Manages authentication, licenses, office data, and business logic.
    -   Serves as the central source of truth.

-   **PACCS Master App (Admin)**:
    -   Built with **Flutter**.
    -   Used by administrators to generate licenses, manage offices, and track plan usage.

-   **PACCS Loan Calculator (Client)**:
    -   Built with **Flutter**.
    -   The primary tool for end-users to calculate loans, generate reports, and manage daily operations.

---

## 🔍 Deep Dive: PACCS Loan Calculator

The project is the client-facing front-end of the ecosystem. It is designed to be visually engaging ("Precision Lending, Made Simple") while providing rigorous financial accuracy.

### 🌟 Key Features

#### 1. Smart Calculation Engine
-   **Automated Logic**: Users can perform complex interest and EMI calculations without manual errors.
-   **Flexible Parameters**: The calculator accepts custom inputs to adapt to various loan types and schemes supported by the society.

#### 2. Detailed Reporting & auditing
-   **PDF Generation**: The app allows users to generate professional-grade PDF reports.
-   **Audit Ready**: Reports are designed to meet audit standards, making record-keeping effortless.

#### 3. Security & Licensing
-   **Local & Secure**: Data is primarily stored locally for privacy, but access is controlled via a strict **License Verification** system.
-   **Device Quotas**: The app implements a check (via `LICENSE_FLOW_IMPLEMENTATION.md`) to limit the number of active devices (Mobile, Laptop, Web) per license.
-   **Fresh Token Security**: Uses a "Fresh Token" flow (analyzed in `FRESH_TOKEN_LOGIN_FLOW.md`) where the app authenticates the *device* before the *user*, ensuring a secure handshake.

#### 4. Responsive & Modern UI
-   **Cross-Platform Adaptive**: The `LandingScreen` implements specific layouts for **Desktop** and **Mobile** using `LayoutBuilder`.
    -   **Desktop**: Features a comprehensive navbar, side-by-side hero section, and expanded feature cards.
    -   **Mobile**: Optimized simplified navbar, stacked layout, and touch-friendly controls.
-   **Rich Aesthetics**:
    -   **Typography**: Uses `GoogleFonts` (Poppins, Inter, Manrope) for a clean, professional look.
    -   **Animations**: Integrates `Lottie` animations (e.g., `loan_payment.json`) to make the interface dynamic and welcoming.

### 🛠️ Technical Implementation
-   **Framework**: Flutter (SDK ^3.5.1).
-   **Routing**: `go_router` manages complex navigation flows (Login -> Verify License -> Dashboard).
-   **State Management**: `flutter_riverpod` handles app state efficiently.
-   **Assets**: Centrally managed images and animations in `src/assets/`.

## 📂 Documentation Resources
This folder (`Paccs-Calculator`) contains high-level documentation helping developers understand the broader context:
-   `HighLevelArchitecture.md`: System-wide diagrams and component roles.
-   `SystemDesign.md`: Detailed module breakdowns.
-   `ProjectFlowChart.md`: Visual flows of user interactions.
-   `PseudocodeLogic.md`: Algorithmic explanations of core business rules.
