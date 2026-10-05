# DSA 4060 – Week 3 Lab: Building a Simple Content-Based Recommender

**Student ID:** 671463
**Course:** DSA 4060 – Recommender Systems, United States International University-Africa

## Overview

This project builds a simple content-based movie recommender using structured genre features. The workflow is:

```
Movie Features → User Preferences → Recommendation Scores → Top Recommendations
```

Movies are described by five binary genre features (Action, Comedy, Drama, Romance, SciFi). A user's ratings are used to weight those features into a user profile. Every movie is then scored against that profile, movies the user has already watched are removed, and the highest-scoring movies are returned as Top-N recommendations.

## Repository Contents

```
DSA4060-Week3-StudentID/
├── content_based_lab.ipynb
├── movies.csv
└── README.md
```

| File | Description |
|------|-------------|
| `content_based_lab.ipynb` | Notebook with the full workflow, interpretation and limitations |
| `movies.csv` | Movie dataset (10 original movies plus my unique movie, *Silent Orbit*) |
| `README.md` | This file |

## How to Run

1. Install the requirements:
```
   pip install pandas ipykernel
```
2. Open `content_based_lab.ipynb` in VS Code or Jupyter.
3. Select a Python kernel.
4. Choose **Restart → Run All**.

## Method

1. **Item profiles:** each movie is a row of 1s and 0s across five genres.
2. **User ratings:** each user rates a few movies.
3. **Weighting:** each rated movie's genre vector is multiplied by its rating.
4. **User profile:** the weighted vectors are summed, then normalized so the scores add up to 1.
5. **Scoring:** each movie's score is the sum of the user's profile values for the genres it has.
6. **Filtering and ranking:** watched movies are removed and the rest are sorted by score.
7. **Reusable function:** `recommend_movies(movies, ratings, features, n)` runs the whole pipeline.

## Users Tested

| User | Profile (strongest genres) | Top recommendation |
|------|---------------------------|--------------------|
| User A | Action 0.50, SciFi 0.357 | Space Warriors (0.857) |
| User B | Romance 0.4375, Drama 0.3125 | Hidden Truth / City Detectives (0.3125) |
| User C | Action 0.5, SciFi 0.5 (one rating only) | Future World / Space Warriors (1.0) |
| Hans (my user) | Drama 0.417, Action 0.375 | Silent Orbit (0.583) |

## My Unique Movie

**Silent Orbit** (movie_id 11): Drama = 1, SciFi = 1, all other genres 0.

## Key Findings

- Different users get different recommendations because their ratings produce different profiles.
- Two users who watched the same movies but rated them differently get different scores and rankings, because ratings act as weights.
- A user with a single rating (User C) gets a very narrow profile and tied scores.

## Limitations

- Only five genre features are used.
- Actors, directors, release year, language and descriptions are ignored.
- Recommendations can be too similar to what the user already liked.
- New users with little or no history get weak recommendations (cold start).
- Low ratings still add positive weight to a genre, since there is no negative signal.
- Poor metadata gives poor recommendations.
