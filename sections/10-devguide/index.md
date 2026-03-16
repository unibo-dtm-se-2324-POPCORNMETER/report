---
title: Devguide
has_children: false
nav_order: 11
---

# Developer Guide

This section explains how a new developer can join the **Popcorn Meter** development team and start contributing to the project. It describes the development environment, repository workflow, coding conventions, and collaboration practices used by the team.

----------

# 1. Project Overview for Contributors

Popcorn Meter is a **layered Python web application** designed to provide movie recommendations based on user preferences and viewing history.

The system is implemented using the following technologies:

-   **Streamlit** — user interface layer
    
-   **Application Service layer (`AppService`)** — business logic and use cases
    
-   **SQLite repository (`SqliteRepo`)** — persistence layer
    
-   **OMDb API / TMDb API integration** — movie data retrieval
    
-   **Poetry** — dependency and environment management
    
-   **GitHub Actions** — CI/CD automation
    
-   **Semantic release** — automated versioning and release generation
    

The project follows these architectural and development principles:

-   Layered architecture
    
-   Separation of UI, business logic, and persistence
    
-   Feature-branch development workflow
    
-   Automated testing and CI validation
    
-   Semantic versioning for releases
    

----------

# 2. Team Organization & Communication

## 2.1 Communication Channels

In a professional environment, communication is organized through the following channels:

-   **GitHub Issues** — bug reports and feature requests
    
-   **GitHub Pull Requests** — code reviews and implementation discussions
    
-   **Email or Slack** — internal coordination
    

Primary contacts:

**Team Member:** [kosar.mazahery@studio.unibo.it](mailto:kosar.mazahery@studio.unibo.it)

**Team Member:** [ethar.ali@studio.unibo.it](mailto:ethar.ali@studio.unibo.it)

----------

## 2.2 Reporting Issues

To report a bug:

1.  Open the project repository on GitHub.
    
2.  Create a new **Issue**.
    
3.  Use the following template.
    

Example bug report:

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

Example feature request:

```
Title: [FEATURE] Description

Problem:
Proposed solution:
Impact on architecture:

```

----------

# 3. Development Environment Setup

## 3.1 Prerequisites

Before contributing, developers must install:

-   **Python 3.10 or higher** (recommended: Python 3.12+)
    
-   **Git**
    
-   **pip**
    
-   **Poetry**
    
-   **Node.js** (required for semantic-release during release automation)
    
-   A **GitHub account**
    

Recommended IDEs:

-   VS Code
    
-   PyCharm
    

----------

## 3.2 Cloning the Repository

Clone the project repository:

```bash
git clone https://github.com/unibo-dtm-se-2324-POPCORNMETER/artifact.git
cd artifact

```

----------

## 3.3 Installing Dependencies

The project dependencies can be installed using both **pip** and **Poetry**.

Install Python dependencies:

```bash
pip install -r requirements.txt
poetry install

```

Poetry creates a virtual environment and installs the project dependencies.

Activate the Poetry environment:

```bash
poetry shell

```

----------

## 3.4 Environment Configuration

To enable external movie API integration, create the following configuration file:

```
.streamlit/secrets.toml

```

Add the required API keys:

```toml
OMDB_API_KEY = "your_omdb_key"
TMDB_API_KEY = "your_tmdb_key"

```

These keys are required for:

-   retrieving movie metadata from **OMDb**
    
-   retrieving trending movie lists from **TMDb**
    

If these keys are not configured, some features (for example trending lists or detailed metadata) may be limited.

The `.streamlit/` directory is excluded from version control via `.gitignore`.

----------

# 4. Running the Application

Once dependencies and environment variables are configured, the application can be started locally.

Run using Poetry:

```bash
poetry run popcorn-meter

```

or

```bash
poetry run python -m popcorn_meter

```

The application will start locally and be accessible at:

```
http://localhost:8501

```

----------

# 5. Running Tests

All tests must pass before creating a Pull Request.

Run the test suite:

```bash
python -m unittest discover

```

or through Poetry:

```bash
poetry run python -m unittest discover

```

The CI pipeline will automatically execute the full test suite for each commit.

Developers should run tests locally before submitting changes.

----------

# 6. Coding Standards & Conventions

## 6.1 Architecture Rules

Developers must respect the layered architecture of the system.

The following rules apply:

-   The **UI layer** must not directly access the database.
    
-   The UI interacts only with **`AppService`**.
    
-   Business logic must reside inside the **application layer**.
    
-   SQL queries must exist only inside **`SqliteRepo`**.
    
-   External API calls must exist only inside **`OmdbClient`**.
    

This separation improves maintainability and testability.

----------

## 6.2 Naming Conventions

The project follows standard Python naming conventions:

Classes  
`PascalCase`

Example

```
AppService
SqliteRepo

```

Functions and methods  
`snake_case`

Example

```
add_to_watchlist
list_watched

```

Constants  
`UPPER_CASE`

Example

```
ALL_GENRES

```

Branch naming conventions:

```
feature/<short-description>
fix/<short-description>

```

----------

## 6.3 Type Safety

All public functions must include **type hints**.

Static type checks are performed using **mypy**, which runs automatically during CI.

----------

## 6.4 Code Quality Rules

Developers must follow these guidelines:

-   Avoid commented-out legacy code.
    
-   Do not commit hardcoded credentials or API keys.
    
-   Keep SQL logic confined to the repository layer.
    
-   Write clear and descriptive commit messages.
    

----------

# 7. Development Workflow

## 7.1 Branching Strategy

The repository uses a **Git feature branch workflow**.

Main branches:

```
master     → stable release branch
develop    → integration branch
feature/*  → new features
fix/*      → bug fixes

```

----------

## 7.2 Creating a Feature Branch

Start development from the `develop` branch:

```bash
git checkout develop
git pull origin develop
git checkout -b feature/add-search-filter

```

----------

## 7.3 Committing Changes

Commit messages must follow semantic conventions:

```
feat: add advanced genre filtering
fix: correct login validation bug
refactor: simplify recommendation scoring

```

These commit prefixes allow automated tools to determine release versions.

----------

## 7.4 Pushing Changes

Push the branch to the remote repository:

```bash
git add .
git commit -m "feat: add watchlist sorting"
git push --set-upstream origin feature/add-watchlist-sorting

```

----------

## 7.5 Creating a Pull Request

To merge changes:

1.  Push the feature branch.
    
2.  Open a Pull Request targeting **`develop`**.
    
3.  Ensure CI checks pass.
    
4.  Request review from another contributor.
    
5.  Merge after approval.
    

----------

# 8. CI/CD Rules

The project uses **GitHub Actions** for automated testing and deployment.

CI pipelines enforce the following rules:

-   Pull Requests cannot be merged if CI fails.
    
-   All tests must pass before merging.
    
-   Static analysis checks must pass.
    
-   Only maintainers can merge into `master`.
    

Release versions are generated automatically using **semantic-release**.

----------

# 9. Development Tools

## 9.1 Recommended IDE Configuration

For **VS Code**, recommended extensions include:

-   Python
    
-   Pylance
    
-   GitLens
    

Recommended settings:

-   Enable **Format on Save**
    
-   Enable **Type Checking**
    
-   Select the **Poetry virtual environment interpreter**
    

----------

## 9.2 Command Line Usage

Common commands used during development:

```bash
git pull
git fetch
git checkout
poetry install
python -m unittest discover

```

Developers are expected to be comfortable working with the **Git command line interface**.

----------

# 10. Optional Package Installation (TestPyPI)

The Popcorn Meter package can also be installed from **TestPyPI** for testing releases.

Example:

```bash
pip install --index-url https://test.pypi.org/simple/ \
--extra-index-url https://pypi.org/simple \
popcorn-meter==<version>

```

This method is primarily used for validating release artifacts before publishing to the main Python Package Index.

----------

# 11. Onboarding Checklist for New Developers

A new developer joining the project should follow this checklist:

1.  Clone the repository.
    
2.  Install Python and Poetry.
    
3.  Install project dependencies.
    
4.  Configure `.streamlit/secrets.toml` with API keys.
    
5.  Run the test suite.
    
6.  Start the application locally.
    
7.  Create a feature branch for development.
    
