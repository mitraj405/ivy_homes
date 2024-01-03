# IMDb Genre-Based Movie Data and Reviews Extractor

## Overview

This script automates the extraction of movie data by genre from IMDb. It retrieves details for the top 20 movies per genre and their latest 10 user reviews, leveraging web scraping to handle server-rendered pages and process data for MongoDB storage.

## Table of Contents

- [Flow of the Script]
- [Database Integration]
  - [MongoDB Functions]
  - [Note on MongoDB Operations]
- [Challenges and Solutions]
- [Predefined Strings]
- [Instructions for Use]
- [Submission Instructions]

## Flow of the Script
![Untitled Diagram drawio](https://github.com/mitraj405/ivy_homes/assets/47468515/8642fcc4-8e3d-4432-abef-ed4ff4d213b3)



1. **Initialization**: Begins with a list of predefined string constants essential for the script's operation.
2. **Genre Fetching**: `fetch_genres()` retrieves a `genres_list` containing dictionary-type data with genre names.
3. **Top Movies Retrieval**: `fetch_top_20_for_genre()` fetches the top 20 movies for each genre, identified by unique IDs.
4. **Detail and Review Extraction**: Utilizes two functions:
    - `fetch_details_from_url()`: Gathers detailed information for each movie.
    - `fetch_reviews_for_title()`: Collects the latest 10 user reviews per movie.
5. **Data Storage**: Selectively stores movie details, reviews, or both in `accumulated_movie_details`, `global_movie_details`, and `global_reviews`.

## Database Integration

The script requires MongoDB to be running. MongoDB Compass is recommended for a user-friendly interface.

### MongoDB Functions

- `insert_genres_into_mongo()`: Mandatory for genre-based data storage.
- `insert_movies_into_mongo()`: Stores a compact list of movie details.
- `insert_reviews_into_mongo()`: Stores reviews for each movie.
- `insert_accumulated_movies_into_mongo()`: Stores all movies genre-wise.

### Note on MongoDB Operations

Only execute `client.close()` after completing all database operations to prevent data loss.

## Challenges and Solutions

- **Server-Side Rendering**: Overcome by parsing JSON data from `__NEXT_DATA__` and HTML elements for reviews.
- **Efficiency**: Optimized to fetch only necessary data, not the entire HTML page.
- **Extensibility**: Includes functionalities to accommodate future requirements with diverse parameter options.

## Predefined Strings

Configure the script's fetching behavior with these strings:

```python
# Define genre selection
genre_movies = "movieGenreList"
genre_tv_shows = "tvGenreList"
genre_video_games = "videoGameGenreList"

# Define top titles fetching
title_video_game = "video_game"
title_tv_series = "tv_series,tv_miniseries"
title_movies = "feature"

# Define sorting options
sort_titles_by_popularity = "moviemeter"
# ... other sorting options ...
```

## Instructions for Use

1. Confirm MongoDB installation and start the service.
2. Clone the GitHub repository and install Python dependencies.
3. If interrupted, restart the script from the beginning to maintain dictionary integrity.
4. Adhere to provided parameters and structures for script functions.
5. Use MongoDB insertion functions to persist data.
