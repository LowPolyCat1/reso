# reso

reso is a desktop music player. It plays local files, internet radio, and one
streaming provider. It gets metadata for the music from open data providers.

reso is in early development. The app has no functions at this time.

## Stack

- Tauri, Rust, and SQLite
- SolidJS 2 (`solid-js@2.0.0-rc.10`), TypeScript, and Tailwind CSS
- Playback in Rust with `symphonia` and `cpal`

## Providers

reso uses only official, open APIs:

- MusicBrainz
- Cover Art Archive
- LRCLIB
- Wikidata, Wikipedia, and Wikimedia Commons
- Radio Browser
- ListenBrainz
- Audius

reso does not extract streams and does not bypass DRM.

## Layout

```
reso/
├─ Cargo.toml     # workspace, shared dependencies and lints
├─ crates/        # library crates (reso-core, reso-meta, reso-player, and others)
└─ apps/
   └─ reso-app/   # Tauri app (src-tauri and the SolidJS frontend)
```

Each crate starts with its step of the roadmap.

## Documents

- [Architecture](docs/architecture.md)
- [Roadmap](docs/roadmap.md)
- [Decisions](docs/decisions.md)
- [Provider rules](docs/provider-rules.md)

## License

You can use reso under one of these licenses:

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE))
- MIT License ([LICENSE-MIT](LICENSE-MIT))

Unless you explicitly state otherwise, any contribution intentionally
submitted for inclusion in the work by you, as defined in the Apache-2.0
license, shall be dual licensed as above, without any additional terms or
conditions.
