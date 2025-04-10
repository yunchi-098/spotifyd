# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.4.1]

### Fixed
- revert default features to `alsa_backend` ([#1337])
- do not require `bindgen` dependencies on supported systems ([#1340])
- always return exitcode 1 on error ([#1338])
- the released binaries for `linux-x86_64` also work for older systems ([#1342])

[#1337]: https://github.com/Spotifyd/spotifyd/pull/1337
[#1338]: https://github.com/Spotifyd/spotifyd/pull/1338
[#1340]: https://github.com/Spotifyd/spotifyd/pull/1340
[#1342]: https://github.com/Spotifyd/spotifyd/pull/1342

## [0.4.0]

### Breaking
- username and password authentaction have been removed and are replaced by OAuth ([#1321])
  Look at the [docs](https://docs.spotifyd.rs/) for setup instructions.

### Added
- retry enabling discovery several times before exiting ([#1228])
- development artifacts are now available ([#1332])
- prebuilt binaries are available for `aarch64` (both Linux and macOS) ([#1332])
- Windows and Android are now supported ([#1219], [#1314])
- expose pipe and subprocess backends ([#1284])
- new device type options are available ([#1316])
- OAuth login is now supported ([#1321])
- a warning is emitted on unsupported configuration values ([#1327])

### Changed
- the docs have been overhauled to reflect the current state of the project and simplify onboarding ([#1327])
- `librespot` dependency has been updated to 0.6 ([#1317])
- Credential caching has been re-enabled. ([#1214])

### Fixed
- alsa mixer: volume calculation has been fixed ([#1229])

### Removed
- `armv6` binaries are no longer available by default ([#1332])
  If you still need them, please join our matrix channel (https://matrix.to/#/#spotifyd:matrix.org) and tell us!

[#1214]: https://github.com/Spotifyd/spotifyd/pull/1214
[#1229]: https://github.com/Spotifyd/spotifyd/pull/1229
[#1228]: https://github.com/Spotifyd/spotifyd/pull/1228
[#1284]: https://github.com/Spotifyd/spotifyd/pull/1284
[#1219]: https://github.com/Spotifyd/spotifyd/pull/1219
[#1314]: https://github.com/Spotifyd/spotifyd/pull/1314
[#1316]: https://github.com/Spotifyd/spotifyd/pull/1316
[#1317]: https://github.com/Spotifyd/spotifyd/pull/1317
[#1321]: https://github.com/Spotifyd/spotifyd/pull/1321
[#1327]: https://github.com/Spotifyd/spotifyd/pull/1327
[#1332]: https://github.com/Spotifyd/spotifyd/pull/1332

## [0.3.5]

We now have a [project website](https://spotifyd.rs) (thanks @slondr!) and a [matrix room](https://matrix.to/#/#spotifyd:matrix.org).
Feel free to join and ask your questions!

### Added
- `TransferPlayback` D-Bus method to transfer the playback to `spotifyd` ([#1162])
  To host this, a `rs.spotifyd.Controls` interface has been added.
- A `audio_format` option was added to circumvent certain errors ([#1082])
- A setter was added to the `Shuffle` property ([#1188])
- `volume_control = "none"` variant to disable changing the volume in clients ([#750])
### Changed
- Improve backend selection logic, especially for macOS ([#1158])
- Update `keyring` dependency to newest version ([#1174])
- `VolumeUp`, `VolumeDown` D-Bus methods have been copied to spotifyd's controls interface ([#1162])
  Their versions in `org.mpris.MediaPlayer2.Player` have been deprecated and will be removed in a breaking release.
- The `librespot` dependency has been upgraded to the most recent release 🎉 ([#1182], [#1197])
- Many other dependency updates ([#1183], [#1145], [#1199])
- Documentation improvements ([#1156])
- Our minimum supported rust version (MSRV) has been bumped to 1.64 ([#1145])

[#750]: https://github.com/Spotifyd/spotifyd/pull/750
[#1082]: https://github.com/Spotifyd/spotifyd/pull/1082
[#1145]: https://github.com/Spotifyd/spotifyd/pull/1145
[#1156]: https://github.com/Spotifyd/spotifyd/pull/1156
[#1158]: https://github.com/Spotifyd/spotifyd/pull/1158
[#1162]: https://github.com/Spotifyd/spotifyd/pull/1162
[#1174]: https://github.com/Spotifyd/spotifyd/pull/1174
[#1182]: https://github.com/Spotifyd/spotifyd/pull/1182
[#1183]: https://github.com/Spotifyd/spotifyd/pull/1183
[#1188]: https://github.com/Spotifyd/spotifyd/pull/1188
[#1197]: https://github.com/Spotifyd/spotifyd/pull/1197
[#1199]: https://github.com/Spotifyd/spotifyd/pull/1199

## [0.3.4]
### Added 
- Implement the `PropertiesChanged` and `Seeked` events for the MPRIS-interface ([#1025])
- Add `cache_size` configuration option ([#1092])
- Add `dbus_type` configuration option ([#954])
- Added formal documentation of the minimum required Rust version - which is currently 1.62 ([#1127])
### Changed
- Improvements to the documentation ([#894], [#955], [#1030], [#1039], [#1054], [#1055], [#1067])
- Fix cumulating delay in `on_song_change_hook` ([#1059])
- Only enable one of zeroconf discovery and password-authentication at the same time ([#1059])
- Convert mainloop to using `async` / `await` ([#1059])
- Upgrade `rspotify` dependency to `0.11.5` ([#1079])
- Improve error reporting ([#1108])
- Make `spotifyd` bus name unique ([#1100])  
  **Note:** If you were relying on the consistent bus name of `org.mpris.MediaPlayer2.spotifyd`,
  you can adapt your script e.g. by querying the name like `qdbus | grep "org.mpris.MediaPlayer2.spotifyd"`
- Fix wrong handling of credential cache ([#1121])
### Removed
- Replace redundant `reqwest` dependency ([#1120])

[#894]: https://github.com/Spotifyd/spotifyd/pull/894
[#954]: https://github.com/Spotifyd/spotifyd/pull/954
[#955]: https://github.com/Spotifyd/spotifyd/pull/955
[#1025]: https://github.com/Spotifyd/spotifyd/pull/1025
[#1030]: https://github.com/Spotifyd/spotifyd/pull/1030
[#1039]: https://github.com/Spotifyd/spotifyd/pull/1039
[#1054]: https://github.com/Spotifyd/spotifyd/pull/1054
[#1055]: https://github.com/Spotifyd/spotifyd/pull/1055
[#1059]: https://github.com/Spotifyd/spotifyd/pull/1059
[#1067]: https://github.com/Spotifyd/spotifyd/pull/1067
[#1079]: https://github.com/Spotifyd/spotifyd/pull/1079
[#1092]: https://github.com/Spotifyd/spotifyd/pull/1092
[#1100]: https://github.com/Spotifyd/spotifyd/pull/1100
[#1108]: https://github.com/Spotifyd/spotifyd/pull/1108
[#1120]: https://github.com/Spotifyd/spotifyd/pull/1120
[#1121]: https://github.com/Spotifyd/spotifyd/pull/1120

## [0.3.3]
### Added 
- Add `debug_credentials` feature for debugging `BadCredentials` errors [#915]
- Implement `VolumeUp` and `VolumeDown` in the DBUS/MPRIS interface [#963]
- Update librespot to 0.2.0 [#977]
- Rewrite DBUS/MPRIS integration [#977]
### Changed
- Improved panic error message [#925]
### Removed

[#915]: https://github.com/Spotifyd/spotifyd/pull/915
[#925]: https://github.com/Spotifyd/spotifyd/pull/925
[#963]: https://github.com/Spotifyd/spotifyd/pull/963
[#977]: https://github.com/Spotifyd/spotifyd/pull/977

## [0.3.1]
### Added 
- Use eyre for better error reporting [#789]
- Add a contributers file

### Changed
- Change docs from readme to mkdocs [#783]
- Update librespot, thus fixing [#719] [#900]
### Removed

[#789]: https://github.com/Spotifyd/spotifyd/pull/789
[#783]: https://github.com/Spotifyd/spotifyd/pull/783
[#719]: https://github.com/Spotifyd/spotifyd/issues/719
[#900]: https://github.com/Spotifyd/spotifyd/pull/900
## [0.3.0]
### Added
- Added a changelog [#714]
### Changed
- Changed the config format from ini to TOML [#571]

[#571]: https://github.com/Spotifyd/spotifyd/pull/571
[#714]: https://github.com/Spotifyd/spotifyd/pull/714
### Removed

## [0.2.24]

[Unreleased]: https://github.com/Spotifyd/spotifyd/compare/v0.4.1...HEAD
[0.4.1]: https://github.com/Spotifyd/spotifyd/releases/tag/v0.4.1
[0.4.0]: https://github.com/Spotifyd/spotifyd/releases/tag/v0.4.0
[0.3.5]: https://github.com/Spotifyd/spotifyd/releases/tag/v0.3.5
[0.3.4]: https://github.com/Spotifyd/spotifyd/releases/tag/v0.3.4
[0.3.3]: https://github.com/Spotifyd/spotifyd/releases/tag/v0.3.3
[0.3.1]: https://github.com/Spotifyd/spotifyd/releases/tag/v0.3.1
[0.3.0]: https://github.com/Spotifyd/spotifyd/releases/tag/v0.3.0
[0.2.24]: https://github.com/Spotifyd/spotifyd/releases/tag/v0.2.24
