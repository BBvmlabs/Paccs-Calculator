# Contribution Guidelines

## Getting Started

We welcome contributions to improve the PACCS ecosystem. Please follow these guidelines to ensure a smooth workflow.

## Version Control

### Branching Strategy
*   **main**: Production-ready code. Do not push directly here.
*   **develop** (or equivalent): Integration branch for testing.
*   **feature/your-feature-name**: Use for new features.
*   **fix/bug-name**: Use for bug fixes.

### Commit Messages
Follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:
*   `feat: add new loan calculator logic`
*   `fix: resolve api connection timeout`
*   `docs: update setup guide`
*   `style: format code according to linter`

## Code Standards

### Backend (Python)
*   follows **PEP 8** style guidelines.
*   Use type hints (`from typing import ...`) for all function signatures.
*   Ensure all new endpoints have corresponding Pydantic schemas.

### Frontend (Flutter/Dart)
*   Follow [Effective Dart](https://dart.dev/guides/language/effective-dart) style.
*   Use `const` constructors where possible to improve performance.
*   Separate business logic (BLoC/Provider) from UI Widgets.

## Pull Request Process
1.  Ensure your branch is up to date with `main`.
2.  Run tests locally.
3.  Create a Pull Request (PR) with a clear description of changes.
4.  Link related issues.
5.  Wait for code review and approval.

## CI/CD (Abstracted Implementation)

Example workflow file structure for GitHub Actions:

```yaml
# .github/workflows/ci.yml example
name: CI Pipeline

on: [push, pull_request]

jobs:
  backend-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.9'
      - name: Install dependencies
        run: |
          cd paccs_fastapi_server
          pip install -r requirements.txt
      - name: Run Tests
        run: |
          cd paccs_fastapi_server
          pytest

  frontend-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: subosito/flutter-action@v1
      - name: Authenticate & Install
        run: |
          cd paccs_master_app
          flutter pub get
      - name: Analyze
        run: |
          cd paccs_master_app
          flutter analyze
```
