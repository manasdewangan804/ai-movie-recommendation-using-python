# 🎬 AI Movie Recommendation System

A content-based movie recommender built with **Python**, **scikit-learn**, and **Streamlit** (with custom HTML/CSS for styling).

## How it works

1. **Data**: `movies.csv` holds 50+ movies with title, genres, director, cast, overview, and keywords.
2. **Feature engineering**: `recommender.py` combines those text fields into one "tags" string per movie (genres, director, and keywords are weighted more heavily than the plain overview).
3. **Vectorization**: `TfidfVectorizer` (scikit-learn) turns each movie's tags into a numeric vector, ignoring common English stop words.
4. **Similarity**: `cosine_similarity` computes how close every pair of movies is in that vector space.
5. **Recommendation**: given a movie you like, the app looks up its similarity scores against every other movie and returns the top matches.

## Project structure

```
movie-recommender/
├── app.py            # Streamlit UI (with HTML/CSS banner)
├── recommender.py     # Core ML logic (TF-IDF + cosine similarity)
├── movies.csv          # Sample dataset (50+ movies)
├── requirements.txt
└── README.md
```

## Setup & run

```bash
# 1. (optional) create a virtual environment
python -m venv venv
source venv/bin/activate      # on Windows: venv\Scripts\activate

# 2. install dependencies
pip install -r requirements.txt

# 3. run the app
streamlit run app.py
```

The app opens in your browser at `http://localhost:8501`.

## Features

- **Similar Movies mode**: pick any movie and get the top N most similar titles, with a match-percentage score.
- **Browse by Genre mode**: filter the catalog by genre.
- Adjustable number of recommendations via a sidebar slider.
- Cached model loading (`st.cache_resource`) so the TF-IDF matrix is only built once.

## Extending it

- Swap `movies.csv` for a larger dataset (e.g., the [TMDB 5000 Movies dataset](https://www.kaggle.com/) or [MovieLens](https://grouplens.org/datasets/movielens/)) — just keep the same column names, or adjust `_prepare_data()` in `recommender.py`.
- Add a poster image per movie (e.g., via the TMDB API) and display it with `st.image`.
- Try a different similarity approach: `CountVectorizer` instead of TF-IDF, or add collaborative filtering (e.g., `surprise` library) using user ratings if you have them.
- Add a rating/feedback loop so the recommender learns from what users click.

## Testing the ML logic without Streamlit

```bash
python recommender.py
```

This prints the dataset size and a sample recommendation list for "Inception" directly in the terminal — useful for verifying the model works before touching the UI.
