---
name: Play music and podcasts with MixerBox OnePlayer
description: Find playlists by genre/mood, search for a track, and browse or search podcasts using MixerBox OnePlayer.
api: openapi/mixerbox-oneplayer-openapi-original.json
operations: [getPlaylistByType, searchMusic, getPodcastsByCategory, searchPodcast]
method: generated
generated: '2026-07-20'
---

# Play music and podcasts with MixerBox OnePlayer

MixerBox OnePlayer serves music, podcasts and videos. No authentication is required (`auth: none`). Base URL `https://www.mbplayer.com`. Results come back nested under `{ gpt: { items: [...] } }`.

## Steps

1. **Browse playlists by mood/genre** — call `getPlaylistByType` (`GET /gpt/getPlaylists`) with `locale` (`en-us` | `zh-tw` | `ja-jp`) and a `type` such as `pop`, `hiphop`, `kpop`, `jazz`, `workout`, `chill`, `focus`, `sleep`, `party`. Return the playlist `title`, `url` and `thumbnail` items.
2. **Search a specific track** — call `searchMusic` (`GET /gpt/searchMusic`) with `q` set to the track/artist name; surface the returned `MusicItem` `url`s for streaming.
3. **Browse podcasts by category** — call `getPodcastsByCategory` (`GET /gpt/getPodcastsByCategory`) with `locale` and a numeric `categoryId` (e.g. `1310` music, `1303` comedy, `1489` news, `1304` education).
4. **Search a specific podcast** — call `searchPodcast` (`GET /gpt/searchPodcast`) with `q` set to the podcast name.

## Rules

- Pass `locale` on every localized call; default to `en-us` when the user's language is unknown.
- These are read-only GETs; no idempotency or write concerns apply.
- Present the `url` fields as playable links; do not fabricate stream URLs not returned by the API.
