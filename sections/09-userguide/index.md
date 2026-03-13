title: User Guide
has_children: false
nav_order: 10
---

# User Guide

This section explains how an end user can interact with the *Popcorn Meter* application once it is deployed and running.

Popcorn Meter is a web-based movie recommendation application that allows users to search for movies, view detailed movie information, manage a personal watchlist, track watched movies, and receive personalized recommendations based on preferences and activity history.

Users interact with the system through a browser-based interface.

---

# Accessing the Application

Once deployed, the application can be opened through a web browser using the provided URL.

The interface is divided into two main areas:

- *Navigation panel (left sidebar)*
- *Main interaction area (center of the page)*

The sidebar allows users to move between the main sections of the application:

- *Home*
- *Account*
- *Favorite Genres*
- *Watchlist*
- *Watched*
- *Recommendations*

<img width="1802" height="670" alt="image" src="https://github.com/user-attachments/assets/b77edc38-8f45-44fc-9d10-73d6f0f18b65" />


---

# User Roles

The system supports two types of users.

## Guest User

A guest user can browse the application without authentication.

Guest users can:

- search for movies from the *Home* page
- view movie details
- browse trending movies


  

Guest users cannot save personal data such as:

- favorite genres
- watchlist entries
- watched history
- feedback on recommendations

## Registered User

A registered user can log in and access personalized features.

Registered users can:

- choose favorite genres
- maintain a watchlist
- track watched movies
- receive personalized recommendations
- give feedback on movies through likes, dislikes, and ratings

---

# Home Page

The *Home* page is the main entry point of the application.

It includes:

- a movie title search bar
- a trending movies section
- personalized recommendations for logged-in users who have selected favorite genres

Home page behavior depends on the user state:

- *Guest users* see trending movies and a message inviting them to log in for personalized recommendations
- *Logged-in users without favorite genres* see trending movies and a prompt to select genres first
- *Logged-in users with favorite genres* see personalized recommendations first, followed by trending movies

If trending data cannot be retrieved from the external API, the system shows a fallback message and a small default movie set.

---

# Creating an Account

To register a new account:

1. Open the *Account* page from the sidebar.
2. Select the *Sign up* tab.
3. Enter:
   - username
   - email address
   - password
4. Click *Create account*.

If the registration is successful, the account is stored in the system database and the user can log in from the *Login* tab.

<img width="1857" height="803" alt="image" src="https://github.com/user-attachments/assets/3fb7153c-47ef-498f-9d7e-62291455f628" />



---

# Logging In

To access personalized features:

1. Open the *Account* page.
2. Select the *Login* tab.
3. Enter:
   - email
   - password
4. Click *Login*.

If the credentials are correct, the user session is created and the interface updates to show the logged-in user.

<img width="1087" height="622" alt="image" src="https://github.com/user-attachments/assets/7e6f0eb1-4c7b-4463-b0b0-a040861a973d" />



If the credentials are invalid, the system shows an error message.

<img width="1355" height="567" alt="image" src="https://github.com/user-attachments/assets/7939a96f-ff9a-45d2-a811-78fd78ce857f" />



---

# Logging Out

When logged in, the *Account* page shows a welcome message and a *Logout* button.

By logging out, the system returns to guest mode and personalized features are disabled.

---

# Searching for Movies

Movie search is performed from the *Home* page.

Steps:

1. Enter a movie title in the search field.
2. Click the search button.
3. The system retrieves movie details using the configured movie APIs.

If the title is found, the movie details dialog opens automatically.  

<img width="1346" height="810" alt="image" src="https://github.com/user-attachments/assets/ff09f4d4-806b-4bf9-b94e-0032e3585a6c" />

For users, there are actions:
<img width="586" height="817" alt="image" src="https://github.com/user-attachments/assets/9f07a499-1a5c-40f0-9ea6-4f78d60f4f3d" />



If the title is not found, the system displays an error message.
<img width="1362" height="232" alt="image" src="https://github.com/user-attachments/assets/c002008b-0808-45e3-93ec-e27994eaf68c" />





---

# Viewing Movie Details

Movies displayed in search results, trending lists, watchlist, watched list, and recommendations can be opened using the *Details* button.

The movie details dialog may include:

- title
- release year
- poster
- IMDb rating
- runtime
- genre
- plot summary
- director
- cast
- language
- country

The dialog also provides a *Where to watch* section with quick links to external platforms such as:

- Netflix
- Prime Video
- Disney+
- YouTube
- Google
- official website, if available

<img width="816" height="823" alt="image" src="https://github.com/user-attachments/assets/a90b4a9c-3bec-4478-8997-ef02eecc1207" />



---

# Managing Favorite Genres

The *Favorite Genres* page allows registered users to define their preferred movie genres.

Steps:

1. Open *Favorite Genres* from the sidebar.
3. Select one or more genres from the list.
   
   <img width="1411" height="641" alt="image" src="https://github.com/user-attachments/assets/a98e883a-c226-4d7b-8a35-db005b2d430a" />


5. Click *Save*.
<img width="710" height="617" alt="image" src="https://github.com/user-attachments/assets/5ecefb29-4c22-44f9-a372-8320b5ceecf8" />


These preferences are used as the strongest signal in recommendation generation.

Users can also clear all selected genres using *Clear selection*.

---

# Managing the Watchlist

The *Watchlist* page shows the list of movies the user wants to watch.

Users can:

- add a movie manually by entering its title
- add a movie from the movie details dialog
- remove a movie from their lists using the movie details dialog
- clear the entire watchlist

<img width="1466" height="783" alt="image" src="https://github.com/user-attachments/assets/e2afd8f7-7053-4835-903d-9170cb9a9131" />


  
If a manually entered movie title does not exist, the system shows an error.

---

# Managing Watched Movies

The *Watched* page stores the user’s watched movie history.

Users can:

- add a watched movie manually by title
- add a movie to watched from the movie details dialog
- remove a movie from their lists using the movie details dialog
- clear the watched list

The watched list is used by the system to avoid recommending movies the user has already seen.

<img width="1296" height="830" alt="image" src="https://github.com/user-attachments/assets/1f9951b3-10bf-48b7-87e8-81b192e8666b" />


---

# Giving Feedback on Movies

When a logged-in user opens a movie details dialog, the application also provides feedback actions.

Users can:

- mark a movie as *Like*
- mark a movie as *Dislike*
- save a numeric rating
- mark a movie as *Not interested*, which hides it from recommendations

This feedback is used to further refine recommendation results.

<img width="648" height="558" alt="image" src="https://github.com/user-attachments/assets/26dbfc74-a149-4570-ae90-b253f5170d78" />


---

# Viewing Recommendations

The *Recommendations* page provides personalized movie suggestions for logged-in users.

Recommendations are based on a hybrid heuristic scoring system using:

1. favorite genres
2. actors appearing in watched movies
3. IMDb rating
4. plot keywords related to preferred genres
5. watchlist presence
6. user feedback such as likes, dislikes, and ratings

The system excludes movies already marked as watched.

<img width="1848" height="802" alt="image" src="https://github.com/user-attachments/assets/dd2aa3bb-a102-4a4c-b171-e0a248eeaa1f" />


If the user has not selected favorite genres yet, the page shows a message asking them to do so first.

<img width="1400" height="388" alt="image" src="https://github.com/user-attachments/assets/02d0acea-5363-4d6e-903a-be1e5023f4eb" />



---

# Recommendation Filters

The *Recommendations* page also includes filters in the sidebar.

Users can filter recommendations by:

- *Minimum IMDb rating*
- *Year range*

<img width="352" height="527" alt="image" src="https://github.com/user-attachments/assets/88bbd138-243a-4f65-8c93-fe807f7aa43d" />


If no movie matches the selected filters, the system shows an informative message.

Recommendations are paginated when the result set is large.

---

# Error Messages

The system may display messages in situations such as:

- *Movie not found*: when a title cannot be retrieved from the external movie API
- *Invalid email or password*: when login credentials are incorrect
- *Could not create account*: when fields are empty or the email already exists
- *Login required*: when a guest user tries to access saved-personal-data features
- *Trending is temporarily unavailable*: when trending data cannot be retrieved
- *API key missing*: when external movie API keys are not configured

These messages help users understand what action is required to continue.
