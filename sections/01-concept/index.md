---
title: Concept
has_children: false
nav_order: 1
---

# Concept

Popcorn Meter is a small web application with a GUI built in Streamlit. It helps users discover movies, keep a personal watchlist, track watched movies, and get simple recommendations.

From a usage perspective, users interact with the app through a browser on laptop/desktop/tablet, typically in short sessions when deciding what to watch.

## Use cases and users

- **Registered user**: signs in, searches movies, saves watchlist items, marks watched movies, sets favorite genres, and receives personalized suggestions.
- **Guest user**: can search and view movie details, but cannot save personal data until login.

## Data and storage

The app stores user-related data locally in SQLite (accounts, favorite genres, watchlist, watched history). Movie information is fetched from external APIs (OMDb/TMDb integrations) during search and recommendation flows.

## Interaction model

The main flow is: search movie -> view details -> save or mark watched -> update preferences -> review recommendations.
