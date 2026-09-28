# Roadmap

This document gives the scope of the MVP and the steps to the MVP.

## MVP scope

| Function | Provider | Tier |
|---|---|---|
| Tags and IDs | MusicBrainz | T1 |
| Covers | Cover Art Archive | T1 |
| Lyrics | LRCLIB | T1 |
| Artist biographies | Wikidata, then Wikipedia | T1 |
| Artist photos | Wikimedia Commons (Wikidata property P18) | T1 |
| Radio | Radio Browser | T1 |
| Similar artists | ListenBrainz (read endpoints only) | T1 |
| Streaming | Audius (`app_name` parameter, no key) | T1 |

The lookup chain starts with the MBID. Then it uses Cover Art Archive, Wikidata,
Wikipedia, Commons, and LRCLIB.

## Steps

| Step | Task | Crate |
|---|---|---|
| 1 | Enrichment DTOs (serde structs, 1:1 with each API) | `reso-meta` |
| 2 | Domain types and traits (`Artist`, `Release`, `Recording`, `ItemRef`, `Source`, `Enricher`, `Playback`) | `reso-core` |
| 3 | Enrichment engine (HTTP client, rate limit, mapping from DTO to domain type) | `reso-meta` |
| 4 | Cache (trait and in-memory implementation) | `reso-core` and `reso-app` |
| 5 | Frontend in Tauri, tray | `reso-app` |
| 6 | SQLite (library schema and enrichment cache, implements the cache trait) | `reso-app` |
| 7 | Playback | `reso-player` |
| 8 | Local files | `reso-local` |
| 9 | Radio | `reso-radio` |
| 10 | Streaming | `reso-audius` |
| 11 | Downloads | `reso-audius` and `reso-app` |

Add a crate only when its step starts.
