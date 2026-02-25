

# Developer Guide

This section describes how a new contributor can join the Popcorn Meter development team and start contributing effectively. It defines team conventions, environment setup, workflow, and communication standards.

----------

# 1. Project Overview for Contributors

Popcorn Meter is a layered Python web application built with:

-   **Streamlit** (UI layer)
    
-   **Application Service layer** (business logic)
    
-   **SQLite repository layer** (persistence)
    
-   **OMDb API integration**
    
-   **GitHub Actions CI/CD**
    
-   **Poetry-based dependency management**
    

The project follows:

-   Layered architecture
    
-   Feature-branch workflow
    
-   Automated CI validation
    
-   Semantic versioning for releases
    

----------

# 2. Team Organization & Communication

## 2.1 Communication Channels

In a professional setting, the team uses:

-   GitHub Issues for bug reports and feature requests
    
-   GitHub Pull Requests for code review discussions
    
-   Email or Slack for internal coordination
    

Primary contact:

-   Project Maintainer (Team Lead): [[kosar.mazahery@studio.unibo.it](mailto:example@email.com)]
    
-   Technical Owner (CI/CD): [[ethar.ali@studio.unibo.it](mailto:example@email.com)]
    

----------

## 2.2 Reporting Issues

To report a bug:

1.  Navigate to the GitHub repository.
    
2.  Open a new Issue.
    
3.  Use the following template:
    

```
Title: [BUG] Short description

Environment:
- OS:
- Python version:
- Branch:

Steps to reproduce:
1.
2.
3.

Expected behavior:
Actual behavior:

```

For feature requests:

```
Title: [FEATURE] Description

Problem:
Proposed solution:
Impact on architecture:

```

----------

# 3. Development Environment Setup

## 3.1 Prerequisites

A contributor must have:

-   Python 3.10+ installed
    
-   Git
    
-   Poetry
    
-   Node.js (required for semantic-release)
    
-   A GitHub account
    

Optional:

-   VS Code or PyCharm
    

----------

## 3.2 Cloning the Repository

```bash
git clone https://github.com/<organization>/popcorn-meter.git
cd popcorn-meter

```

----------

## 3.3 Installing Dependencies

The project uses Poetry for dependency management.

```bash
pip install poetry
poetry install

```

This creates a virtual environment and installs all required dependencies.

To activate the environment:

```bash
poetry shell

```

----------

## 3.4 Environment Variables

To use OMDb integration locally:

Create:

```
.streamlit/secrets.toml

```

Add:

```toml
OMDB_API_KEY = "your_key_here"

```

The `.streamlit/` directory is excluded from version control via `.gitignore`.

----------

# 4. Running the Application

To run locally:

```bash
python -m streamlit run popcorn_meter/ui/streamlit_app.py

```

The app will be available at:

```
http://localhost:8501

```

----------

# 5. Running Tests

All tests must pass before creating a Pull Request.

Run:

```bash
poetry run pytest

```

Or using the Poetry task runner:

```bash
poetry run poe test

```

To generate coverage:

```bash
poetry run poe coverage

```

CI will reject changes if tests fail.

----------

# 6. Coding Standards & Conventions

## 6.1 Architecture Rules

Developers must respect the layered architecture:

-   UI must NOT directly access the database.
    
-   UI must call only `AppService`.
    
-   `AppService` must not contain SQL.
    
-   Database queries must be inside `SqliteRepo`.
    
-   External API calls must be inside `OmdbClient`.
    

----------

## 6.2 Naming Conventions

-   Classes → PascalCase (`AppService`)
    
-   Methods → snake_case (`add_to_watchlist`)
    
-   Constants → UPPER_CASE (`ALL_GENRES`)
    
-   Feature branches → `feature/<short-description>`
    
-   Bugfix branches → `fix/<short-description>`
    

----------

## 6.3 Type Safety

-   All public methods must include type hints.
    
-   Mypy must pass (CI enforces static checks).
    

----------

## 6.4 Code Quality

-   No commented-out legacy code
    
-   No hardcoded credentials
    
-   No direct SQL outside repository layer
    
-   Meaningful commit messages
    

----------

# 7. Development Workflow

## 7.1 Branching Strategy

Main branches:

-   `master` → stable release branch
    
-   `develop` → integration branch
    
-   `feature/*` → new features
    
-   `fix/*` → bug fixes
    

----------

## 7.2 Creating a Feature Branch

```bash
git checkout develop
git pull origin develop
git checkout -b feature/add-search-filter

```

----------

## 7.3 Committing Changes

Commit messages must follow semantic style:

```
feat: add advanced genre filtering
fix: correct login validation bug
refactor: separate recommendation logic

```

----------

## 7.4 Pushing Changes

```bash
git add .
git commit -m "feat: add watchlist sorting"
git push --set-upstream origin feature/add-watchlist-sorting

```

----------

## 7.5 Creating a Pull Request

1.  Push branch to GitHub.
    
2.  Open Pull Request targeting `develop`.
    
3.  Ensure CI passes.
    
4.  Request review from at least one team member.
    
5.  Merge only after approval.
    

----------

# 8. CI/CD Rules

-   Pull Requests cannot be merged if CI fails.
    
-   All tests must pass on all OS + Python versions.
    
-   Coverage should not decrease significantly.
    
-   Only maintainers can merge to `master`.
    

Releases are generated automatically via semantic-release.

----------

# 9. Development Tools

## 9.1 Recommended IDE Configuration

For VS Code:

Recommended extensions:

-   Python
    
-   Pylance
    
-   GitLens
    

Enable:

-   Format on Save
    
-   Type checking
    

Interpreter:

-   Select Poetry virtual environment.
    

----------

## 9.2 Command Line Usage

Common commands:

```bash
git pull
git fetch
git checkout
poetry install
pytest

```

Developers are expected to be comfortable with Git CLI.

----------

# 10. Onboarding Checklist for New Developers

1.  Clone repository
    
2.  Install Poetry
    
3.  Install dependencies
    
4.  Configure OMDb key
    
5.  Run tests
    
6.  Run application locally
    
7.  Create first feature branch
    


    

    

