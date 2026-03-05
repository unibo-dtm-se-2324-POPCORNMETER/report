

# Concept

The project developed in this work is a **web-based application with a graphical user interface (GUI)** designed to help users explore movies and manage their personal movie preferences. The system allows users to search for movie information, maintain a watchlist, track watched movies, and receive recommendations based on their favorite genres.

The application is implemented as a **web application**, meaning that users interact with it through a web browser. The graphical interface is built using Streamlit, which allows users to interact with the system through buttons, forms, and navigation elements without requiring technical knowledge.

----------

## Type of Product

The developed system can be classified as:

**Web Application (GUI)**

It provides an interactive interface where users can:

-   search for movies
    
-   view movie information
    
-   manage their personal watchlist
    
-   mark movies as watched
    
-   receive recommendations based on selected genres
    

The application also integrates an **external movie database service (OMDb API)** to retrieve movie metadata such as title, year, genre, plot, and poster.

----------

## Users and Interaction

The system is designed for **individual users interested in discovering and organizing movies**. These users interact with the application through a standard web browser.

Users are expected to interact with the system:

-   occasionally when searching for movie information
    
-   when planning movies they want to watch
    
-   when tracking movies they have already watched
    

The interaction frequency is therefore **irregular and user-driven**, typically occurring whenever a user wants to explore new movies or update their watchlist.

----------

## Interaction Devices

Users interact with the system through **personal computing devices**, such as:

-   laptops
    
-   desktop computers
    
-   tablets
    

Since the application is web-based, it does not require installation and can be accessed directly through a browser.

----------

## User Roles

The system distinguishes between two main user roles:

### Guest Users

Guest users can access the application without authentication. They can:

-   search for movies
    
-   view movie details retrieved from the external API
    

However, they cannot store personalized data.

### Registered Users

Registered users can log into the system and access additional features, including:

-   saving movies to a watchlist
    
-   marking movies as watched
    
-   selecting favorite genres
    
-   receiving personalized recommendations
    

----------

## Data Storage

The system stores user-related data in a **local relational database (SQLite)**.

The stored data includes:

-   user accounts (username, email, password)
    
-   favorite genres
    
-   watchlist entries
    
-   watched movie lists
    

This data allows the system to personalize the experience for each user and maintain persistent information between sessions.

Movie metadata itself is **not stored locally**, but retrieved dynamically from the OMDb API whenever a search is performed.

----------

## System Usage Context

The application is intended as a **personal movie discovery and tracking tool**. It helps users organize their viewing preferences and discover new movies in a simple and accessible way.

Because the system integrates external movie information services while maintaining user-specific data locally, it combines both **data retrieval from external sources and persistent local data management**.

