


# Development

## Distributed Version Control System (DVCS)

The project uses **Git** as the distributed version control system and **GitHub** as the hosting platform for collaboration and code management.

### Branching Strategy

Development follows a **multi-branch workflow** separating stable releases from ongoing development and experimental features.

Main branches:

-   **master** – stable production-ready code
    
-   **develop** – integration branch for features before release
    

Feature development occurs in **dedicated feature branches**, such as:

-   `feature/auth-email`
    
-   `feature/database`
    
-   `feature/streamlit-ui`
    
-   `feature/omdb-integration`
    
-   `feature/omdb-improvements`
    
-   `feature/integration-final`
    

Each feature branch contains the implementation of a specific functionality and is later merged into `develop`, which is then merged into `master` during releases.

This structure allows multiple contributors to work simultaneously without interfering with the stable version of the application.

The commit history shows that releases are produced through merges from `develop` into `master`, followed by automated release commits (e.g., `chore(release): 1.1.2`). This ensures traceable versioning and stable release points.

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

1.  Developer creates a feature branch from `develop`.
    
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

The OMDb movie database is accessed through a REST API using HTTP requests. The client is implemented in Python using the `requests` library.

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
    

Authentication logic is handled in the application service layer.

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
    

The project supports Python versions between **3.9 and 4.0**.

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

-   **pytest / unittest** – automated testing
    
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

The API key is provided through an environment variable:

```
OMDB_API_KEY

```

to avoid exposing secrets in the repository.

----------

## Release and Automation Tools

The project uses **semantic-release** to automate software releases.

Release automation:

-   determines the next version based on commit messages
    
-   updates the changelog
    
-   publishes packages
    
-   creates GitHub releases.
    

This automation integrates with GitHub Actions in the CI/CD pipeline.

