# (PROBLEM - A) IMDb Genre-Based Movie Data and Reviews Extractor

## (Bonus Point - Video Explanation Link)
I will recommend to watch my explanation video, to understand code and solution in a better way
! ([drive link](https://drive.google.com/file/d/1jJL7YlxXO-Fab_tNwkEOOrqJbHR0KH1m/view?usp=sharing))


## Overview

This script automates the extraction of movie data by genre from IMDb. It retrieves details for the top 20 movies per genre and their latest 10 user reviews, leveraging web scraping to handle server-rendered pages and process data for MongoDB storage.

## Table of Contents

- [Overview]
- [Table of Contents]
- [Flow of the Script]
- [Database Integration]
- [Database Schema]
- [Data Dump]
- [Challenges and Solutions]
- [Predefined Strings]
- [Instructions for Use]
- [Submission Instructions]

## Flow of the Script

![Flow of Script](https://github.com/mitraj405/ivy_homes/assets/47468515/8642fcc4-8e3d-4432-abef-ed4ff4d213b3)

The script operates as follows:

1. **Initialization**: It begins with a list of predefined string constants essential for the script's operation.
2. **Genre Fetching**: The `fetch_genres()` function retrieves a `genres_list` containing dictionary-type data with genre names.
3. **Top Movies Retrieval**: The `fetch_top_20_for_genre()` function fetches the top 20 movies for each genre, identified by their unique IDs.
4. **Detail and Review Extraction**: It utilizes two functions to gather details and reviews:
    - `fetch_details_from_url()`: For gathering detailed information about each movie.
    - `fetch_reviews_for_title()`: For collecting the latest 10 user reviews for each movie.
5. **Data Storage**: It selectively stores movie details and reviews in `accumulated_movie_details`, `global_movie_details`, and `global_reviews`.

## Database Integration

The script requires a running MongoDB instance. MongoDB Compass is recommended for a user-friendly interface.

### MongoDB Functions

- `insert_genres_into_mongo()`: For genre-based data storage.
- `insert_movies_into_mongo()`: For storing compact movie details.
- `insert_reviews_into_mongo()`: For storing movie reviews.
- `insert_accumulated_movies_into_mongo()`: For storing all movies genre-wise.

### Note on MongoDB Operations

Execute `client.close()` only after completing all database operations to prevent data loss.

## Database Schema

Below is the schema diagram for the database used by this script:

![Untitled (1)](https://github.com/mitraj405/ivy_homes/assets/47468515/f6f8105a-5d55-4bb6-95f4-ebd08360f579)


The database consists of the following tables:

- **Movies**: Stores details about movies, including cast and genres.
- **Genres**: Contains the different genres available.
- **Reviews**: Holds user reviews for movies.
- **Acc_Movies**: An accumulation of movies with genre-wise details.

Relationships:

- `"Movies"."genres"` < `"Genres"."_id"`: Movies have multiple genres.
- `"Acc_Movies"."genres"` <> `"Genres"."_id"`: Accumulated movies have a many-to-many relationship with genres.
- `"Reviews"."genres"` < `"Genres"."_id"`: Reviews are associated with genres.

## Data Dump

The dump of the database has been provided in the CSV format and is available in the repository.

## Challenges and Solutions

- **Server-Side Rendering**: The script parses JSON data from `__NEXT_DATA__` and HTML elements for reviews.
- **Efficiency**: It fetches only the necessary data, not entire HTML pages.
- **Extensibility**: The script includes additional functionalities to cater to future requirements.

## Predefined Strings

The script's behavior is configured with the following predefined strings:

```python
# Genre selection
genre_movies = "movieGenreList"
genre_tv_shows = "tvGenreList"
genre_video_games = "videoGameGenreList"

# Top titles fetching
title_video_game = "video_game"
title_tv_series = "tv_series,tv_miniseries"
title_movies = "feature"

# Sorting options
sort_titles_by_popularity = "moviemeter"
# ... other sorting options ...
```

## Instructions for Use

1. Confirm MongoDB installation and start the service.
2. Clone the GitHub repository and install Python dependencies.
3. If interrupted, restart the script from the beginning to maintain dictionary integrity.
4. Adhere to provided parameters and structures for script functions.
5. Use MongoDB insertion functions to persist data.
