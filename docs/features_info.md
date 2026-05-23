# Dataset Features

## Song Metadata
- **artist_name** — The name of the artist.
- **track_name** — The name of the song.
- **release_date** — When the song was released.
- **genre** — The categorical genre of the song.
- **lyrics** — The pre-tokenized lyrics of the song. Note: real-world lyrical content may be obscene.
- **len** — The number of words in the lyrics.
- **topic** — The categorical label of lyrical content.
- **age** — A score from 0 to 1 expressing how “old” a song is (1 = oldest, 0 = newest).

## Lyrical Feature Scores (0–1)
Each feature represents the likelihood that the song’s lyrics relate to a specific theme.

- **dating** — Likelihood the lyrics relate to dating.
- **violence** — Likelihood the lyrics relate to violence.
- **world/life** — Likelihood the lyrics relate to the world or life in general.
- **night/time** — Likelihood the lyrics relate to nightlife or time.
- **shake_the_audience** — Likelihood the lyrics aim to provoke or excite.
- **family/gospel** — Likelihood the lyrics relate to family themes or gospel.
- **romantic** — Likelihood the lyrics relate to romantic feelings.
- **communication** — Likelihood the lyrics relate to communication (romantic or otherwise).
- **obscene** — Likelihood the lyrics relate to obscene or explicit content (money, lifestyle, etc.).
- **music** — Likelihood the lyrics relate to music itself.
- **movement/places** — Likelihood the lyrics relate to movement or locations.
- **light/visual_perceptions** — Likelihood the lyrics relate to the sun or weather-related imagery.
- **family/spiritual** — Likelihood the lyrics relate to family importance or spirituality.
- **sadness** — Likelihood the lyrics relate to sadness.
- **feelings** — Likelihood the lyrics relate to emotions, positive or negative.
