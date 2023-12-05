## Movie Recommendataion System using Content Based Filtering

### Introduction
- This project is a movie recommendation system using content based filtering.
- The first dataset which contains information about movies till 2017 used is the TMDB 5000 Movie Dataset which contains information about 5000 movies. The dataset can be found [here](https://www.kaggle.com/tmdb/tmdb-movie-metadata).
- The dataset for movies from 2018 to 2023 is created using the TMDB API and Wikipedia.
- The names of the movies were scraped from Wikipedia and the data was collected using the TMDB API.
- TMDB API :- [TMDB](https://developer.themoviedb.org/reference/search-movie)
- Wikipedia links :-
    - [2018](https://en.wikipedia.org/wiki/List_of_American_films_of_2018)
    - [2019](https://en.wikipedia.org/wiki/List_of_American_films_of_2019)
    - [2020](https://en.wikipedia.org/wiki/List_of_American_films_of_2020)
    - [2021](https://en.wikipedia.org/wiki/List_of_American_films_of_2021)
    - [2022](https://en.wikipedia.org/wiki/List_of_American_films_of_2022)
    - [2023](https://en.wikipedia.org/wiki/List_of_American_films_of_2023)

### The model
- The model uses the cosine similarity between the movie vectors to find the most similar movies.
- The movie vectors are created using the following features:
    - The genres of the movie
    - The cast of the movie
    - The director of the movie
    - The keywords of the movie
    - The overview of the movie

### What is happening in the code ?
1.  Stemming:
    -   It uses the `nltk.stem.porter` module's `PorterStemmer` to perform stemming on the text data in the 'tags' column of the DataFrame (`ew_df`).
    -   Stemming reduces words to their root form (e.g., 'running' to 'run', 'easily' to 'easili'), aiming to normalize the text data for analysis.

2.  CountVectorizer:
    -   Utilizes `CountVectorizer` from `sklearn.feature_extraction.text` to convert the processed 'tags' data into numerical vectors.
    -   `max_features=5000` sets the maximum number of features to consider.
    -   `stop_words='english'` removes English stop words (common words like 'and', 'the', 'is', etc.) during vectorization.

3.  Cosine Similarity:
    -   Calculates the cosine similarity between the vectors derived from the 'tags' using `cosine_similarity` from `sklearn.metrics.pairwise`.

    <img alt="Cosine Similarity" src ="./screenshots/_1.png"/>
    -   This similarity matrix shows how similar movies are based on their 'tags' content.

4.  Recommendation Function (`recommend`):
    -   Finds the index of the given movie in the DataFrame (`new_df`) based on its title.
    -   Retrieves the similarity scores of that movie with all others from the similarity matrix.
    -   Sorts the movies by similarity scores and prints the top 5 recommendations (excluding the queried movie).

   