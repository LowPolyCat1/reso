# Decisions

This document records the decisions for reso. It also lists the open decisions.

## Made decisions

1. reso uses only official, open APIs. reso does not extract streams and does not bypass DRM.
   This rule prevents DMCA risk.
2. reso prefers providers of tier T1. A T1 provider is free and needs no key and no login.
3. The code is in one repository, `lowpolycat1/reso`, as one Cargo workspace.
4. Playback runs in Rust with `symphonia` and `cpal`. The webview `<audio>` element stops
   when the window closes. The app must also play from the tray.
5. The license is `MIT OR Apache-2.0`.
6. The tool for TypeScript bindings is `tauri-specta`. Before step 2, examine its release
   status.

## Open decisions

1. Commercial use: is the app free and non-commercial? This decision is not made. It
   changes the terms of later T2 providers, for example AcoustID, Last.fm, and Jamendo.
