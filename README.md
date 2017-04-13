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
    <td>Recommendations</td>
    <td>3</td>
  </tr>
  <tr>
    <td>Saved</td>
    <td>2</td>
  </tr>
  <tr>
    <td>Playlist</td>
    <td>1</td>
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
