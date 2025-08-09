**🛍️ Movie Recommendation System (MovieLens 100K)**

This repository contains a complete end-to-end Movie Recommendation System implemented for the Elevvo Internship — Task 5.

It includes:

User-based collaborative filtering (cosine similarity)

Item-based collaborative filtering (bonus)

Matrix factorization via SVD (bonus)

Leave-one-out evaluation with Precision@K

Colab-ready pipeline to download MovieLens 100K from Kaggle using your kaggle.json

🔗 Files included

Movie_Recommendation_Notebook.ipynb — Jupyter notebook with full pipeline (data download + preprocessing + models + evaluation + plots)

movie_recommender_full.py — standalone script (same logic as notebook)

requirements.txt — Python dependencies

README.md — this file

outputs/ — example outputs (generated after running): diagnostic plots and example_recommendations.csv

⚙️ Quick start (Google Colab)

Open a new Colab notebook.

Upload your kaggle.json (Kaggle API token) using the file upload widget in Colab.

Run the Colab-ready cell (provided in the notebook) which will:

place kaggle.json in ~/.kaggle with correct permissions

download MovieLens 100K from Kaggle

unzip the dataset

run the full recommendation pipeline and save outputs to ./outputs/

Important: If the Kaggle download returns a 403 Forbidden, open the dataset page on Kaggle and Accept the dataset license first:
https://www.kaggle.com/datasets/grouplens/movielens-100k

🧩 How the pipeline works

Data loading — reads u.data and u.item after unzip and merges ratings with movie titles.

Train/Test split — leave-one-out: for each user with 2+ ratings we hold out one rating for evaluation.

User-Item matrix — pivot table with user_id rows and movie_id columns (NaN for unseen).

User-based CF — compute user–user cosine similarity (on demeaned ratings), predict unseen ratings with weighted average of neighbors.

Item-based CF (bonus) — item–item cosine similarity, predict by aggregating similar items a user rated.

SVD (bonus) — impute missing with user mean, apply truncated SVD (via scipy.svds) and reconstruct predicted ratings.

Evaluation — Precision@K using the held-out test pairs.

Outputs — saves example recommendations CSV and diagnostic plots to ./outputs/.


📌 Notes & Tips

For quick testing reduce n_neighbors and SVD components; for final runs use larger settings.

If Kaggle download fails, you can manually download the zip from Kaggle and upload it to ./data/.

Evaluation uses a simple leave-one-out Precision@K; you can expand to NDCG, MAP, or train/test splits.
