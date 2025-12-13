---
title: Home
layout: home
has_children: false
nav_order: 1
---

# PopcornMeter

### Authors

- [Ethar Mohammed Hassan Ali](mailto:ethar.ali@unibo.it)
- [Farideh Tavakoli](mailto:farideh.tavakoli@studio.unibo.it)
- [Kosar Mazahery](mailto:kosar.mazahery@studio.unibo.it)

## Abstract

### Overview

We are building a **Movie Recommendation Website** designed to improve how users discover movies by delivering **personalized suggestions** based on their preferences and activity. The platform will allow users to create an account, manage their profiles, organize movies into watchlists, and receive recommendations that evolve over time.

### Core User Experience

After signing up and logging in, each user will have access to:

- **Account/Profile Page**
    
    Stores and displays user information (e.g., username, email, basic settings).
    
- **Favorite Genres Page**
    
    Users can select and update their preferred genres, which will directly influence recommendations.
    
- **Watchlist System (3 Status Categories)**
    
    Users can manage movies under:
    
    - Want to Watch
    - Watching
    - Watched

This watchlist history helps the system understand the user’s taste and refine recommendations.

### Recommendation Approach

The website will include a **rule-based recommendation system** (simple and explainable). For example:

- Recommend movies that match the user’s **top favorite genres**
- Increase recommendation priority for genres that appear frequently in the user’s **Watched** list
- Optionally reduce repetition by filtering out movies the user has already marked as **Watched**

This approach ensures recommendations are **personalized, fast, and easy to implement/debug**, while still feeling relevant to the user.

### Movie Data and API Integration

To provide rich and reliable movie details, the application will integrate with a **public movie API**. When a user searches for a title, the system will call the API to fetch information such as:

- Poster and cover images
- Description/overview
- Cast and crew
- Genres, ratings, runtime, release year
- Availability and/or links to streaming platforms (when supported by the API)

### Database and Backend Design

A **relational database** will store and manage user data and watchlist history. Key stored data will include:

- User accounts and authentication data
- Favorite genres
- Watchlist entries (movie + status + timestamps)
- Recommendation-related data (e.g., genre weights, recently recommended titles)

This structure supports filtering and recommendation logic using attributes like **genre, rating, themes, cast**, and other available metadata from the API.

### Expected Outcomes

By combining account personalization, structured watchlists, API-powered movie details, and an explainable recommendation algorithm, the platform will help users:

- Discover movies aligned with their interests
- Track what they’ve watched and what they plan to watch
- Get better recommendations as their activity increases
- Access movie information quickly through search and detailed results

