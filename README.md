# Open Song Timeline Format — OSTF 3.1.0

**Official specification distribution • 100 GitHub-uploadable files • UTF-8 JSON `.ostf`**

OSTF is a host-neutral interchange format for **song structure, chord progressions, a designated primary melody, lyrics, and optional lightweight multitrack arrangement**. It exchanges musical meaning and adopted note placements among composition tools; it is **not** a DAW session, virtual instrument preset, rendered audio, or universal plugin-project interchange format.

[日本語の説明](README_JA.md) · [Specification (EN)](docs/FORMAT_SPECIFICATION.en.md) · [仕様書 (JA)](docs/FORMAT_SPECIFICATION.ja.md)

## Main publication documents

| Publication | English | 日本語 |
| --- | --- | --- |
| **Normative file format & semantics** | [FORMAT_SPECIFICATION.en.md](docs/FORMAT_SPECIFICATION.en.md) | [FORMAT_SPECIFICATION.ja.md](docs/FORMAT_SPECIFICATION.ja.md) |
| **Full user/implementer manual** | [COMPLETE_MANUAL.en.md](docs/COMPLETE_MANUAL.en.md) | [COMPLETE_MANUAL.ja.md](docs/COMPLETE_MANUAL.ja.md) |
| **All parameter definitions** | [PARAMETER_REFERENCE.en.md](docs/PARAMETER_REFERENCE.en.md) | [PARAMETER_REFERENCE.ja.md](docs/PARAMETER_REFERENCE.ja.md) |
| **Every field → example** | [Complete static coverage](docs/COVERAGE.md) | [76 `.ostf` examples and descriptions](samples/INDEX.md) |

Additional: [3.0 → 3.1 migration](docs/MIGRATION_3_0_TO_3_1.md), [GM1 drum key map](docs/GM1_DRUM_MAP.json), [JSON Schema 3.1](schema/ostf-3.1.0.schema.json), [original 3.0 schema](schema/ostf-3.0.0.schema.json), [license](LICENSE.md), [release decision/limitations](RELEASE_NOTES.md).

## Start with real `.ostf` files

| Need | Working document example |
| --- | --- |
| Minimal song (empty content is valid) | [02_empty_sketch.ostf](samples/02_empty_sketch.ostf) |
| Chord progression only | [03_harmony_only.ostf](samples/03_harmony_only.ostf) |
| Primary melody only | [04_melody_only.ostf](samples/04_melody_only.ostf) |
| Lyrics and their alignment to notes | [20_lyric_alignment.ostf](samples/20_lyric_alignment.ostf) |
| Combined song with multiple parts | [58_complete_workflow.ostf](samples/58_complete_workflow.ostf) |
| GM1 drum targets and grid | [61_gm1_drum_grid.ostf](samples/61_gm1_drum_grid.ostf) |
| Custom MIDI drum routing | [64_custom_drum_mapping.ostf](samples/64_custom_drum_mapping.ostf) |
| Multilingual track labels and multiple kits | [71_multilingual_tracks_and_multiple_drum_kits.ostf](samples/71_multilingual_tracks_and_multiple_drum_kits.ostf) |
| Optional note velocity: melodic/drums | [74](samples/74_velocity_melody_optional.ostf), [75](samples/75_velocity_drum_accents.ostf) |

All 76 examples are **standalone JSON documents with `.ostf` extensions**. The [coverage matrix](docs/COVERAGE.md) locates all 194 canonical declarations, 18 conditional overlays, 53 enum choices, 15 constants, 56 definitions and 37 structural branch locations (static occurrences, not validation results). Three unchanged OSTF 3.0 examples remain under `samples/legacy_3_0/` for reference. The earlier OSTF 2.3 materials remain in their [separate project](https://github.com/yoh-nak/Open-Song-Timeline-Format-2.3).

## Key 3.1 decisions

- A track has a stable ID, original Unicode `name`, order, and optional language-tagged `localizedNames`. Instrument names and kit/slot names can also be localized; automatic translation is out of scope.
- `trackType`: `melodic`, `drum`, `mixed`; `preferredView`: `auto`, `pianoRoll`, `drumGrid`. This is a **display hint**, not a DAW GUI command.
- Global `soundSlots[]` has no fixed count; optional `drumKits[]` and `track.drumKitId` support multiple percussion tracks. `midiMapping` is explicit; legacy `midiNote` alone is not proof of GM1 compatibility.
- A source `instrument` is descriptive. `soundSource` is an inert category hint. Core deliberately excludes Program Change, Bank Select, plugin preset/state, CC, bend, aftertouch, and detailed mixing.
- `tracks[].clips[].notes[].velocity` is an **optional integer 1–127**, for performed melodic or drum notes only. When absent, it stays absent in OSTF; export-time adapters may disclose a fallback. Harmony/chord intervals and the frozen phrase-template note profile have no velocity field.
- `song.primaryMelodyTrackId` points to **at most one** primary melody; other melodies and backing parts are normal arrangement tracks. Lyrics use separate documents/units with explicit alignment to note IDs. No automatic arrangement or voice synthesis happens when loading a file.
- A valid OSTF 3.1 reader also accepts 3.0.0 data without silent rewriting. 3.0-only software need not accept 3.1. Downgrades must disclose lost 3.1 fields.

## Normative source, conformance & implementation

The **3.1 schema** constrains structure; the [specification](docs/FORMAT_SPECIFICATION.en.md) adds semantic rules (IDs/references, tick math, sorted timelines, known profile dispatch, non-destructive preservation of unsupported extension data). Merely passing JSON syntax or a schema cannot certify DAW interoperability.

An **informative** strict JSON/reference reader is bundled as [`ostf3.py`](ostf3.py), with its four versioned schema files. It is a Python library rather than a direct Ableton, MIDI `.mid` writer, or installer; `jsonschema` must be installed separately if a user chooses to run it. The former operation editors, migrations, and adapter CLIs are **not** bundled in this compact 100-file GitHub package. Their normative behavior is described in the specification/manual, and any future implementation is separate from OSTF's interchange contract.

### File/version basics

- Extension `.ostf`, content **UTF-8 strict JSON** (`format: "OSTF"`, root `version: "3.1.0"`), not YAML, not MIDI.
- Concrete note target is **exactly one** of `pitch` or `soundSlotId`; onset and gate are exact integer PPQ ticks. The clip placement span is not a note truncation boundary.
- A Core-only client can ignore supported-optional-profile semantics only if it preserves unsupported extension envelopes without corrupting them; implementations should clearly disclose their capability limits.
- [LICENSE.md](LICENSE.md) describes attribution for the distributed specification/source/examples. Using OSTF does not automatically license the user's music or independently written application code.

## Release declaration

**GO for publication of the specification, complete bilingual manuals and parameter references, schemas and authored examples.** This is a *static documentation/publication decision*. **No schema-validator execution, reference-program tests, MIDI/DAW operation, Max for Live run, or independent interoperability verification was performed at the user's request.** Do not describe any such behavior as verified. See [release notes](RELEASE_NOTES.md).

Unpack and commit these files into a repository root. The distribution contains **exactly 100 files including the manifest**, meeting the requested maximum. GitHub repository creation/push/tag/release are not done by producing this ZIP. Suggested release tag: `v3.1.0`.
