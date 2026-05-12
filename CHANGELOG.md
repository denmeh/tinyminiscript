# Changelog

All notable changes to tinyminiscript will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [Unreleased]

---

## [0.0.7] - 2026-05-12

### Added
- Allow bare miniscript expression parsing (without a descriptor wrapper)

### Fixed
- Memory OOM in `parse_internal` (#51)
- Script generation of `wpkh` descriptors

---

## [0.0.6] - 2025-10-21

### Changed
- Refactored public API for a cleaner consumer-facing surface
- `Context` is now exposed directly instead of `ParserContext`
- Removed lifetime parameter from `Context` struct (#50)

---

## [0.0.5] - 2025-10-17

### Added
- Bare `pk` descriptor support (#47)
- AFL.rs fuzzing harness with auto-resume script (#46)
- Helper script to inspect AFL crash artifacts
- `script` fuzz target

### Changed
- Removed `ast-printer` feature (was an opt-in compile-time feature)
- Reduced parser binary size
- Removed miniscript fuzz filter

### Fixed
- Invalid x-only key accepted in `tr` descriptor (#49)
- Missing error limits on `sh(wsh(*))` descriptors (#48)
- Invalid checksum not rejected (#45)
- Expected comma in `thresh` not enforced (#44)
- `AndB` fragment property `N` incorrectly computed (#42)
- Memory leak in parser
- Satisfaction edge cases
- `OP_EQUALVERIFY` optimization (#41)
- Taproot keys must be 66 or 130 hex digits (#40)
- Taproot scripts not parsed correctly (#31)
- `thresh` with only one key accepted (#39)
- `pkh` descriptor missing `OP_CHECKSIG` (#38)
- Identity `j` wrapper incorrectly handled (#37)
- Identity `n` incorrectly reported in fuzz script (#36)

---

## [0.0.4] - 2025-09-15

### Added
- Extended keys support (xpub/xprv derivation paths) (#17)
- `multi` and `multi_a` fragment support (#20)
- Checksum computation for descriptors (#23)
- Method to serialize the descriptor back to string (#21)
- Address builder utility
- Method to iterate over all keys in a descriptor
- `iterate_keys` now covers `Multi`/`Multi_a` fragments
- `derive` on keys via `Context` (#19)
- `PkH` variant added to key iterators and `derive`
- `Feature-gate` satisfaction behind `satisfy` feature
- `ast-printer` as an opt-in feature (replaces always-on)
- `MaxWitnessScriptSizeExceeded` validation check (#35)
- `MaxRecursiveDepthExceeded` guard (#14)
- Non-ASCII input rejection (#32)
- Non-top-level type checking
- Additional utility methods on descriptors

### Changed
- Refactored `keys.rs` with performance improvements
- Refactored parser internals for clarity and performance
- Errors are no longer serialized; descriptors are now directly exposed
- Relaxed trait bounds on `PublicKeyTrait` (#22)
- `is_wrapped` helper corrected

### Fixed
- `single-sig` descriptors not parsed correctly (#16)
- Parsing invalid hex strings (#34)
- Threshold number parsing (#33)
- Unexpected `NonZeroZero` error (#30)
- Absolute locktime limits not enforced (#29)
- Invalid descriptor `older(+1)` accepted (#27)
- Valid descriptor rejected for `UnexpectedTrailingToken` (#26)
- Fragment `dvu:0` incorrectly represented (#24)
- Fragment `x` must represent `z` (consume zero stack elements) (#15)
- Number must start with digit `1-9` (#18)
- Stack overflow on deeply nested expressions (#3)
- Fix `#11`, `#12`, `#13` — various parsing edge cases
- `MultiColon` parsing error
- `swap` fragment wrapping something that doesn't take exactly one input
- `N` identity must not be a top-level fragment
- `j:` wrapper around a fragment that may be satisfied by zero-size input
- Top-level `V` identity fragment incorrectly accepted
- `sh(0)` parsing (was falling into `tr(0)` branch)
- Invalid fragment identities
- `Parsing must start with a descriptor` guard added
- Unexpected trailing token after valid descriptor (#26)
- Key downcasting (#22)

---

## [0.0.3] - 2025-08-26

> Pre-release development phase. No formal version tag; covers work from project rename through initial fuzzing infrastructure.

### Added
- Fuzzing target comparing output against `rust-miniscript` (#4)
- Nix flake for reproducible builds
- Miniscript satisfaction engine
- `alloc` and `debug` feature flags
- Documentation pass across public API
- AST printer (`ast_printer`)
- Arena-based (flat) AST representation — eliminated tree recursion
- Correctness Properties validation for type checker
- Identity fragments support
- Better error system with source positions
- Bitcoin script generation from AST
- Translator to produce stringified Bitcoin script

### Changed
- Project renamed from `f-miniscript` / `miniscript-rs` to `tinyminiscript`
- `satisfy` function reduced from 30 KB to 22 KB binary footprint
- `Vec16`/`Vec256` replaced with `Vec<const N: usize>` const-generic arrays
- `FRAGMENT_BUFFER_SIZE` now has a default of 256
- `NodeVisitor` now returns a `Result`
- `Fragment` enum refactored to use enum-variant structs
- `Position` type made `Copy`
- Parser heap allocations reduced from 42 KB → 34 KB → 27 KB binary size
- Type checker switched to bit-flags (from enums), reducing binary from 57 KB to 42 KB

### Fixed
- Lexer integer/boolean parsing
- `swap` fragment parsing
- Various parser correctness fixes surfaced by fuzzing

---

## [0.0.1] - 2025-07-30

### Added
- Initial project scaffolding (`tinyminiscript`)
- Lexer with position tracking
- Recursive-descent parser skeleton
- Parsing of basic fragments and key-check fragments
- Parsing of `older`, `after`, hash fragments
- Parsing of logic fragments: `andor`, `and_v`, `and_b`, `and_n`, `or_b`, `or_c`, `or_d`, `or_i`
- Parsing of `thresh` and `multi`/`multi_a` fragments

[Unreleased]: https://github.com/unldenis/tinyminiscript/compare/v0.0.7...HEAD
[0.0.7]: https://github.com/unldenis/tinyminiscript/compare/v0.0.6...v0.0.7
[0.0.6]: https://github.com/unldenis/tinyminiscript/compare/v0.0.5...v0.0.6
[0.0.5]: https://github.com/unldenis/tinyminiscript/compare/v0.0.4...v0.0.5
[0.0.4]: https://github.com/unldenis/tinyminiscript/compare/v0.0.3...v0.0.4
[0.0.3]: https://github.com/unldenis/tinyminiscript/compare/v0.0.1...v0.0.3
[0.0.1]: https://github.com/unldenis/tinyminiscript/releases/tag/v0.0.1
