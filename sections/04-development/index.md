---
title: Developement
has_children: false
nav_order: 4
---


# Development

## Distributed Version Control System (DVCS)

The project uses **Git** as the distributed version control system and **GitHub** as the hosting platform for collaboration and code management.

### Branching Strategy

The repository uses multiple branches for development, but releases are automated from the main release branch (`master`, with `main` also supported in workflow configuration).

Main branches:

-   The repository contains both **master** and **develop** branches
    
-   release automation is configured for **master/main**, not for **develop**
    

Feature development occurs in **dedicated feature branches**, such as:

-   `feature/auth-email`
    
-   `feature/database`
    
-   `feature/streamlit-ui`
    
-   `feature/omdb-integration`
    
-   `feature/omdb-improvements`
    
-   `feature/integration-final`
    

Feature branches are used for isolated development work and are later integrated through pull requests.

This structure allows multiple contributors to work simultaneously without interfering with the stable version of the application.

The commit history shows automated release commits such as `chore(release): 2.4.7`, but it does not support claiming that every release is produced specifically through merges from `develop` into `master`. This ensures traceable versioning and stable release points.

----------

### Commit Message Conventions

The project follows **Conventional Commit standards**, which structure commit messages in the form:

```
type(scope): description

```

Examples from the repository include:

```
feat: align template setup, CI checks, and auth hardening
fix(ci): correct setup-node step in deploy workflow
chore(release): 1.1.2

```

Common commit types include:

-   **feat** – new feature implementation
    
-   **fix** – bug fixes
    
-   **chore** – maintenance tasks (e.g., releases)
    
-   **ci** – continuous integration adjustments
    

These conventions allow automated tooling to determine semantic version changes.

The release automation system uses **semantic-release**, which reads commit messages to determine version increments.

----------

### Pull Requests and Code Review

Changes are integrated into the main development branches through **pull requests**.

Typical workflow:

1.  Developer works on a feature branch.
    
2.  Changes are committed following the conventional commit format.
    
3.  A pull request is opened.
    
4.  GitHub Actions automatically runs checks and tests.
    
5.  After validation, the branch is merged.
    

This workflow ensures that:

-   code quality checks run automatically
    
-   tests pass before integration
    
-   releases are consistent and traceable.
    

----------

# Implementation Details

## Network Protocols

The system communicates with external services using the **HTTP protocol over TCP**.

The OMDb API is accessed through HTTP requests. The client is implemented in Python using the `requests` library.

Example interaction:

-   Client sends HTTP GET request
    
-   API returns structured movie information
    

HTTP was chosen because:

-   OMDb provides a REST interface
    
-   HTTP is the standard protocol for web APIs
    
-   it integrates easily with Python libraries.
    

----------

## Data Representation

Data exchanged with the OMDb API is represented in **JSON format**.

The response is parsed using:

```python
return r.json()

```

in the OMDb client implementation.

JSON was selected because:

-   it is the default format for REST APIs
    
-   it is lightweight and human readable
    
-   it integrates naturally with Python dictionaries.
    

----------

## Database Querying

The system uses a **relational database (SQLite)** for persistent storage.

Database access is implemented through the `SqliteRepo` repository class.

The database stores the following entities:

-   users
    
-   favorite genres
    
-   watchlist
    
-   watched history
    

Data is queried using **SQL statements**, such as:

```sql
SELECT password FROM users WHERE email = ?

```

SQLite was selected because:

-   it requires no external server
    
-   it is lightweight
    
-   it is suitable for small applications and prototypes.
    

----------

## Authentication

User authentication is implemented using **email and password verification**.

When a user logs in:

1.  The email and password are submitted from the UI.
    
2.  The application service validates the credentials.
    
3.  The repository queries the database to check if they match.
    

Authentication is coordinated by the application service layer, while credential verification and password hashing are implemented in the `SqliteRepo` infrastructure component.

Example:

```python
ok = self.repo.verify_login(email, password)

```

If successful, the user is represented by a `SessionUser` object stored in the application session.

----------

## Authorization

Authorization is implemented through **simple session-based access control**.

Certain operations require a logged-in user, such as:

-   saving favorite genres
    
-   managing watchlists
    
-   adding watched movies
    
-   generating recommendations.
    

The user session is stored in Streamlit’s session state:

```python
st.session_state.session_user

```

and checked before executing user-specific actions.

This ensures that only authenticated users can modify personal data.

----------

# Technological Details

## Programming Language

The entire application is implemented in **Python**.

Python was chosen because:

-   it supports rapid development
    
-   it has strong ecosystem support for data processing
    
-   it integrates well with web APIs and lightweight databases.
    

The project supports Python versions **>=3.10 and <4.0.0**.

----------

## Frameworks and Libraries

The following main libraries are used:

### Streamlit

Streamlit is used to build the **graphical user interface** of the application.

It enables:

-   interactive UI components
    
-   session management
    
-   fast prototyping of web interfaces.
    

----------

### Requests

The **requests** library is used to communicate with the OMDb API via HTTP requests.

----------

### SQLite

SQLite is used as the embedded relational database for storing persistent data such as:

-   user accounts
    
-   preferences
    
-   watchlists
    
-   watched movies.
    

----------

### Poetry

Dependency management and packaging are handled using **Poetry**.

Poetry manages:

-   dependencies
    
-   development tools
    
-   build configuration.
    

----------

### Testing Tools

The project includes testing and static analysis tools such as:

-   **pytest** for test execution, with some test modules written using **unittest.TestCase**
    
-   **coverage** – test coverage measurement
    
-   **mypy** – static type checking.
    

----------

## External Services

The application integrates with the **OMDb API (Open Movie Database)** to retrieve movie metadata such as:

-   title
    
-   year
    
-   genre
    
-   plot
    
-   poster images.
    

This functionality is implemented in the `OmdbClient` infrastructure component.

The OMDb API key can be provided through an environment variable or through Streamlit secrets:

```
OMDB_API_KEY

```

to avoid exposing secrets in the repository.

----------

## Release and Automation Tools

The project uses **semantic-release** to automate software releases.

Release automation:

-   determines the next version based on commit messages
    
-   updates project versioning metadata
    
-   updates the changelog
    
-   publishes packages
    
-   creates GitHub releases when not running in dry-run mode.
    

This automation integrates with GitHub Actions in the CI/CD pipeline.
