# SpotifyCollector

### Types
```typescript
enum TrackSource {
  Playlist
  Saved
  Recommended
  History
  Manual
}

interface BaseTrack {
  id: string
  name: string
  uri: string
  genres: string[]
}

interface AnalyzedTrack {
  popularity: float
  danceability: float
  duration_ms: float
  energy: float
  tempo: float
  valence: float
  acousticness: float
}

interface Track extends BaseTrack, AnalyzedTrack {}


interface UserTrack {
  source: TrackSource
  track: Track
}

interface WeightedTrack extends UserTrack {
  weight: float;
}
```

#### Track weights

<table>
  <thead>
    <th>source</th>
    <th>weight</th>
  </thead>
  <tr>
    <td>Manual</td>
    <td>5</td>
  </tr>
  <tr>
    <td>User Spotify recommandation tracks</td>
    <td>Recommendations</td>
  </tr>
  <tr>
    <td>User saved tracks</td>
    <td>Saved</td>
  </tr>
  <tr>
    <td>User's playlist tracks</td>
    <td>Playlist</td>
  </tr>
</table>

### Fetcher
```typescript
UserPlaylistTracks(accessToken): UserTrack[]
UserSavedTracks(accessToken): UserTrack[]
UserHistoryTracks(accessToken): UserTrack[]
UserRecommendedTracks(accessToken): UserTrack[]
```

### Transformers
```typescript
UserUniqTracks(UserTrack[]): Set<UserTrack>
UserWeightedTracks(UserTrack[] | Set<UserTrack>): Set<WeightedTrack>
```
