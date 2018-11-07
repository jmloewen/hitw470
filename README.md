# Rare Eats

_Discover Restaurants You Love_

By _WebsiteDispenser_

## Access the Website

- Vagrant Up and navigate to http://localhost:8080/.
- Log in as Admin (see below for login info) or create an account to explore the app's functionalities.

## What does the app do?

- Facilitates finding restaurants.
- Gives users recommendations based on their preferences.
    - Users need to create a list of restaurants to receive a recommendation.

## Features:

- View restaurants in Vancouver.
- Create personalized lists of restaurants based on the plan category. i.e. "Date Night" or "Post-Workout."
    - Append a restaurant to the list from the restaurant's view page.
- Recommend restaurants based on users' personal lists.
- Review and rate restaurants.

## Technology Stack

- **Codeigniter**
    - Reason:
        - 3/6 people in our group had experience with PHP.
    - Benefits:
        - Simple MVC and installation.
        - Does not enforce the use of a templating languge (besides PHP).
        - Comes with built-in protection against CSRF and XSS attacks.
        - Good documentation (Mircea really likes it)
    - Issues:
        - No authentication library.
            - All user authentication features are created from scratch using Codeigniter's session.

- **Foursquare**
    - "Why did we use Foursquare over Google Places, or Zomato?
        - There are a few reasons for this.
            - First, neither Google Places nor Zomato allow the storage of their data.  We wanted to honor the TOS of these APIs, and used Foursquare instead, which allows storage of its API data, so long as the data is refreshed every 30 days.
            - Second, Foursquare was the most familiar tool to the three members on our team, letting us develop faster.
            - Third, Foursquare's free account provided a more flexible functionality than Places and Zomato, despite having inferior data available and requiring more navigation.
    - "What data did we scalp?"
        - Since this is not a live website, and is merely a demonstration, we chose a specific set of data to load.  This included restaurants from preselected categories, targeted to help us create recommendation lists based on time of day.
            - The general 'Food' category, which encompasses all restaurants
            - Breakfast
            - Cafes
            - Sandwiches
            - Comfort food
    - "What was the data querying process?"
        - The idea behind the website is to eliminate chain restaurants and fast food, promoting unpopular and high quality restaurants. To accomplish this without manually entering a large amount of data, we first loaded a list of categories from Foursquare.
        - These categories were then filtered to remove undesireable and unsuitable items.
            - Restaurants are loaded if they are tagged by one of these allowed categories and not a banned one, and are not a chain (ex: Cactus Club).
                - We then load a static number of restaurants and photos for each item.  This is done on migration on first load of the site.
        - We also make a call for the restaurant's latitude and longitude on access to an individual restaurant page. This data is used to query Google Maps and allow users to navigate to the selected website.
            -This was not added to the database since some members disagreed, and it was a feature added late in the project.
    - "What API features would we add given more time?"
        - If this were to become a full project, the app would suggest nearby restaurants from the API based on the user's current location.  Currently, the app displays a set of sample data based on a relatively static JSON query.
            - This would have been in the base project, but the group was strongly against doing this - I don't know why.  They likely considered it to be too complex (it's really not).
        - If this project were to continue, the above location data would be added to the database, increasing overall stability of the website and reducing usage of the API.
        - As review data obtained from Foursquare does not include ratings or a tagging system analogous to our data, I would consider adding tags from the user review text, as well as predicting how positive a review is based on the supplied text.
            - I would also allow reviews to push from our site to the Foursquare API.

## Accounts

- Admin account:
    - overlord@example.com
    - pwd: admin
    - can edit/delete restaurants
    - can create/edit/delete tags
    - can delete user playlists

## Contributions

- Everyone:
    - Code Review
    - Debugging

- Jon:
    - API Integration with Foursquare to load restaurants, cuisine type tags
    - Photos, Reviews for each restaurant.
    - Google Maps link integration
    - Data filtering to remove unwanted cuisine types
    - Associating restaurants with tags

- Mircea
    - Restaurant CRUD
    - Restaurant Search
    - User Playlist search (shows all for admin, otherwise shows user’s private lists and public non-private lists)
    - Ratings Display on Restaurant Search
    - Font-Awesome Icons throughout site
    - Website design/styling across the board

- Isis
    - Reviews CRUD
    - Ratings (like/dislike) CRUD
    - Login redirect to original page

- Harris
    - User playlists CRUD
    - Adding/removing restaurants to/from playlists (contents table)
    - Subscribing to (unsubscribing from) playlists
    - Viewing of playlists by author, viewing all subscribed playlists

- Farzin
    - CRUD + Search for Users (no scaffolding in codeigniter)
    - Login/Maintaining Session (No Authentication library in Codeigniter)
    - Landing page (only the jumbotron bit)
    - Auto Playlists (recommendations) creation based off tags in a user's playlists, season, or time of day (breakfast/lunch/dinner)

- Piet
    - Initial database design
    - Initial website groundwork
    - Add/Remove tags to/from restaurants
    - All of poster design
    - Knowledge of CodeIgniter
    - Vagrant (and webserver) setup

## Known Bugs/Issues/TODOs:

(QA Testing By Andy Sun)
- Subscription to a public list that is later turned private still shows up on the list of subscribed lists but the subscribed user cannot access it because its been made private
- Password cannot be reset
- No proper admin panel. Admin cannot edit user information or view individual user profiles
