---
title: CI/CD
has_children: false
nav_order: 9
---

# CI/CD


**Continuous Integration (CI)** is the practice of automatically validating every change pushed to the repository. The goal is to detect problems early by running automated checks (e.g., syntax checks, static analysis, and tests) on each commit or pull request. CI reduces integration risk and ensures that the main branches remain in a working state.

**Continuous Delivery / Continuous Deployment (CD)** extends CI by automating the release process. After the code passes CI checks, the pipeline can automatically produce a release artifact (and potentially deploy it).

-   **Continuous Delivery**: releases are prepared automatically, but may require manual approval to deploy.
    
-   **Continuous Deployment**: deployment happens automatically after validation.
    

In this project, CI is used to enforce code quality and correctness on every change, and CD is used to automate releases when conditions are met.

----------

## CI/CD workflow in this project

### Overview

The project adopts a **feature-branch workflow** with automated quality gates:

-   **CI** runs on pushes and pull requests to validate code changes.
    
-   **CD** (release pipeline) runs after CI succeeds and is designed to publish releases via **semantic-release**.
    

The workflows are implemented using **GitHub Actions** in `.github/workflows/`.

----------

## Continuous Integration (CI)

### When CI runs (automation triggers)

The CI workflow (`check.yml`) runs on:

-   `push` (excluding `dependabot/**` and `renovate/**`)
    
-   `pull_request`
    
-   `workflow_dispatch` (manual run)
    

It also ignores documentation-only changes (`README.md`, `LICENSE`, etc.) to avoid wasting CI resources on changes that cannot break the software.

### What is automated and why

CI automates the following to prevent regressions and ensure consistent quality across team contributions:

1.  **Dependency installation / environment restoration**
    
    -   Ensures a clean, reproducible environment for every run.
        
    -   Implemented via `poetry install`.
        
2.  **Syntax validation (“compile” check)**
    
    -   Early detection of syntax errors and broken imports.
        
    -   Implemented via `poetry run poe compile`.
        
3.  **Static type checking**
    
    -   Catches type mismatches and interface mistakes before runtime.
        
    -   Implemented via `poetry run poe mypy`.
        
4.  **Automated test suite execution with coverage**
    
    -   Confirms functional correctness, including regressions introduced by new features.
        
    -   Measures coverage to quantify how much code is exercised by tests.
        
    -   Implemented via:
        
        -   `poetry run poe coverage`
            
        -   `poetry run poe coverage-report`
            
        -   `poetry run poe coverage-html`
            
5.  **Artifact publishing (coverage report)**
    
    -   Makes HTML coverage report available as a downloadable artifact for inspection.
        
    -   Implemented using `actions/upload-artifact` of the `htmlcov` folder.
        

### Cross-platform and multi-version compatibility

After preliminary checks succeed, the `test` job runs a **matrix** across:

-   OS: Ubuntu, Windows, macOS
    
-   Python: 3.9–3.13
    

This is important because:

-   developers may run the project on different OSes,
    
-   Python version differences can introduce subtle bugs,
    
-   the project uses external dependencies (e.g., HTTP clients) and file paths (SQLite DB location) that can behave differently across platforms.
    

----------

## Continuous Delivery (CD)

### When CD runs

The CI workflow includes a `deploy` job that is executed **only if the full test matrix succeeds**.  
The deploy logic is implemented in a reusable workflow: `.github/workflows/deploy.yml`.

### What CD automates

The deploy workflow automates:

1.  **Release orchestration**
    
    -   Fetches git history + tags
        
    -   Determines whether release should be skipped for initial commits
        
    -   Runs **semantic-release** to generate version numbers and release notes automatically
        
2.  **Build toolchain setup**
    
    -   Python env restored (Poetry)
        
    -   Node installed (used by semantic-release)
        
    -   Dependencies installed (`npm install`)
        
3.  **Controlled publishing**
    
    -   Publishing credentials are injected through GitHub Secrets.
        
    -   Release can run as a **dry run** if conditions are not met (e.g., not on `main/master`).
        

### Why semantic-release

Using semantic-release ensures:

-   consistent semantic versioning (major/minor/patch) derived from commit history,
    
-   automated changelog generation,
    
-   reduced manual release mistakes.
    

This is particularly useful in collaborative work where multiple contributors continuously add features.

----------

## Secrets and environment variables

The CD pipeline uses **GitHub Secrets** to avoid hardcoding sensitive data:

-   `PYPI_USERNAME`, `PYPI_PASSWORD` (publishing credentials)
    
-   `RELEASE_TOKEN` (used as `GITHUB_TOKEN` for release automation)
    

Secrets are injected only at runtime inside GitHub Actions, ensuring:

-   they never appear in source control,
    
-   they are not exposed in logs (unless explicitly printed, which is avoided).
    

### OMDb API key handling (project runtime)

The OMDb integration requires `OMDB_API_KEY`.  
For local development and deployment, the key must be provided securely via either:

-   Streamlit secrets (`.streamlit/secrets.toml`) for local/Streamlit Cloud usage, or
    
-   environment variables (e.g., `OMDB_API_KEY` in runtime environment).
    

This design prevents committing API keys to git while still enabling external API functionality.

----------

## Room for modifications / future enhancements

The existing CI/CD is intentionally modular and can be extended as the project evolves. Examples of planned enhancements:

1.  **Add UI-level checks**
    
    -   Include Streamlit smoke tests in CI (import + minimal execution checks).
        
2.  **Add stricter quality gates**
    
    -   Add formatting/linting (Black/Ruff) to fail PRs that violate style rules.
        
3.  **Deploy to a hosted environment**
    
    -   Integrate Streamlit Community Cloud deployment or container-based deployment (Render/Fly.io).
        
    -   Configure environment secrets (OMDb key) on the hosting platform.
        
4.  **Branch-based release policy**
    
    -   Keep current policy: real releases only on `master/main`.
        
    -   Allow preview releases on feature branches via dry-run mode.
        

These enhancements require minimal changes because the pipeline already separates concerns: checks → tests → deploy.

----------

## Where this is implemented in the repository

-   CI workflow: `.github/workflows/check.yml`
    
-   CD workflow: `.github/workflows/deploy.yml`
