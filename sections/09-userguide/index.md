---
title: Future work
has_children: false
nav_order: 10
---

# User Guide

This section explains how an end user can interact with the **Popcorn Meter** application after it has been deployed and is running.

Popcorn Meter is a web-based application that allows users to search for movies, view movie details, manage a personal watchlist, record watched movies, and receive movie recommendations based on their preferences.

Users interact with the system through a **web interface**, typically accessed through a browser.

----------

# Accessing the Application

Once deployed, the application can be opened through a web browser using the provided URL.



The system interface is divided into two main areas:

-   **Navigation panel (left sidebar)**
    
-   **Main interaction area (center of the page)**
    

The sidebar allows users to navigate between different sections of the application.

<img width="1788" height="788" alt="image" src="https://github.com/user-attachments/assets/5a540253-9ef0-43a2-a515-4271ddab484d" />


----------

# User Roles

The system supports two types of users:

### Guest User

A guest user can browse the application without authentication.

Guest users can:

-   search for movies
    
-   view movie details
    

However, guest users **cannot save personal data** such as watchlists or preferences.

<img width="1830" height="697" alt="image" src="https://github.com/user-attachments/assets/2ea5ff4f-572e-4b16-94d9-902ff3a23462" />


----------

### Registered User

A registered user can log in and access personalized features.

Registered users can:

-   manage favorite genres
    
-   maintain a watchlist
    
-   track watched movies
    
-   receive movie recommendations
    

----------

# Creating an Account

To register a new account:

1.  Navigate to the **Account** section in the sidebar.
    
2.  Enter the required information:
    
    -   Username
        
    -   Email address
        
    -   Password
        
3.  Submit the registration form.
    

If the registration is successful, the user account will be stored in the system database.

<img width="1795" height="587" alt="image" src="https://github.com/user-attachments/assets/2cf28210-ca8e-4938-b3b9-01ec5930e535" />


----------

# Logging In

To access personalized features:

1.  Open the **Account** section.
    
2.  Enter:
    
    -   Email
        
    -   Password
        
3.  Click **Log In**.
    

If the credentials are correct, the user session will be created and the interface will show the logged-in user.

<img width="1551" height="486" alt="image" src="https://github.com/user-attachments/assets/2994aaca-d50e-4f5e-8b48-ef3743706a78" />

----------

# Searching for Movies

The **Search** section allows users to look for movies by title.

Steps:

1.  Enter a movie title in the **Movie title** search field.
    
2.  Click **Fetch details**.
    

The system retrieves movie information using the **OMDb API** and displays details such as:

-   movie title
    
-   release year
    
-   genre
    
-   plot summary
    
-   poster image (if available)
    

----------

# Adding Movies to the Watchlist

Logged-in users can save movies for later viewing.

Steps:

1.  Search for a movie using the search field.
    
2.  Click **Add to Watchlist**.
    

The movie will be stored in the user’s watchlist.

<img width="1820" height="855" alt="image" src="https://github.com/user-attachments/assets/80bbdeae-af57-43f7-91e6-049d098175ca" />


----------

# Managing Favorite Genres

Users can specify their preferred movie genres.

Steps:

1.  Navigate to the **Favorite Genres** section.
    
2.  Select the genres of interest.
    
3.  Save the selection.
    

These preferences are used by the system to generate personalized recommendations.

<img width="1746" height="497" alt="image" src="https://github.com/user-attachments/assets/e52d2eff-40d0-4b6f-af9a-e031cea5e60c" />


----------

# Managing the Watchlist

The **Watchlist** section shows all movies saved by the user.

Users can:

-   view saved movies
    
-   remove movies from the watchlist

<img width="1402" height="640" alt="image" src="https://github.com/user-attachments/assets/4883aec8-bf00-4899-bcab-30452734553a" />

    

----------

# Managing Watched Movies

Users can record movies they have already watched.

Steps:

1.  Navigate to the **Watched** section.
    
2.  Add movie titles to the watched list.
    

The watched list is used to avoid recommending movies the user has already seen.

<img width="1381" height="612" alt="image" src="https://github.com/user-attachments/assets/128461ce-43c5-4bee-b0da-b1c842d5ccd5" />


----------

# Viewing Recommendations

The Recommendations section generates personalized movie suggestions.

The recommendation engine uses a hybrid scoring system based on:

1. favorite genres (strongest signal)

2. actors appearing in previously watched movies

3. IMDb rating

4. plot keywords related to preferred genres

5. watchlist presence

6. user feedback (likes, dislikes, ratings)
    

The system generates a list of recommended movie titles that match the user's preferences but have not yet been watched.

<img width="796" height="727" alt="image" src="https://github.com/user-attachments/assets/88ebf51e-8f5f-4fd8-ac21-8ccf4a936e68" />


----------

# Logging Out

Users can end their session by selecting **Log Out** from the account section.

After logging out, the system returns to guest mode and personalized features are disabled.

----------

# Error Messages

The system may display messages in the following situations:

-   **Movie not found** – when the OMDb API cannot find a matching title
    
-   **Login required** – when attempting to save data without being logged in
    
-   **API key missing** – when the OMDb API key has not been configured in the system environment
    

These messages help users understand what action is required to proceed.


