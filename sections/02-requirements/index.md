---
title: Requirements
has_children: false
nav_order: 2
---

#  Requirements

## User Stories (Personas)

### Persona 1 — Guest User

A visitor who has not logged in yet and wants to explore the application.

**User Stories**

-   As a guest, I want to search for a movie by title so that I can view its details.
    
-   As a guest, I want to see trending movies so that I can explore content.
    
-   As a guest, I want to create an account so that I can personalize my experience.
    
-   As a guest, I want to log in so that I can access my saved data.
    

----------

### Persona 2 — Registered User

A logged-in user who wants personalized recommendations and persistent movie lists.

**User Stories**

-   As a registered user, I want to set my favorite genres so that I receive relevant recommendations.
    
-   As a registered user, I want to add movies to my watchlist so that I can remember what to watch.
    
-   As a registered user, I want to remove movies from my watchlist.
    
-   As a registered user, I want to mark movies as watched.
    
-   As a registered user, I want to remove movies from my watched list.
    
-   As a registered user, I want to view my watch history.
    
-   As a registered user, I want to provide feedback or ratings for movies so that recommendations improve.
    
-   As a registered user, I want to receive movie recommendations based on my profile and activity.
    
-   As a registered user, I want to log out securely.
    

----------

#  Requirements Analysis

This section describes **what the system must do**, independently from how it is implemented.

Requirements are divided into:

-   Functional Requirements (FR)
    
-   Non-Functional Requirements (NFR)
    
-   Implementation Requirements (IR)
    

----------

#  Functional Requirements (FR)

## FR1 — User Registration

The system shall allow a new user to create an account by providing:

-   Username
    
-   Email
    
-   Password
    

**Acceptance Criteria**

-   A new account is created if the email does not already exist.
    
-   The system rejects registration if required fields are empty.
    
-   Duplicate email registrations are not allowed.
    

----------

## FR2 — User Login

The system shall allow registered users to log in using their email and password.

**Acceptance Criteria**

-   The system grants access if credentials are valid.
    
-   The system denies access if credentials are invalid.
    
-   After login, a user session is established.
    

----------

## FR3 — User Logout

The system shall allow authenticated users to log out of the application.

**Acceptance Criteria**

-   After logout, user-specific data is no longer accessible.
    
-   The user session is cleared.
    

----------

## FR4 — Search Movie by Title

The system shall allow users to search for a movie by entering its title.

**Acceptance Criteria**

-   The system retrieves movie details if the title exists.
    
-   The system shows an error message if the movie is not found.
    
-   The system displays movie attributes including:
    
    -   Title
        
    -   Year
        
    -   Genre
        
    -   Plot
        
    -   Poster
        

----------

## FR5 — View Movie Details

The system shall display detailed information about a selected movie.

**Acceptance Criteria**

The system displays available attributes such as:

-   Title
    
-   Release year
    
-   Genre
    
-   Plot
    
-   Runtime
    
-   IMDb rating
    
-   Poster (if available)
    

Missing information is handled gracefully.

----------

## FR6 — Manage Favorite Genres

The system shall allow authenticated users to select and store preferred genres.

**Acceptance Criteria**

-   Selected genres are saved.
    
-   Saved genres can be retrieved and displayed.
    
-   Genre preferences can be modified.
    

----------

## FR7 — Manage Watchlist

The system shall allow authenticated users to:

-   Add a movie to their watchlist.
    
-   Remove a movie from their watchlist.
    
-   Clear the watchlist.
    
-   View the watchlist.
    

**Acceptance Criteria**

-   A movie can be added only once.
    
-   The watchlist persists between sessions.
    
-   The watchlist is displayed in a structured format.
    

----------

## FR8 — Manage Watched Movies

The system shall allow authenticated users to:

-   Mark movies as watched.
    
-   Remove movies from the watched list.
    
-   View watched movies.
    
-   Clear the watched list.
    

**Acceptance Criteria**

-   Watched movies are stored persistently.
    
-   Individual watched movies can be removed.
    
-   The list can be cleared completely.
    

----------

## FR9 — Provide Movie Feedback

The system shall allow users to provide optional feedback on movies.

Feedback may include:

-   like/dislike preference
    
-   numeric rating
    

**Acceptance Criteria**

-   Users can store feedback associated with a movie.
    
-   Stored feedback can be retrieved.
    
-   Feedback may influence recommendation ranking.
    

----------

## FR10 — Generate Recommendations

The system shall generate personalized movie recommendations for authenticated users.

Recommendations are computed using a hybrid scoring strategy based on:

-   overlap between favorite genres and movie genres
    
-   actors appearing in previously watched movies
    
-   IMDb movie ratings
    
-   keyword matches between movie plots and user preferences
    
-   optional user feedback and ratings
    
-   movies in the watchlist
    

Already watched movies are excluded from recommendations.

**Acceptance Criteria**

-   Recommendations prioritize movies matching user favorite genres.
    
-   Movies already watched are excluded.
    
-   Recommendation ranking may incorporate user feedback and ratings.
    
-   If no genres are selected, no recommendations are generated.
    
-   If external movie data is unavailable, the system falls back to a predefined demo catalog.
    

----------

## FR11 — Navigation

The system shall provide structured navigation allowing access to the following sections:

-   Home
    
-   Account
    
-   Favorite Genres
    
-   Watchlist
    
-   Watched
    
-   Recommendations
    

**Acceptance Criteria**

-   Navigation options are visible.
    
-   Selecting a section loads the corresponding view.
    

----------

# Use-case Diagram

Figure 1 illustrates the use-case diagram of the Popcorn Meter system.  
It summarizes the functional scope and interactions between user roles and system capabilities.  
Each use case corresponds to one of the functional requirements (FR1–FR11).

![PlantUML Diagram](https://uml.planttext.com/plantuml/png/TPFRJiCm38RlynHMxoUnytQ3Dd6Oa1YWJOnhApDjf3IP4dUSnBkJTYsaK7gLJ_vj_tRIXMTqNEHQQ7fcO0jEfHd3NZcIhAmH0YLR1wk2FDVdP4EfyaoEzl3eoIM0lZe8KMQXIJL1yc0FqZe3QmfAsBw5X3o13o408jMou8mCAubbjp8EuIiyIVJqqmcMKjh2yAdLHR-jkhKft9WwDlWRko-Qn648VfOMlkDtU5GfCi7sDB2lbQDVHjVsg0YkNW_QkcwlMq8dCwY4TP5nMx5Jz7AAmoKnAjqqcpIsulsHyzQWLk_TxTPeC2MungDrAlXVaN7K59nsQf-GPQR3GclLx7zLkDhAQ5DmtZ79XgJDSp9xZ1VNFwk62UDKRmPwlVFgnc8Qj6ZKed6B9aAKBwkcOGoZ6COnJ6AOnZ2BOHv3i2qMOPRmBtm1)

----------

#  Non-Functional Requirements (NFR)

## NFR1 — Usability

The system shall provide a clean and intuitive user interface.

**Acceptance**

-   Navigation is clearly visible.
    
-   Buttons and actions are labeled.
    
-   Feedback messages are displayed for user actions.
    

----------

## NFR2 — Data Persistence

User data shall persist across sessions.

**Acceptance**

-   Watchlist, watched movies, favorite genres, and feedback remain saved after restarting the application.
    

----------

## NFR3 — Availability

The system shall remain operational under normal usage conditions.

**Acceptance**

-   Invalid inputs are handled gracefully.
    
-   Clear error messages are displayed.
    

----------

## NFR4 — Security (Basic)

The system shall restrict personalization features to authenticated users.

**Acceptance**

-   Guests cannot store watchlists or watched movies.
    
-   Guests cannot modify user preferences.
    

----------

## NFR5 — External API Robustness

The system relies on an external movie database API for movie information.

**Acceptance**

-   If the API key is missing, an informative error message is displayed.
    
-   If the external service fails, the system continues operating.
    
-   Recommendation generation falls back to a predefined demo catalog when external data is unavailable.
    

----------

#  Implementation Requirements (IR)

## IR1 — Programming Language

The system shall be implemented using **Python**.

**Justification**

-   widely used in academic environments
    
-   supports rapid prototyping
    

----------

## IR2 — Web Framework

The system shall use **Streamlit** for the user interface.

**Justification**

-   enables rapid UI development
    
-   simplifies deployment for small web applications
    

----------

## IR3 — Database

The system shall use **SQLite** as persistent storage.

**Justification**

-   lightweight database
    
-   does not require a separate server
    
-   suitable for academic projects
    

----------

## IR4 — External Movie Data

The system shall retrieve movie information using the **OMDb API**.

**Justification**

-   publicly accessible movie metadata
    
-   suitable free API tier
    

OMDb Website  
[https://www.omdbapi.com/](https://www.omdbapi.com/)

### OMDb API — External Service Reference

| Field | Value |
|---|---|
| Service | OMDb API (Open Movie Database) |
| Base URL | `http://www.omdbapi.com/` |
| Protocol | HTTP GET |
| Authentication | API key via `apikey` query parameter |
| Key Parameters | `t` (title), `apikey`, `plot=full` |
| Response Format | JSON |
| Fields Used | Title, Year, Genre, Plot, Poster, imdbRating, Actors, Runtime |
| Error Handling | `Response=False` → fallback to demo catalog |
| Documentation | [https://www.omdbapi.com/](https://www.omdbapi.com/) |

----------

#  Glossary

|Term  |Definition  |
|--|--|
|Watchlist  |List of movies a user intends to watch  |
|Watched  |List of movies already seen  |
|Genre |Category of a movie (e.g., Action, Drama)  |
|Recommendation |Suggested movie based on user preferences and behavior  |
|Session |Active authenticated state of a user  |
