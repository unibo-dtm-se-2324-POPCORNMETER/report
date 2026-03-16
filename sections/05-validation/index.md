---
title: Validation
has_children: false
nav_order: 5
---


#  Validation

## Testing Approach

The project adopts a **layered testing strategy**, consistent with the architectural layers of the system:

-   Presentation layer (Streamlit UI)
    
-   Application layer (use cases)
    
-   Infrastructure layer (database and external API adapters)
    

Testing was performed at four levels:

-   **Unit testing**
    
-   **Integration testing**
    
-   **System testing**
    
-   **Manual acceptance testing**
    

This structure ensures that individual components are validated independently before verifying the behavior of combined components and the system as a whole.

Although strict **Test-Driven Development (TDD)** was not applied from the beginning of the project, testing was progressively integrated into development. As the database and OMDb integration were implemented, tests were written alongside new functionality to verify correctness and avoid regressions.

----------

# Testing Framework

The automated tests are executed with **pytest**, while several test modules are written using Python’s built-in **`unittest` framework**.

### Why `unittest`?

The choice of `unittest` was motivated by several factors:

-   It is included in the **Python standard library**, requiring no external dependencies.
    
-   It provides **structured test cases and assertions** suitable for unit and integration testing.
    
-   It integrates well with **mocking tools (`unittest.mock`)**.
    
-   It is compatible with CI pipelines and coverage tools.
    

Tests can be executed using:

```bash
python -m unittest discover

```

In the CI pipeline, additional scripts generate **coverage reports** using the coverage tools integrated in the repository workflow.

----------

#  Automated Testing

##  Unit Testing

### Scope

Unit tests target the **application layer**, implemented in the `AppService` class, and also include a separate unit test module for `OmdbClient`.

These tests isolate business logic from external dependencies by replacing collaborators with **mock objects**.

Dependencies mocked in the tests include:

-   the repository (`RepoPort`)
    
-   the OMDb movie information provider (`MovieInfoPort`)
    

This allows the tests to validate only the **logic of the use cases**, without interacting with the database or external APIs.

----------

### Test Doubles

The unit tests use **mock objects (`unittest.mock.Mock`)** as test doubles.

Examples:

```python
repo = Mock()
omdb = Mock()
svc = AppService(repo=repo, omdb=omdb)

```

Mocks allow tests to:

-   simulate repository responses
    
-   simulate OMDb API responses
    
-   verify that the correct methods are invoked
    

This makes unit tests:

-   deterministic
    
-   independent from filesystem/database state
    
-   independent from network calls
    

----------

### Unit tests implemented

The unit tests verify most main use cases implemented in `AppService`.

#### Authentication

-   **test_sign_up_delegates_to_repo_create_user**  
    Confirms that the sign-up operation delegates to the repository and returns the expected result.
    
-   **test_login_returns_none_if_verify_login_fails**  
    Verifies that login fails when credentials are invalid.
    
-   **test_login_returns_none_if_user_id_missing**  
    Ensures the service handles a missing user identifier safely.
    
-   **test_login_returns_none_if_username_missing**  
    Ensures the service handles incomplete user data.
    
-   **test_login_returns_session_user_on_success_and_strips_username**  
    Confirms correct creation of the `SessionUser` object and normalization of the username.
    

These tests correspond to the following requirements:

-   **FR1 – User Registration**
    
-   **FR2 – User Login**
    

----------

#### Favorite genres

-   **test_set_genres_delegates_to_repo_set_favorite_genres**
    
-   **test_get_genres_returns_repo_value**
    

These tests verify that genre preferences are stored and retrieved correctly.

Related requirement:

-   **FR6 – Manage Favorite Genres**
    

----------

#### Watchlist

-   **test_add_to_watchlist_delegates_to_repo**
    
-   **test_remove_from_watchlist_delegates_to_repo**
    
-   **test_clear_watchlist_delegates_to_repo**
    
-   **test_list_watchlist_returns_repo_value**
    

These tests ensure that watchlist operations correctly delegate to the persistence layer.

Related requirement:

-   **FR7 – Manage Watchlist**
    

----------

#### Watched list

-   **test_add_to_watched_delegates_to_repo**
    
-   **test_clear_watched_delegates_to_repo**
    
-   **test_list_watched_returns_repo_value**
    

These tests verify examples of correct handling of watched movies.

Related requirement:

-   **FR8 – Manage Watched Movies**
    

----------

#### Recommendation logic

-   **test_recommend_titles_empty_when_no_favorite_genres**
    
-   **test_recommend_titles_filters_by_genre_and_excludes_watched**
    
-   **test_recommend_titles_uses_omdb_scoring_and_feedback**
    

These tests validate core recommendation rules:

-   recommendations depend on favorite genres
    
-   already watched movies must be excluded
    
-   OMDb-based scoring and persisted feedback can affect ranking
    

Related requirement:

-   **FR9 – Generate Recommendations**
    

----------

#### OMDb delegation

-   **test_fetch_movie_details_delegates_to_omdb_client**
    

This test ensures that the application layer delegates movie metadata retrieval to the OMDb adapter.

A separate unit test module also validates the behavior of `OmdbClient` directly.

Related requirements:

-   **FR4 – Search Movie by Title**
    
-   **FR5 – View Movie Details**
    

----------

### Success Rate

The repository includes unit tests for the implemented components.

----------

### Coverage

Unit tests provide strong coverage of the application layer.

Coverage reports are generated in the CI pipeline.

-   Exact percentages are not stated here.
    

----------

#  Integration Testing

### Scope

Integration tests validate the interaction between the **repository implementation (`SqliteRepo`)** and the underlying **SQLite database**.

These tests operate on a **real SQLite database**, created temporarily during test execution.

The tests use:

```python
tempfile.TemporaryDirectory()

```

to create an isolated database file for each test.

In addition, the project also contains a lightweight UI smoke test at system level.

----------

### Integration tests implemented

The repository integration tests validate the following behaviors.

#### User management

-   **test_create_user_and_login_success**  
    Verifies that a user can be created and authenticated.
    
-   **test_password_is_stored_hashed**  
    Ensures that passwords are not stored in plain text and are hashed using `pbkdf2_sha256`.
    
-   **test_verify_login_fails_for_wrong_password**  
    Verifies that incorrect credentials are rejected.
    
-   **test_verify_login_migrates_legacy_plaintext_password**  
    Ensures that legacy plain-text passwords are automatically migrated to hashed storage.
    
-   **test_create_user_duplicate_email_fails**  
    Verifies that duplicate email addresses are rejected.
    
-   **test_get_user_id_and_username**  
    Confirms correct retrieval of user identifiers.
    

These tests validate:

-   **FR1 – User Registration**
    
-   **FR2 – User Login**
    
-   **NFR4 – Basic Security**
    

----------

#### Genre persistence

-   **test_set_and_get_favorite_genres**
    

Validates correct storage and retrieval of user genre preferences.

Requirement:

-   **FR6 – Manage Favorite Genres**
    

----------

#### Watchlist persistence

-   **test_watchlist_add_and_list**
    
-   **test_watchlist_duplicate_fails**
    

These tests confirm correct watchlist behavior and duplicate protection.

Requirement:

-   **FR7 – Manage Watchlist**
    

----------

#### Watched list persistence

-   **test_watched_add_and_list**
    

Confirms correct persistence of watched movies.

Requirement:

-   **FR8 – Manage Watched Movies**
    

----------

#### Feedback persistence

-   **test_feedback_save_and_read**
    
-   **test_feedback_partial_update_keeps_existing_values**
    

These tests verify the feedback system and confirm that partial updates preserve previous values.

Requirement:

-   **FR9 – Recommendation Feedback**
    

----------

### Success Rate

The repository includes integration tests covering the implemented persistence behavior.

----------

#  System Testing (Automated)

A lightweight **system smoke test** validates that the entire application can be initialized successfully.

The test imports the Streamlit UI module while mocking external dependencies.

The test:

-   injects a temporary OMDb API key
    
-   mocks the OMDb API response
    
-   imports the Streamlit application module
    

Example behavior tested:

```python
importlib.import_module("popcorn_meter.ui.streamlit_app")

```

This ensures that:

-   the UI module loads correctly
    
-   dependencies are correctly wired
    
-   no runtime errors occur during application startup
    

Related requirements:

-   **FR10 – Navigation**
    
-   **NFR1 – Usability**
    
-   **NFR3 – Availability**
    
-   **NFR5 – External API Robustness**
    

----------

### Success Rate

The repository includes a lightweight system smoke test for application startup.

----------

#  Continuous Integration

All tests are executed automatically through **GitHub Actions** on each repository push.

The CI pipeline performs the following steps:

1.  Install project dependencies.
    
2.  Restore the Python development environment.
    
3.  Run static checks.
    
4.  Execute all tests.
    
5.  Generate coverage reports.
    

This process ensures:

-   regression prevention
    
-   reproducible builds
    
-   validation in a clean environment
    
-   early detection of integration errors
    

----------

#  Manual Acceptance Tests

In addition to automated testing, manual acceptance tests were performed to validate user-visible functionality.

The following tests correspond to the functional requirements of the system.

----------

## AT-1 — Account Creation

Steps:

1.  Navigate to the **Account** page.
    
2.  Register a new user.
    
3.  Log in with the created credentials.
    

Expected result:

-   Account creation succeeds.
    
-   Login is successful.
    

Result: **Passed**

Related requirements:

-   **FR1**
    
-   **FR2**
    

----------

## AT-2 — Data Persistence

Steps:

1.  Add a movie to the watchlist.
    
2.  Restart the application.
    
3.  Log in again.
    

Expected result:

-   The movie remains in the watchlist.
    

Result: **Passed**

Related requirement:

-   **NFR2 – Data Persistence**
    

----------

## AT-3 — Recommendation Logic

Steps:

1.  Select a favorite genre.
    
2.  Mark one movie as watched.
    
3.  Open the Recommendations page.
    

Expected result:

-   Movies from the selected genre are recommended.
    
-   Watched movies are excluded.
    

Result: **Passed**

Related requirement:

-   **FR9 – Generate Recommendations**
    

----------

## AT-4 — OMDb Integration

Steps:

1.  Enter a movie title.
    
2.  Fetch movie details.
    

Expected result:

-   Title, year, plot, and poster are displayed.
    
-   No application crash occurs.
    

Result: **Passed**

Related requirements:

-   **FR4 - Search Movie by Title**
    
-   **FR5 - View Movie Details**
    

----------

# Acceptance Testing Success Rate

All defined manual acceptance tests passed successfully.


