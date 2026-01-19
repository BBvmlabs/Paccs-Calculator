# Setup Guide

## Prerequisites
*   **OS**: Linux (Preferred), MacOS, or Windows.
*   **Languages**:
    *   Python 3.9+ (for Backend)
    *   Flutter SDK (for Mobile/Web Apps)
*   **Database**: SQLite (default for dev) or PostgreSQL (production).

## 1. Backend Server Setup (`paccs_fastapi_server`)

### Installation
1.  Navigate to the server directory:
    ```bash
    cd paccs_fastapi_server
    ```

2.  Create a virtual environment:
    ```bash
    python3 -m venv .venv
    source .venv/bin/activate
    ```

3.  Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```

### Configuration
Create a `.env` file based on the example (or internal config):
```ini
# .env example
SECRET_KEY=your_secret_key_here
DATABASE_URL=sqlite:///./storage/paccs.db
DEBUG=True
```

### Database Migration
Run Alembic to create the database schema:
```bash
alembic upgrade head
```

### Running the Server
```bash
uvicorn main:app --reload
```
The API will be available at `http://localhost:8000/v1`.
Documentation (Swagger UI) at `http://localhost:8000/docs`.

---

## 2. Master App Setup (`paccs_master_app`)

### Installation
1.  Navigate to the app directory:
    ```bash
    cd paccs_master_app
    ```

2.  Install Flutter dependencies:
    ```bash
    flutter pub get
    ```

### Running
*   **Web**:
    ```bash
    flutter run -d chrome
    ```
*   **Desktop (Linux)**:
    ```bash
    flutter run -d linux
    ```

---

## 3. Loan Calculator Setup (`pacs_loan_calc`)

### Installation
1.  Navigate to the directory:
    ```bash
    cd pacs_loan_calc
    ```

2.  Install dependencies:
    ```bash
    flutter pub get
    ```

### Running
```bash
flutter run
```

## Troubleshooting

*   **Port Conflicts**: Ensure port 8000 is free or change the port in the start command (`--port 8081`).
*   **Flutter Doctor**: Run `flutter doctor` to verify your environment health.
