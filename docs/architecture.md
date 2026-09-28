# Architecture

This document gives the structure of the code and the design rules.

## Repository layout

```
reso/
├─ Cargo.toml            # [workspace], shared dependencies and lints
├─ crates/
│  ├─ reso-core/         # domain types, traits
│  ├─ reso-meta/         # enrichment DTOs, clients, engine
│  ├─ reso-player/       # symphonia + cpal playback
│  ├─ reso-local/        # local files
│  ├─ reso-radio/        # Radio Browser
│  └─ reso-audius/       # Audius
└─ apps/
   └─ reso-app/
      ├─ src-tauri/      # workspace member, SQLite, Tauri commands
      ├─ src/            # SolidJS + TypeScript + Tailwind CSS
      └─ package.json
```

Each crate gets `version`, `edition`, `license`, `repository`, and `publish` from
`[workspace.package]`. Each crate sets `[lints] workspace = true`.

The workspace members are `crates/*`. Cargo rejects a member path that does not exist.
When step 5 starts, add `apps/reso-app/src-tauri` to `members`.

## Design rules

- Keep the DTOs in `reso-meta`. Do not put the field names of an API into `reso-core`.
- Keep `reso-core` small. Do not put SQLite, Tauri, or an HTTP client into `reso-core`.
- The enrichment engine uses only the cache trait. Then SQLite can replace the in-memory cache.
- Generate the TypeScript bindings with `tauri-specta`. Put the derive behind the `ts` feature of `reso-core`.
- A playback source is not always a byte stream. Model the sources as `Stream`, `Url`, and `Live`.

## Frontend

- Use `solid-js@2.0.0-rc.10`, which has the npm dist-tag `next`. Pin this exact version.
- Do not use the npm dist-tag `latest`. The tag `latest` points to SolidJS 1.x.
- SolidJS 2 has a different API than SolidJS 1.x. Use the documentation of SolidJS 2.
- Before you add a Solid package, make sure that it supports SolidJS 2. Examples are the router, the Vite plugin, and the test library.

## Playback

```
Frontend (Solid) --commands--> Player (Rust, own threads)
         <--events (position, track, state)--

Player:
  control thread   queue, state, commands
  decode thread    symphonia -> resample -> ring buffer
  cpal callback    ring buffer -> output device (real time, no locks, no allocation)
```

| Task | Crate |
|---|---|
| Decoding | `symphonia` |
| Output | `cpal` |
| Ring buffer | `rtrb` or `ringbuf` |
| Resampling | `rubato` |
| OS media controls | `souvlaki` |
| Tag reading (local files) | `lofty` |

Known problems:

- `symphonia` has no Opus decoder, and some radio streams use Opus. Add `opus` (libopus), or mark these stations as not supported.
- Audius streams are seekable. Use HTTP range requests with a buffer.
- Radio streams are not seekable. Parse the ICY metadata to get the title that plays.
- Plan gapless playback early. Decode the next track ahead into the same ring buffer.
- On Linux, `cpal` needs `libasound2-dev` in CI.
