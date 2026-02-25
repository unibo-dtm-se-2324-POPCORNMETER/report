# 7. Validation

## 7.1 Testing Approach

We adopted a layered testing strategy aligned with the layered architecture of the system (Presentation → Application → Infrastructure).

Testing was performed at three levels:

-   Unit testing
    
-   Integration testing
    
-   System testing
    
-   Manual acceptance testing
    

While we did not strictly follow Test-Driven Development (TDD) from the very beginning of the project, during the database and OMDb integration phases we progressively adopted a test-first approach, writing tests in parallel with new features to validate correctness and prevent regressions.

----------

## Testing Framework

We used **pytest** as our testing framework.

### Why pytest?

We selected pytest because:

-   It provides concise and readable test syntax.
    
-   It supports powerful fixtures for test setup and teardown.
    
-   It integrates easily with coverage tools.
    
-   It offers better failure reporting compared to unittest.
    
-   It is widely adopted in professional Python projects.
    

Tests are executed via:

```bash
pytest -v

```

Coverage is measured using:

```bash
pytest --cov=popcorn_meter --cov-report=term-missing

```

----------


## 7.2 Automated Testing

### 7.2.1 Unit Testing

**Scope**  

Unit tests target the **use cases** implemented in `AppService`. These tests isolate business logic from external dependencies by using mocks.

**Test rationale**  

The goal is to verify that each use case:

-   returns the correct value (success/failure)
    
-   delegates the correct calls to its collaborators (repository and OMDb client)
    
-   handles failure conditions safely (e.g., invalid login, missing user id, missing username)
    

**Test Doubles**  

We used **mocks** (`unittest.mock.Mock`) as test doubles:

-   `repo = Mock()` replaces the SQLite repository
    
-   `omdb = Mock()` replaces the OMDb client
    

This ensures unit tests are:

-   deterministic
    
-   independent from filesystem/database state
    
-   independent from external network/API calls
    

**Unit tests implemented (actual file: use_cases test)** 
 
The unit test module validates:

####  Authentication

-   `test_sign_up_delegates_to_repo_create_user`  
    Verifies sign-up delegates to repository and returns success.
    
-   `test_login_returns_none_if_verify_login_fails`  
    Verifies login fails correctly when credentials are invalid.
    
-   `test_login_returns_none_if_user_id_missing`  
    Handles repository returning no user id.
    
-   `test_login_returns_none_if_username_missing`  
    Handles missing username case.
    
-   `test_login_returns_session_user_on_success_and_strips_username`  
    Ensures correct creation of `SessionUser` and normalization (strip whitespace).
    

####  Preferences (Favorite Genres)

-   `test_set_genres_delegates_to_repo_set_favorite_genres`
    
-   `test_get_genres_returns_repo_value`
    

####  Watchlist

-   `test_add_to_watchlist_delegates_to_repo`
    
-   `test_remove_from_watchlist_delegates_to_repo`
    
-   `test_clear_watchlist_delegates_to_repo`
    
-   `test_list_watchlist_returns_repo_value`
    

####  Watched list

-   `test_add_to_watched_delegates_to_repo`
    
-   `test_clear_watched_delegates_to_repo`
    
-   `test_list_watched_returns_repo_value`
    

####  Recommendation logic

-   `test_recommend_titles_empty_when_no_favorite_genres`
    
-   `test_recommend_titles_filters_by_genre_and_excludes_watched`
    

These validate the recommendation rule:

-   recommendations depend on the favorite genres
    
-   watched titles must be excluded
    

####  OMDb integration delegation

-   `test_fetch_movie_details_delegates_to_omdb_client`  
    Confirms the application layer delegates OMDb fetching to the OMDb adapter.
    

**Success rate**  

All unit tests pass (success rate: **100%**).
    

### Coverage

Application layer coverage: ~85–95%  
Infrastructure layer coverage: ~80–90%  
Overall coverage: ~85–90%


----------

## 7.2.2 Integration Testing

**Scope**  

Integration tests validated interaction between:

1.  AppService and SqliteRepo
    
2.  AppService and OMDbClient
    

**Test rationale** 

These tests ensure that components work correctly when combined.

Examples:

-   User registration persists correctly in SQLite.
    
-   Login retrieves correct user ID.
    
-   Watchlist operations remain consistent across sessions.
    
-   OMDb data is correctly processed and returned to the UI layer.
    

Integration tests used:

-   A temporary SQLite test database
    
-   Either mocked or controlled OMDb responses
    

 **Success Rate**

-   100% passing tests.
    

 **Coverage**

Integration tests improved overall behavioral coverage to ~85–90%.

----------

## 7.2.3 System Testing (Automated)

System tests validated the system as a whole.

**Scope**

End-to-end workflow validation:

-   Application startup
    
-   Account creation
    
-   Login
    
-   Genre selection
    
-   Watchlist management
    
-   Watched list updates
    
-   Recommendation generation
    
-   OMDb integration
    

These tests validate that the application components are correctly wired and no runtime errors occur.

 **Success Rate**

-   100% passing.
    

----------

# 7.3 Continuous Integration

All tests are executed automatically via GitHub Actions CI on each push.

The pipeline:

1.  Installs dependencies
    
2.  Runs pytest
    
3.  Generates coverage reports
    
4.  Fails the build if tests fail
    

This ensures:

-   Regression prevention
    
-   Clean environment execution
    
-   Reproducibility
    

----------

# 7.4 Manual Acceptance Tests

Since formal acceptance test automation was not implemented, we designed repeatable manual acceptance tests aligned with system requirements.

----------

## AT-1: Account Creation

Steps:

1.  Navigate to Account page.
    
2.  Create new user.
    
3.  Login with credentials.
    

Expected:

-   Account created successfully.
    
-   Login succeeds.
    

Result: Passed

----------

## AT-2: Data Persistence

Steps:

1.  Add movie to watchlist.
    
2.  Restart application.
    
3.  Login again.
    

Expected:

-   Movie still present in watchlist.
    

Result: Passed

----------

## AT-3: Recommendation Logic

Steps:

1.  Set favorite genre.
    
2.  Mark one movie as watched.
    
3.  Open Recommendations.
    

Expected:

-   Movies from selected genre shown.
    
-   Watched movie excluded.
    

Result: Passed

----------

## AT-4: OMDb Integration

Steps:

1.  Enter movie title.
    
2.  Fetch OMDb details.
    

Expected:

-   Title, year, plot, and poster displayed.
    
-   No crash occurs.
    

Result: Passed

----------

### Acceptance Testing Success Rate

All defined manual acceptance tests passed successfully.
