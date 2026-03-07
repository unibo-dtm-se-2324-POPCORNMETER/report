# 3. Design

This chapter explains the architectural and modelling strategies adopted to satisfy the requirements identified in the previous section.

The design is described independently from specific technological implementation choices whenever possible.

---

## 3.1 Architecture

### 3.1.1 Architectural Style

The system adopts a **layered architectural style**.

### Why Layered?

The application clearly separates:

- **Presentation logic** (UI)
- **Application logic** (use cases)
- **Infrastructure logic** (database + external API)

This supports:

- Separation of concerns  
- Maintainability  
- Testability (unit tests per layer)  
- Clear dependency direction  

---

### Why Not Other Styles?

- **Event-based architecture**  
  Unnecessary complexity for a non-asynchronous system.

- **Shared dataspace**  
  Not applicable, as there are no multiple distributed writers/readers.

- **Microservices / Distributed architecture**  
  Out of scope for academic size and requirements.

- **Hexagonal (Ports & Adapters)**  
  Conceptually similar, but a simplified layered structure was sufficient.

---

## 3.1.2 Adopted Architecture

The system follows a **3-layer architecture**:


Presentation Layer → Application Layer → Infrastructure Layer


---

### Layer Responsibilities

---

### 1️ Presentation Layer (UI)

**Implemented using Streamlit**

Responsible for:

- Handling user input
- Managing navigation
- Rendering views
- Displaying feedback messages

Constraints:

- Does **not** access the database directly
- Communicates only with the Application Layer

---

### 2️ Application Layer

Contains:

- `AppService`

Responsible for implementing business rules:

- Authentication flow
- Recommendation logic
- Watchlist management
- Genre filtering

Responsibilities:

- Coordinates repositories and external services
- Contains core business logic
- Acts as mediator between UI and infrastructure

---

### 3️ Infrastructure Layer

Contains:

- `SqliteRepo` (database persistence)
- `OmdbClient` (external API integration)

Responsible for:

- Data storage
- Data retrieval
- API communication
- Low-level technical concerns

---

### 3.1.3 High-Level Architecture Diagram

<img width="345" height="407" alt="image" src="https://github.com/user-attachments/assets/26095056-23b0-4386-a537-37517cc00934" />


---
## 3.2 Infrastructure

Although not a distributed system, the application includes infrastructural components.

### Components

- Client browser (user interface)
- Streamlit runtime (server)
- SQLite database file
- External OMDb API

---

### Deployment Topology

All internal components (UI, AppService, SQLite) run on the same machine.

**External dependency:**

- OMDb API accessed over HTTP

There are:

- No load balancers
- No distributed servers
- No message brokers
- No caching layer

This matches the academic scope and simplicity requirements.

---

### Deployment Diagram

<img width="547" height="567" alt="image" src="https://github.com/user-attachments/assets/603ffd22-3d87-4fb1-a473-f65cc4d67716" />

---

## 3.3 Modelling

### 3.3.1 Domain-Driven Design (DDD)

The system design follows Domain-Driven Design (DDD) principles to clearly separate business concerns and define explicit domain boundaries.

---

### Bounded Contexts

The domain is divided into the following bounded contexts:

#### 1️. Authentication Context

Responsible for user identity and access control.

- User
- Session

---

#### 2️. Movie Management Context

Responsible for user-related movie data.

- Watchlist
- Watched
- Genre preferences

---

#### 3️. Recommendation Context

Responsible for personalization logic.

- Recommendation logic
- Filtering rules

---

#### 4️. External Movie Data Context

Responsible for integration with the external movie data provider.

- Movie metadata
- OMDb API responses

---

## Domain Concepts

### Entities

#### Entity: User

Represents a registered system user.

Attributes:

- id
- username
- email
- password

---

#### Entity: SessionUser

Represents the currently authenticated user session.

Attributes:

- username
- user_id

---

### Aggregates

#### Aggregate: Watchlist

Represents the collection of movies a user intends to watch.

Attributes:

- user_id
- titles

---

#### Aggregate: Watched

Represents the collection of movies already watched by a user.

Attributes:

- user_id
- titles

---

### Value Objects

#### Value Object: Genre

Represents a movie genre preference.

Attributes:

- string value

---

## Repositories

### SqliteRepo

Responsible for the persistence of:

- users
- watchlist
- watched
- preferences

Encapsulates all database queries and ensures separation between domain logic and data storage.

---

## Domain Services

### AppService

Acts as a domain service that:

- Coordinates repositories
- Implements recommendation logic
- Orchestrates authentication flow
- Connects application layer with infrastructure

---

## Context Map Diagram

<img width="761" height="230" alt="image" src="https://github.com/user-attachments/assets/f3df5c4c-82dc-4ada-96e1-d5b54ee69537" />

---

## 3.4 Object-Oriented Modelling

This section describes the main classes of the system and their responsibilities following object-oriented design principles.

---

### Main Classes

---

### 1️. AppService

**Role:**  
Acts as the application service layer and orchestrates business logic between the presentation layer and infrastructure layer.

**Responsibilities:**

- Handles authentication workflow
- Manages watchlist operations
- Coordinates recommendation logic
- Fetches movie details from external services
- Delegates persistence to the repository layer

**Methods:**

- `sign_up()`
- `login()`
- `add_to_watchlist()`
- `set_genres()’
- `get_genres()`
- `add_to_whatchlist()`
-  `remove_from_watchlist()`
- `clear_watchlist()`
- `list_watchlist()` 
- `add_to_watched()`
- `clear_watched()`
- `list_watchlist()`
- `recommend_titles()`
- `fetch_movie_details()`

---

### 2️. SqliteRepo

**Role:**  
Handles all persistence operations using SQLite.

Encapsulates direct database access and prevents the application layer from executing SQL queries directly.

**Responsibilities:**

- User creation and verification
- Watchlist persistence
- Genre storage
- Retrieval of stored data

**Methods:**

- `create_user()`
- `verify_login()`
- `get_user_id_by_email()`
- `get_username_by_email()`
- `set_favorite_genres()`
- `get_favorite_genres()`
- `add_watchlist()`
- `remove_watchlist()`
- `clear_watchlist()`
- `list_watchlist()`
- `add_watched()`
- `clear_watched()`
- `list_watched()`


---

### 3️. OmdbClient

**Role:**  
Encapsulates communication with the external OMDb API.

**Responsibilities:**

- Sends HTTP requests to the OMDb API
- Parses JSON responses
- Handles API errors gracefully

**Methods:**

- `search_by_title()`

---

### Design Principles Applied

- **Single Responsibility Principle (SRP)**  
  Each class has a clearly defined responsibility.

- **Separation of Concerns**  
  UI, business logic, and infrastructure are separated.

- **Dependency Direction**  
  `AppService` depends on `SqliteRepo` and `OmdbClient`, but not vice versa.

---
### UML class diagram

<img width="397" height="641" alt="image" src="https://github.com/user-attachments/assets/0f8bb761-7a7b-4d1b-bb2a-ce354f47395a" />

### Sequence: Fetch Movie Details

<img width="653" height="383" alt="image" src="https://github.com/user-attachments/assets/f31092c4-5b68-44c4-8b1e-6f0ceaff7771" />


--- 
## 3.6 Behaviour

This section describes the system’s runtime behavior and how state is managed.

---

### Stateful Components

The following components maintain persistent or session-based state:

- **SQLite database**  
  Stores all persistent user-related data.

- **Session state (user login)**  
  Maintains the authenticated user context during interaction.

---

### Stateless Components

The following components do not store persistent state:

- **OmdbClient**  
  Acts as a wrapper around HTTP requests to the OMDb API.

- **Recommendation logic**  
  Computed dynamically based on:
  - Favorite genres
  - Watch history

No recommendation data is permanently stored.

---

### State Updates Occur:

- On registration  
- On login  
- On watchlist modification  
- On genre selection  

State transitions are controlled through the Application Layer (`AppService`).

---

## 3.7 Data-Related Aspects

This section describes how data is structured, stored, and accessed.

---

### Persistent Data

The system stores the following data:

- Users
- Favorite genres
- Watchlist
- Watched list

---

### Storage Type

- **Relational database (SQLite)**

---

### Justification

SQLite was chosen because:

- Data is structured and relational
- Relationships between users and movie lists are simple
- No distributed database is required
- Suitable for lightweight academic scope

---

### Query Execution

All database queries are performed exclusively by:

- `SqliteRepo`

This ensures:

- Encapsulation of persistence logic
- Clear separation between business logic and data access

---

### Concurrency Model

- Single-user environment
- No concurrent write conflicts expected
- No need for advanced transaction management

---

 
