# Movie Recommendation System

An item-based movie recommender built with Python, pandas and scikit-learn using the MovieLens dataset.

## Overview

This project recommends movies similar to a given movie by comparing how users rated them, using item-based collaborative filtering with cosine similarity.

## Dataset

- Source: MovieLens Latest Small (GroupLens Research)
- Size: 100,836 ratings from 610 users
- Missing values in ratings: none
- Ratings range from 0.5 to 5.0

## Approach

1. Loaded the movies and ratings files and checked their shape and missing values.
2. Explored the distribution of ratings.
3. Kept only movies with at least 50 ratings to avoid unreliable similarities.
4. Built a user-movie rating matrix (606 users x 450 movies).
5. Computed cosine similarity between movies and wrote a `recommend()` function that returns the top N most similar movies.

## Example

Top 5 recommendations for `Toy Story (1995)`:

| Rank | Movie | Similarity |
|---|---|---|
| 1 | Toy Story 2 (1999) | 0.573 |
| 2 | Jurassic Park (1993) | 0.566 |
| 3 | Independence Day (1996) | 0.564 |
| 4 | Star Wars: Episode IV - A New Hope (1977) | 0.557 |
| 5 | Forrest Gump (1994) | 0.547 |

## Key Findings

- The most common rating is 4.0, and the average rating is about 3.5, so users tend to rate movies they like.
- The sequel Toy Story 2 is the closest match, which shows the similarity measure captures real viewing patterns.

## Evaluation

I evaluated the item-based collaborative filtering model using a hold-out approach. For each user with at least 5 liked movies (rating >= 4), 20% of liked movies were hidden, and the model recommended 10 unseen movies. The model was compared with a popularity baseline.

| Method | Precision@10 | Hit rate@10 |
|---|---|---|
| Item-based CF (cosine) | 0.238 | 0.808 |
| Popularity baseline | 0.128 | 0.562 |

Users evaluated: 569 (MovieLens small, movies with 50+ ratings).

## Limitations and Future Work

- The system uses only ratings, not genres or movie content, so some recommendations (for example Forrest Gump) are popular movies rather than true content matches.
- Missing ratings are filled with 0, which can affect similarity; mean-centering or matrix factorization (SVD) could improve results.
- The evaluation is a first estimate: the similarity matrix and popularity baseline were built from the full rating data (including held-out ratings), so results are optimistic. A stricter version would build them from training data only.
- A hybrid model combining genres and ratings could handle new movies better.

## How to Run

1. Open `Movie_Recommendation_System.ipynb` in Google Colab or Jupyter.
2. Install the requirements if needed:
   ```
   pip install pandas scikit-learn matplotlib seaborn
   ```
3. Run all cells. The first cell downloads the dataset automatically.

## Tools

Python, pandas, scikit-learn, matplotlib, seaborn
