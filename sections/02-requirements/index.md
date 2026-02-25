# 1. Requirements

## 1.1 User Stories (Personas)

### Persona 1 — Guest User

A visitor who has not logged in yet and wants to explore the application.

#### User Stories

- As a guest, I want to search for a movie by title so that I can view its details.
- As a guest, I want to see trending movies so that I can explore content.
- As a guest, I want to create an account so that I can personalize my experience.
- As a guest, I want to log in so that I can access my saved data.

---

### Persona 2 — Registered User

A logged-in user who wants personalized recommendations and persistent watchlists.

#### User Stories

- As a registered user, I want to set my favorite genres so that I receive relevant recommendations.
- As a registered user, I want to add movies to my watchlist so that I can remember what to watch.
- As a registered user, I want to remove movies from my watchlist.
- As a registered user, I want to mark movies as watched.
- As a registered user, I want to view my watch history.
- As a registered user, I want to receive movie recommendations based on my profile.
- As a registered user, I want to log out securely.

---

## 1.2 Requirements Analysis

This section describes what the system must do, independently from technical implementation.

---

# 2. Functional Requirements (FR)

## FR1 — User Registration

The system shall allow a new user to create an account by providing:
- Username
- Email
- Password

### Acceptance Criteria

- A new account is created if the email does not already exist.
- The system rejects registration if required fields are empty.
- The system prevents duplicate email registration.

---

## FR2 — User Login

The system shall allow registered users to log in using their email and password.

### Acceptance Criteria

- The system grants access if credentials are valid.
- The system denies access if credentials are invalid.
- After login, the user session is maintained.

---

## FR3 — User Logout

The system shall allow authenticated users to log out.

### Acceptance Criteria

- After logout, user-specific data is no longer accessible.
- Session state is cleared.

---

## FR4 — Search Movie by Title

The system shall allow users to search for a movie by entering its title.

### Acceptance Criteria

- The system retrieves movie details if the title exists.
- The system shows an error message if the movie is not found.
- The system displays selected movie attributes:
  - Title
  - Year
  - Genre
  - Plot
  - Poster

---

## FR5 — View Movie Details

The system shall display detailed information about a selected movie.

### Acceptance Criteria

The system displays:

- Title  
- Release year  
- Genre  
- Plot  
- Runtime  
- Rating  
- Poster (if available)

The system handles missing information gracefully.

---

## FR6 — Manage Favorite Genres

The system shall allow authenticated users to select and store preferred genres.

### Acceptance Criteria

- Selected genres are saved.
- Saved genres can be retrieved and displayed.
- Genre selection can be modified.

---

## FR7 — Manage Watchlist

The system shall allow authenticated users to:

- Add a movie to their watchlist.
- Remove a movie from their watchlist.
- View their watchlist.

### Acceptance Criteria

- A movie can be added only once.
- The watchlist persists between sessions.
- The watchlist is displayed in a structured format.

---

## FR8 — Manage Watched Movies

The system shall allow authenticated users to:

- Mark movies as watched.
- View watched movies.
- Clear watched list.

### Acceptance Criteria

- Watched movies are stored persistently.
- The list can be cleared completely.

---

## FR9 — Generate Recommendations

The system shall provide personalized movie recommendations based on:

- The user’s selected genres
- Watch history

### Acceptance Criteria

- Recommendations reflect selected genres.
- Already watched movies are excluded.
- If no genres are selected, no recommendations are shown.

---

## FR10 — Navigation

The system shall provide structured navigation allowing access to:

- Home
- Account
- Favorite Genres
- Watchlist
- Watched
- Recommendations

### Acceptance Criteria

- Navigation options are visible.
- Selecting a section loads the corresponding view.

---

### Use-case diagram

<img width="422" height="870" alt="image" src="https://github.com/user-attachments/assets/a6c36682-82f1-482d-801a-cc592bde7ab5" />

Figure 1 illustrates the use-case diagram of the Popcorn Meter system. It summarizes the functional scope and the interaction between user roles and system capabilities. Each use case corresponds to a numbered functional requirement (FR1–FR10).

---

# 3. Non-Functional Requirements (NFR)

## NFR1 — Usability

The system shall provide a clean and intuitive user interface.

### Acceptance

- Navigation is clearly visible.
- Buttons and actions are labeled.
- Feedback messages are displayed for user actions.

---

## NFR2 — Data Persistence

User data shall persist across sessions.

### Acceptance

- Watchlist, watched movies, and genres remain saved after restarting the application.

---

## NFR3 — Availability

The system shall remain usable without crashing under normal user interactions.

### Acceptance

- Invalid inputs are handled gracefully.
- System errors are displayed clearly.

---

## NFR4 — Security (Basic)

The system shall restrict watchlist and personalization features to authenticated users only.

### Acceptance

- Guests cannot save watchlists.
- Unauthorized access to user data is prevented.

---

## NFR5 — External API Robustness

The system shall handle external movie API failures gracefully.

### Acceptance

- If the API key is missing, an error is displayed.
- If the external service fails, the system remains operational.

---

# 4. Implementation Requirements (IR)

## IR1 — Programming Language

The system shall be implemented using **Python**.

**Justification:**
- Academic standardization.
- Ease of rapid development.

---

## IR2 — Web Framework

The system shall use **Streamlit** for the user interface.

**Justification:**
- Rapid prototyping requirement.
- Lightweight deployment.
- Suitable for academic scope.

---

## IR3 — Database

The system shall use **SQLite** as persistent storage.

**Justification:**
- No external server required.
- Simplicity for academic deployment.

---

## IR4 — External Movie Data

The system shall use the **OMDb API** for retrieving movie information.

**Justification:**
- Publicly accessible movie metadata source.
- Free API tier suitable for project scope.

OMDb Website:  
https://www.omdbapi.com/

---



---

## 5. Glossary

| Term | Definition |
|------|------------|
| Watchlist | List of movies a user intends to watch |
| Watched | List of movies already seen |
| Genre | Category of a movie (e.g., Action, Drama) |
| Recommendation | Suggested movie based on user preferences |
| Session | Active authenticated state of a user |


