# Changelog

All notable changes to this project are documented in this file.

## [Unreleased]

### Added
- `applecatcher_min.basic` — a byte-minimized, functionally equivalent rewrite of the source game for Applesoft BASIC on the Apple II.
- `RENDER HUD` subroutine (line 9500 in `applecatcher_src.basic`, line 129 in `applecatcher_min.basic`) so SCORE/LIVES are drawn immediately at game start and after "Continue", instead of only after the first apple lands.

### Changed
- Renamed `apple_catcher.txt` to `applecatcher_src.basic`.
- Default frame delay `T` changed from `1024` to `16`, making the game start faster.
- Speed-up-per-apple: `T` now decreases by `1` per apple (was `64`), with a floor of `0` (was `128`).

### Fixed
- `applecatcher_min.basic`: title screen no longer fails to clear before gameplay starts (a `HOME` call was dropped when subroutines were merged during minification).
- SCORE/LIVES were previously only printed inside the collision handler, so nothing displayed until the first catch or miss; both `applecatcher_src.basic` and `applecatcher_min.basic` now draw the HUD on init and reset as well.
- The apple spawned/reset on row 1 (`AY = 1`), the same row used by the SCORE/LIVES HUD, so its `"O"` glyph could overwrite HUD text (e.g. once SCORE reached 4 digits). The apple now spawns/resets on row 2 (`AY = 2`) so its fall path never overlaps the HUD row (#3).
