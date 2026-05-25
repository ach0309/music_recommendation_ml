Project: Music Recommendation ML Algorithm\
Submitted on: May 24, 2026


### QUESTIONS & ANSWERS


**Q1. Which insights did you gain from your EDA? Were any columns highly correlated? If so, name them.**
From EDA, I found that there are 24 columns and 28362 songs. This dataset is dominated by 4 genres: Pop, Hiphop, Rock, and Country. Hiphop is a strong lyrical outlier, its mean `obscene` score (r=0.41) and is roughly 4–6x higher than every other genre, which all fall between 0.06 and 0.14. This matters for clustering because `obscene` has by far the highest variance across genre group means, meaning it's the single most powerful feature for separating songs. 

There are also shifts that happens between decades. Hiphop is absent before 1990s, Pop and Rock dominate earlier decades, etc. This temporal skew also means the age feature is not independent it encodes genre-era information implicitly.

No feature pair exceeded an absolute Pearson correlation of 0.50. Although no lyrical features were dropped purely for correlation reasons, plotting mean lyrical feature scores by `topic` revealed that each topic label corresponds to whichever lyrical dimension scored highest for that song. 


**Q2. How did you determine which columns to drop or keep? If your EDA informed this process, explain which insights you used to determine which columns were not needed.**

Standardization is dependent on which insights we like to capture. I decided to drop `len` because it has a different scale than lyrical features and ultimately measures song length rather than lyrical content (which is the goal of the project). Here are the other columns that were dropped and their reasoning:
Unnamed: 0   - not informative, likely row index
`artist_name`  - identifier
`track_name`   - identifier
`lyrics`       - raw text
`age`          - confirmed redundant with release_date
`release_date` - could cause clusters to reflect era not lyrical content
`topic`        - derived directly from lyrical scores

The EDA-Informed features consisted of 15 lyrical columns. 
I also did PCA to try and see if it can produce components that can provide a better k value than the raw EDA-Informed columns.

**Q3. What was the optimal number of clusters in your cluster model? Explain how you determined this value.**
I did two evaluation methods on both datasets(Raw and PCA-Reduced) to identify the optimal K for the KMeans model:
1. Elbow Method
EDA-Informed(Raw) flattens out around K=6 or K=7.
PCA-Reduced has more defined elbow at K=7.

Both EDA-Informed(Raw) and PCA-Reduced features dropped steeply from K=2 to K=6 and after K=7, the inertia barely moves in smaller quantities.

2. Silhouette Method
PCA-reduced features silhouette scores consistently beats EDA-Informed features. It removed enough noise making the clusters tighter and separated better.

The silhouette scores peaked at K = 7 with score = 0.4338, confirming that 7 clusters produce the most cohesive and well-separated groupings.


**Q4. Take a look at the respective songs that fell into your clusters. Describe these clusters in human terms to the best of your ability using the columns in your dataset (for example high-gospel songs, low-gospel songs, etc). Feel free to listen to these songs as well to get a sense of what nuance your algorithm picked up on.**

Here's what I found: 

| Cluster # | Name | Dominant Feature | Description |
|-----------|------|-----------------|-------------|
| 1 | Dark & Aggressive | violence | High violence, low romantic and low gospel. Aggressive and confrontational lyrics. |
| 2 | Romantic Ballads | romantic | High romantic, high dating, low violence and low obscene. Love songs focused on relationships.|
| 3 | Spiritual & Gospel | family/gospel | High gospel, high family/spiritual, low violence and low obscene. Faith and family-centered songs. Skews older (1950s–1970s). |
| 4 | Party & Nightlife | night/time | High night/time, high shake the audience, low sadness. High-energy songs about nightlife and dancing. Common in pop and dance. |
| 5 | Philosophical | world/life | High world/life, reflective songs about society and existence. |
| 6 | Melancholic | sadness | High sadness, high feelings, low obscene and low violence. Songs about heartbreak and loss. Common in blues and country. |
| 7 | Everyday Life | movement/places | High movement/places, moderate communication, balanced across all other features. Songs about journeys and daily experience. |



**Q5. Take a look at the clusters that your algorithm assigned to your test samples. Based on these clusters, which songs would you recommend to this user?**

I saved these recommendations under recommendations.csv
The user's top 3 dominant clusters based on the dataset are:
- **Dark & Aggressive** (3 songs), 
- **Melancholic** (2 songs), and 
- **Reflective / Philosophical** (2 songs). 

Based on this taste profile, these are the songs the model helped recommend:

| Artist | Song | Genre | Cluster |
|--------|------|-------|---------|
| Sizzla | No White God | Reggae | Dark & Aggressive |
| Rush | Losing It | Rock | Dark & Aggressive |
| Dr. Feelgood | Milk and Alcohol | Blues | Dark & Aggressive |
| Joey Alexander | Draw Me Nearer | Jazz | Dark & Aggressive |
| Mercyful Fate | Evil | Rock | Dark & Aggressive |
| UNKLE | Unreal | Jazz | Reflective / Philosophical |
| The Raconteurs | What's Yours is Mine | Blues | Reflective / Philosophical |
| The Doors | End of the Night | Rock | Reflective / Philosophical |
| Bobby Bare | When I'm Gone | Country | Reflective / Philosophical |
| Ray Charles | The Right Time | Blues | Reflective / Philosophical |
| The Youngbloods | Beautiful | Country | Melancholic |
| The Cramps | Lonesome Town | Blues | Melancholic |
| Hank Thompson | I Was the First One | Country | Melancholic |
| John Coltrane | All or Nothing at All | Jazz | Melancholic |
| Ricky Van Shelton | From a Jack to a King | Country | Melancholic |