
# Music Recommendation Project

This project explores unsupervised machine learning techniques applied to a real-world music dataset spanning songs from 1950 to 2019. As a data scientist at a Series B music start-up, the goal is to build a song recommendation engine from scratch by clustering unlabeled tracks based on their lyrical and continuous audio features. The workflow includes exploratory data analysis, preprocessing, dimensionality reduction, unsupervised modeling, and a final report.

## About

This project uses unsupervised learning to identify patterns in song lyrics and metadata to generate meaningful song clusters. These clusters form the foundation of a recommendation system that groups similar tracks together without relying on labeled training data.

The dataset includes artist information, song metadata, pre-tokenized lyrics, and a set of engineered lyrical features representing thematic content. The project focuses on understanding these features, reducing dimensionality, and applying clustering algorithms to uncover structure in the music space.

Read more about the dataset features in the [features_info.md](docs/features_info.md) file.


## Project Structure

```
music_recommendation_ml/
│
├── code/
│   ├── eda.ipynb
│   ├── transform.ipynb
│   ├── model.ipynb
│
├── data/
│   ├── recommend.csv
│   ├── train.csv
│
├── docs/
│   ├── features_info.md
│
├── README.md
├── .gitignore
└── .DS_Store
```

### Notebook 1 — EDA (Hypothesis Formulation)
Univariate, bivariate, and multivariate exploration of the dataset.  
Key findings:
- Hip hop is a strong lyrical outlier — its mean obscene score (r=0.41) is roughly 4–6x higher than every other genre, which all fall between 0.06 and 0.14. This matters for clustering because obscene has by far the highest variance across genre group means, meaning it's the single most powerful feature for separating songs. In practice, this likely means KMeans will carve out a dedicated "hip hop cluster" almost automatically, driven almost entirely by this one feature rather than a combination of features.
- `topic` column is derived directly from lyrical scores, making it redundant
- No feature pairs exceed r=0.5, so no features were dropped for correlation
- Genre composition shifted by decade — hip hop absent before 1990s

We hypothesize that K‑Means will identify approximately four clusters. These clusters likely correspond to the dominant lyrical‑feature patterns we observed:
1. High-obscene → hiphop songs
2. High-sadness → country/pop 
3. Violence → rock/blues
4. World/life → reggae


### Notebook 2 — Transform (Cleaning, Wrangling & Preprocessing)
Data cleaning, feature scaling, and PCA analysis.  
Key decisions:
- Dropped: `Unnamed: 0`, `artist_name`, `track_name`, `lyrics`, `age`, `release_date`, `topic`
- No nulls or duplicates found
- Applied `StandardScaler` to normalize all numeric features
- PCA run for analysis — clustering performed on original scaled features due to low inter-feature correlation



### Notebook 3 — Model (Creation & Evaluation)

EDA-informed 15 features → KMeans → elbow + silhouette
PCA on EDA-informed 15 features → KMeans → elbow + silhouette
Compare, pick the better one, move on