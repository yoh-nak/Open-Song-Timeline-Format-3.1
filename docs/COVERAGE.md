# OSTF 3.1.0 — Complete static parameter-to-`.ostf` example coverage / 全項目対応表

**Status: static document inventory, not a validator pass / 静的な所在表であり動作検証の合格結果ではありません。**

Source: [`ostf-3.1.0.schema.json`](../schema/ostf-3.1.0.schema.json). The table maps every finite named field, enum choice, constant, definition and principal schema branch to one of **76 standalone UTF-8 JSON `.ostf` samples**. Every coverage claim means *an occurrence exists in the source text*. It does NOT certify schema validity, conditional predicate satisfaction, timing correctness, interoperability or any runtime behavior. Opaque vendor `extensions.data` is intentionally unbounded.

| Static inventory | Declared | Example occurrence |
| --- | ---: | ---: |
| Canonical parameter declarations | 194 | 194 |
| Conditional property overlays | 18 | 18 |
| Enumeration values | 53 | 53 |
| Constants | 15 | 15 |
| Named schema definitions | 56 | 56 |
| Structural branches | 37 | 37 |

The following tables use JSON Schema pointers. **Example** links open the actual standalone `.ostf`; `At` gives a JSON Pointer into that file. All samples remain complete individual documents, not fragments.

## Canonical parameter declarations / 全パラメーター

| # | Schema declaration / value | Example `.ostf` | At (JSON pointer) |
| ---: | --- | --- | --- |
| 1 | `#/$defs/ref/properties/type` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/appearance/objectColors/0/target/type` |
| 2 | `#/$defs/ref/properties/id` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/appearance/objectColors/0/target/id` |
| 3 | `#/$defs/range/properties/start` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/targetRange/start` |
| 4 | `#/$defs/range/properties/duration` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/targetRange/duration` |
| 5 | `#/$defs/spelledPitchClass/properties/step` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/chords/0/root/step` |
| 6 | `#/$defs/spelledPitchClass/properties/alter` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/chords/0/root/alter` |
| 7 | `#/$defs/song/properties/title` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/song/title` |
| 8 | `#/$defs/song/properties/primaryMelodyTrackId` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/song/primaryMelodyTrackId` |
| 9 | `#/$defs/song/properties/localizedTitles` | [71_multilingual_tracks_and_multiple_drum_kits.ostf](../samples/71_multilingual_tracks_and_multiple_drum_kits.ostf) | `/song/localizedTitles` |
| 10 | `#/$defs/section/properties/id` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline/sections/0/id` |
| 11 | `#/$defs/section/properties/name` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline/sections/0/name` |
| 12 | `#/$defs/section/properties/start` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline/sections/0/start` |
| 13 | `#/$defs/section/properties/duration` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline/sections/0/duration` |
| 14 | `#/$defs/section/properties/role` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline/sections/0/role` |
| 15 | `#/$defs/section/properties/localizedNames` | [71_multilingual_tracks_and_multiple_drum_kits.ostf](../samples/71_multilingual_tracks_and_multiple_drum_kits.ostf) | `/timeline/sections/0/localizedNames` |
| 16 | `#/$defs/tempo/properties/at` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline/tempoChanges/0/at` |
| 17 | `#/$defs/tempo/properties/bpm` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline/tempoChanges/0/bpm` |
| 18 | `#/$defs/meter/properties/at` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline/meterChanges/0/at` |
| 19 | `#/$defs/meter/properties/numerator` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline/meterChanges/0/numerator` |
| 20 | `#/$defs/meter/properties/denominator` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline/meterChanges/0/denominator` |
| 21 | `#/$defs/timeline/properties/sections` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline/sections` |
| 22 | `#/$defs/timeline/properties/tempoChanges` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline/tempoChanges` |
| 23 | `#/$defs/timeline/properties/meterChanges` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline/meterChanges` |
| 24 | `#/$defs/chord/properties/id` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/chords/0/id` |
| 25 | `#/$defs/chord/properties/start` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/chords/0/start` |
| 26 | `#/$defs/chord/properties/duration` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/chords/0/duration` |
| 27 | `#/$defs/chord/properties/label` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/chords/0/label` |
| 28 | `#/$defs/chord/properties/root` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/chords/0/root` |
| 29 | `#/$defs/chord/properties/intervals` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/chords/0/intervals` |
| 30 | `#/$defs/chord/properties/bass` | [34_all_core_fields.ostf](../samples/34_all_core_fields.ostf) | `/harmony/chords/0/bass` |
| 31 | `#/$defs/scale/properties/id` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/scales/0/id` |
| 32 | `#/$defs/scale/properties/start` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/scales/0/start` |
| 33 | `#/$defs/scale/properties/duration` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/scales/0/duration` |
| 34 | `#/$defs/scale/properties/label` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/scales/0/label` |
| 35 | `#/$defs/scale/properties/tonic` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/scales/0/tonic` |
| 36 | `#/$defs/scale/properties/intervals` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/scales/0/intervals` |
| 37 | `#/$defs/harmony/properties/chords` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/chords` |
| 38 | `#/$defs/harmony/properties/scales` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/scales` |
| 39 | `#/$defs/instrument/properties/name` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/instrument/name` |
| 40 | `#/$defs/instrument/properties/family` | [34_all_core_fields.ostf](../samples/34_all_core_fields.ostf) | `/tracks/0/instrument/family` |
| 41 | `#/$defs/instrument/properties/localizedNames` | [71_multilingual_tracks_and_multiple_drum_kits.ostf](../samples/71_multilingual_tracks_and_multiple_drum_kits.ostf) | `/tracks/0/instrument/localizedNames` |
| 42 | `#/$defs/note/properties/id` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/clips/0/notes/0/id` |
| 43 | `#/$defs/note/properties/start` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/clips/0/notes/0/start` |
| 44 | `#/$defs/note/properties/duration` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/clips/0/notes/0/duration` |
| 45 | `#/$defs/note/properties/pitch` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/clips/0/notes/0/pitch` |
| 46 | `#/$defs/note/properties/soundSlotId` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/3/clips/0/notes/0/soundSlotId` |
| 47 | `#/$defs/note/properties/velocity` | [74_velocity_melody_optional.ostf](../samples/74_velocity_melody_optional.ostf) | `/tracks/0/clips/0/notes/0/velocity` |
| 48 | `#/$defs/clip/properties/id` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/clips/0/id` |
| 49 | `#/$defs/clip/properties/name` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/clips/0/name` |
| 50 | `#/$defs/clip/properties/start` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/clips/0/start` |
| 51 | `#/$defs/clip/properties/duration` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/clips/0/duration` |
| 52 | `#/$defs/clip/properties/enabled` | [10_enabled_states.ostf](../samples/10_enabled_states.ostf) | `/tracks/0/clips/1/enabled` |
| 53 | `#/$defs/clip/properties/notes` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/clips/0/notes` |
| 54 | `#/$defs/clip/properties/localizedNames` | [71_multilingual_tracks_and_multiple_drum_kits.ostf](../samples/71_multilingual_tracks_and_multiple_drum_kits.ostf) | `/tracks/0/clips/0/localizedNames` |
| 55 | `#/$defs/track/properties/id` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/id` |
| 56 | `#/$defs/track/properties/name` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/name` |
| 57 | `#/$defs/track/properties/role` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/role` |
| 58 | `#/$defs/track/properties/instrument` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/instrument` |
| 59 | `#/$defs/track/properties/enabled` | [10_enabled_states.ostf](../samples/10_enabled_states.ostf) | `/tracks/1/enabled` |
| 60 | `#/$defs/track/properties/clips` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/clips` |
| 61 | `#/$defs/track/properties/trackType` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/tracks/0/trackType` |
| 62 | `#/$defs/track/properties/preferredView` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/tracks/0/preferredView` |
| 63 | `#/$defs/track/properties/soundSource` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/tracks/0/soundSource` |
| 64 | `#/$defs/track/properties/localizedNames` | [71_multilingual_tracks_and_multiple_drum_kits.ostf](../samples/71_multilingual_tracks_and_multiple_drum_kits.ostf) | `/tracks/0/localizedNames` |
| 65 | `#/$defs/track/properties/drumKitId` | [71_multilingual_tracks_and_multiple_drum_kits.ostf](../samples/71_multilingual_tracks_and_multiple_drum_kits.ostf) | `/tracks/0/drumKitId` |
| 66 | `#/$defs/soundSlot/properties/id` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/soundSlots/0/id` |
| 67 | `#/$defs/soundSlot/properties/name` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/soundSlots/0/name` |
| 68 | `#/$defs/soundSlot/properties/role` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/soundSlots/0/role` |
| 69 | `#/$defs/soundSlot/properties/midiNote` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/soundSlots/0/midiNote` |
| 70 | `#/$defs/soundSlot/properties/midiMapping` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/soundSlots/0/midiMapping` |
| 71 | `#/$defs/soundSlot/properties/localizedNames` | [71_multilingual_tracks_and_multiple_drum_kits.ostf](../samples/71_multilingual_tracks_and_multiple_drum_kits.ostf) | `/soundSlots/0/localizedNames` |
| 72 | `#/$defs/lyricDocument/properties/id` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/documents/0/id` |
| 73 | `#/$defs/lyricDocument/properties/title` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/documents/0/title` |
| 74 | `#/$defs/lyricDocument/properties/language` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/documents/0/language` |
| 75 | `#/$defs/lyricPhrase/properties/id` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/phrases/0/id` |
| 76 | `#/$defs/lyricPhrase/properties/documentId` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/phrases/0/documentId` |
| 77 | `#/$defs/lyricPhrase/properties/text` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/phrases/0/text` |
| 78 | `#/$defs/lyricPhrase/properties/pronunciation` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/phrases/0/pronunciation` |
| 79 | `#/$defs/lyricPhrase/properties/start` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/phrases/0/start` |
| 80 | `#/$defs/lyricPhrase/properties/duration` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/phrases/0/duration` |
| 81 | `#/$defs/lyricUnit/properties/id` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/units/0/id` |
| 82 | `#/$defs/lyricUnit/properties/phraseId` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/units/0/phraseId` |
| 83 | `#/$defs/lyricUnit/properties/text` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/units/0/text` |
| 84 | `#/$defs/lyricUnit/properties/pronunciation` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/units/0/pronunciation` |
| 85 | `#/$defs/lyricUnit/properties/start` | [34_all_core_fields.ostf](../samples/34_all_core_fields.ostf) | `/lyrics/units/0/start` |
| 86 | `#/$defs/lyricUnit/properties/duration` | [34_all_core_fields.ostf](../samples/34_all_core_fields.ostf) | `/lyrics/units/0/duration` |
| 87 | `#/$defs/lyricAlignment/properties/id` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/alignments/0/id` |
| 88 | `#/$defs/lyricAlignment/properties/unitIds` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/alignments/0/unitIds` |
| 89 | `#/$defs/lyricAlignment/properties/noteIds` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/alignments/0/noteIds` |
| 90 | `#/$defs/lyrics/properties/documents` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/documents` |
| 91 | `#/$defs/lyrics/properties/phrases` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/phrases` |
| 92 | `#/$defs/lyrics/properties/units` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/units` |
| 93 | `#/$defs/lyrics/properties/alignments` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/alignments` |
| 94 | `#/$defs/resource/properties/id` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/resources/0/id` |
| 95 | `#/$defs/resource/properties/kind` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/resources/0/kind` |
| 96 | `#/$defs/resource/properties/uri` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/resources/0/uri` |
| 97 | `#/$defs/resource/properties/name` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/resources/0/name` |
| 98 | `#/$defs/resource/properties/sha256` | [16_generation_context.ostf](../samples/16_generation_context.ostf) | `/resources/0/sha256` |
| 99 | `#/$defs/dependencies/oneOf/0/properties/scope` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/dependencies/scope` |
| 100 | `#/$defs/dependencies/oneOf/1/properties/scope` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/dependencies/scope` |
| 101 | `#/$defs/dependencies/oneOf/1/properties/refs` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/com.example.generator-state.v1/dependencies/refs` |
| 102 | `#/$defs/extension/properties/version` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/version` |
| 103 | `#/$defs/extension/properties/status` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/status` |
| 104 | `#/$defs/extension/properties/dependencies` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/dependencies` |
| 105 | `#/$defs/extension/properties/data` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data` |
| 106 | `#/$defs/relativeAssignment/properties/noteId` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/data/assignments/0/noteId` |
| 107 | `#/$defs/relativeAssignment/properties/basis` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/data/assignments/0/basis` |
| 108 | `#/$defs/relativeAssignment/properties/contextId` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/data/assignments/0/contextId` |
| 109 | `#/$defs/relativeAssignment/properties/anchorPitch` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/data/assignments/0/anchorPitch` |
| 110 | `#/$defs/relativeAssignment/properties/index` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/data/assignments/0/index` |
| 111 | `#/$defs/relativeAssignment/properties/chromaticOffset` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/data/assignments/0/chromaticOffset` |
| 112 | `#/$defs/relativeData/properties/assignments` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/data/assignments` |
| 113 | `#/$defs/generator/properties/id` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/generator/id` |
| 114 | `#/$defs/generator/properties/version` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/generator/version` |
| 115 | `#/$defs/generationInput/properties/role` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/inputs/0/role` |
| 116 | `#/$defs/generationInput/properties/ref` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/inputs/0/ref` |
| 117 | `#/$defs/generationInput/properties/readRange` | [16_generation_context.ostf](../samples/16_generation_context.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/inputs/1/readRange` |
| 118 | `#/$defs/generationProcess/properties/id` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/id` |
| 119 | `#/$defs/generationProcess/properties/generator` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/generator` |
| 120 | `#/$defs/generationProcess/properties/inputs` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/inputs` |
| 121 | `#/$defs/generationProcess/properties/outputs` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/outputs` |
| 122 | `#/$defs/generationProcess/properties/targetRange` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/targetRange` |
| 123 | `#/$defs/generationProcess/properties/protectedNoteIds` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/protectedNoteIds` |
| 124 | `#/$defs/generationProcess/properties/vendorExtension` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/vendorExtension` |
| 125 | `#/$defs/generationData/properties/processes` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes` |
| 126 | `#/$defs/roleDefinition/properties/id` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/roleDefinitions/0/id` |
| 127 | `#/$defs/roleDefinition/properties/name` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/roleDefinitions/0/name` |
| 128 | `#/$defs/roleDefinition/properties/baseRole` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/roleDefinitions/0/baseRole` |
| 129 | `#/$defs/objectColor/properties/target` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/appearance/objectColors/0/target` |
| 130 | `#/$defs/objectColor/properties/color` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/appearance/objectColors/0/color` |
| 131 | `#/$defs/appearanceData/properties/roleDefinitions` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/roleDefinitions` |
| 132 | `#/$defs/appearanceData/properties/sectionRoleAssignments` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/sectionRoleAssignments` |
| 133 | `#/$defs/appearanceData/properties/appearance` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/appearance` |
| 134 | `#/$defs/appearanceData/properties/appearance/properties/roleColors` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/appearance/roleColors` |
| 135 | `#/$defs/appearanceData/properties/appearance/properties/customRoleColors` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/appearance/customRoleColors` |
| 136 | `#/$defs/appearanceData/properties/appearance/properties/objectColors` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/appearance/objectColors` |
| 137 | `#/$defs/legacyData/properties/sourceVersion` | [45_legacy_import_archive.ostf](../samples/45_legacy_import_archive.ostf) | `/extensions/org.ostf.legacy-import.v1/data/sourceVersion` |
| 138 | `#/$defs/legacyData/properties/sourceSha256` | [45_legacy_import_archive.ostf](../samples/45_legacy_import_archive.ostf) | `/extensions/org.ostf.legacy-import.v1/data/sourceSha256` |
| 139 | `#/$defs/legacyData/properties/sourceText` | [45_legacy_import_archive.ostf](../samples/45_legacy_import_archive.ostf) | `/extensions/org.ostf.legacy-import.v1/data/sourceText` |
| 140 | `#/$defs/legacyData/properties/conversionReport` | [45_legacy_import_archive.ostf](../samples/45_legacy_import_archive.ostf) | `/extensions/org.ostf.legacy-import.v1/data/conversionReport` |
| 141 | `#/$defs/extensions/properties/org.ostf.relative-phrase.v1` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1` |
| 142 | `#/$defs/extensions/properties/org.ostf.generation-context.v1` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1` |
| 143 | `#/$defs/extensions/properties/org.ostf.appearance.v1` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1` |
| 144 | `#/$defs/extensions/properties/org.ostf.legacy-import.v1` | [45_legacy_import_archive.ostf](../samples/45_legacy_import_archive.ostf) | `/extensions/org.ostf.legacy-import.v1` |
| 145 | `#/$defs/extensions/properties/org.ostf.phrase-library.v1` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1` |
| 146 | `#/$defs/extensions/properties/org.ostf.clip-choices.v1` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1` |
| 147 | `#/$defs/phraseTemplate/properties/id` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/templates/0/id` |
| 148 | `#/$defs/phraseTemplate/properties/duration` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/templates/0/duration` |
| 149 | `#/$defs/phraseTemplate/properties/notes` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/templates/0/notes` |
| 150 | `#/$defs/phraseTemplate/properties/name` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/templates/0/name` |
| 151 | `#/$defs/phraseNoteMapping/properties/templateNoteId` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/instances/0/noteMap/0/templateNoteId` |
| 152 | `#/$defs/phraseNoteMapping/properties/repeatIndex` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/instances/0/noteMap/0/repeatIndex` |
| 153 | `#/$defs/phraseNoteMapping/properties/noteId` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/instances/0/noteMap/0/noteId` |
| 154 | `#/$defs/phraseInstance/properties/id` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/instances/0/id` |
| 155 | `#/$defs/phraseInstance/properties/templateId` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/instances/0/templateId` |
| 156 | `#/$defs/phraseInstance/properties/clipId` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/instances/0/clipId` |
| 157 | `#/$defs/phraseInstance/properties/repeatCount` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/instances/0/repeatCount` |
| 158 | `#/$defs/phraseInstance/properties/transpose` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/instances/0/transpose` |
| 159 | `#/$defs/phraseInstance/properties/noteMap` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/instances/0/noteMap` |
| 160 | `#/$defs/phraseLibraryData/properties/templates` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/templates` |
| 161 | `#/$defs/phraseLibraryData/properties/instances` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/instances` |
| 162 | `#/$defs/clipCandidate/properties/id` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1/data/groups/0/candidates/0/id` |
| 163 | `#/$defs/clipCandidate/properties/clipIds` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1/data/groups/0/candidates/0/clipIds` |
| 164 | `#/$defs/clipCandidate/properties/name` | [55_choice_empty_candidate.ostf](../samples/55_choice_empty_candidate.ostf) | `/extensions/org.ostf.clip-choices.v1/data/groups/0/candidates/0/name` |
| 165 | `#/$defs/clipChoiceGroup/properties/id` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1/data/groups/0/id` |
| 166 | `#/$defs/clipChoiceGroup/properties/candidates` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1/data/groups/0/candidates` |
| 167 | `#/$defs/clipChoiceGroup/properties/selectedCandidateId` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1/data/groups/0/selectedCandidateId` |
| 168 | `#/$defs/clipChoiceGroup/properties/name` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1/data/groups/0/name` |
| 169 | `#/$defs/clipChoicesData/properties/groups` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1/data/groups` |
| 170 | `#/$defs/midiMapping/properties/standard` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/soundSlots/0/midiMapping/standard` |
| 171 | `#/$defs/midiMapping/properties/note` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/soundSlots/0/midiMapping/note` |
| 172 | `#/$defs/soundSource/properties/kind` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/tracks/0/soundSource/kind` |
| 173 | `#/$defs/soundSource/properties/identifier` | [64_custom_drum_mapping.ostf](../samples/64_custom_drum_mapping.ostf) | `/tracks/0/soundSource/identifier` |
| 174 | `#/$defs/drumKit/properties/id` | [71_multilingual_tracks_and_multiple_drum_kits.ostf](../samples/71_multilingual_tracks_and_multiple_drum_kits.ostf) | `/drumKits/0/id` |
| 175 | `#/$defs/drumKit/properties/name` | [71_multilingual_tracks_and_multiple_drum_kits.ostf](../samples/71_multilingual_tracks_and_multiple_drum_kits.ostf) | `/drumKits/0/name` |
| 176 | `#/$defs/drumKit/properties/localizedNames` | [71_multilingual_tracks_and_multiple_drum_kits.ostf](../samples/71_multilingual_tracks_and_multiple_drum_kits.ostf) | `/drumKits/0/localizedNames` |
| 177 | `#/$defs/drumKit/properties/soundSlotIds` | [71_multilingual_tracks_and_multiple_drum_kits.ostf](../samples/71_multilingual_tracks_and_multiple_drum_kits.ostf) | `/drumKits/0/soundSlotIds` |
| 178 | `#/$defs/phraseSourceNote/properties/id` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/templates/0/notes/0/id` |
| 179 | `#/$defs/phraseSourceNote/properties/start` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/templates/0/notes/0/start` |
| 180 | `#/$defs/phraseSourceNote/properties/duration` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/templates/0/notes/0/duration` |
| 181 | `#/$defs/phraseSourceNote/properties/pitch` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/templates/0/notes/0/pitch` |
| 182 | `#/$defs/phraseSourceNote/properties/soundSlotId` | [23_phrase_percussion.ostf](../samples/23_phrase_percussion.ostf) | `/extensions/org.ostf.phrase-library.v1/data/templates/0/notes/0/soundSlotId` |
| 183 | `#/properties/format` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/format` |
| 184 | `#/properties/version` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/version` |
| 185 | `#/properties/ppq` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/ppq` |
| 186 | `#/properties/song` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/song` |
| 187 | `#/properties/timeline` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline` |
| 188 | `#/properties/harmony` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony` |
| 189 | `#/properties/tracks` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks` |
| 190 | `#/properties/soundSlots` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/soundSlots` |
| 191 | `#/properties/lyrics` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics` |
| 192 | `#/properties/resources` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/resources` |
| 193 | `#/properties/extensions` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions` |
| 194 | `#/properties/drumKits` | [71_multilingual_tracks_and_multiple_drum_kits.ostf](../samples/71_multilingual_tracks_and_multiple_drum_kits.ostf) | `/drumKits` |

## Conditional property overlays / 条件付きプロパティ

| # | Schema declaration / value | Example `.ostf` | At (JSON pointer) |
| ---: | --- | --- | --- |
| 1 | `#/$defs/track/allOf/0/if/properties/trackType` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/tracks/0/trackType` |
| 2 | `#/$defs/relativeAssignment/allOf/0/if/properties/basis` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/data/assignments/0/basis` |
| 3 | `#/$defs/relativeAssignment/allOf/0/then/properties/index` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/data/assignments/0/index` |
| 4 | `#/$defs/extensions/properties/org.ostf.relative-phrase.v1/allOf/1/if/properties/version` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/version` |
| 5 | `#/$defs/extensions/properties/org.ostf.relative-phrase.v1/allOf/1/then/properties/data` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/data` |
| 6 | `#/$defs/extensions/properties/org.ostf.generation-context.v1/allOf/1/if/properties/version` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/version` |
| 7 | `#/$defs/extensions/properties/org.ostf.generation-context.v1/allOf/1/then/properties/data` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data` |
| 8 | `#/$defs/extensions/properties/org.ostf.appearance.v1/allOf/1/if/properties/version` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/version` |
| 9 | `#/$defs/extensions/properties/org.ostf.appearance.v1/allOf/1/then/properties/data` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data` |
| 10 | `#/$defs/extensions/properties/org.ostf.legacy-import.v1/allOf/1/if/properties/version` | [45_legacy_import_archive.ostf](../samples/45_legacy_import_archive.ostf) | `/extensions/org.ostf.legacy-import.v1/version` |
| 11 | `#/$defs/extensions/properties/org.ostf.legacy-import.v1/allOf/1/then/properties/data` | [45_legacy_import_archive.ostf](../samples/45_legacy_import_archive.ostf) | `/extensions/org.ostf.legacy-import.v1/data` |
| 12 | `#/$defs/extensions/properties/org.ostf.phrase-library.v1/allOf/1/if/properties/version` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/version` |
| 13 | `#/$defs/extensions/properties/org.ostf.phrase-library.v1/allOf/1/then/properties/data` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data` |
| 14 | `#/$defs/extensions/properties/org.ostf.clip-choices.v1/allOf/1/if/properties/version` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1/version` |
| 15 | `#/$defs/extensions/properties/org.ostf.clip-choices.v1/allOf/1/then/properties/data` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1/data` |
| 16 | `#/$defs/midiMapping/allOf/0/if/properties/standard` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/soundSlots/0/midiMapping/standard` |
| 17 | `#/$defs/midiMapping/allOf/0/then/properties/note` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/soundSlots/0/midiMapping/note` |
| 18 | `#/$defs/soundSource/allOf/0/if/properties/kind` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/tracks/0/soundSource/kind` |

## Enumeration values / 列挙値

| # | Schema declaration / value | Example `.ostf` | At (JSON pointer) |
| ---: | --- | --- | --- |
| 1 | `#/$defs/ref/properties/type/enum` = `"section"` | [38_dependency_scopes.ostf](../samples/38_dependency_scopes.ostf) | `/extensions/com.example.object-state.v1/dependencies/refs/0/type` |
| 2 | `#/$defs/ref/properties/type/enum` = `"track"` | [38_dependency_scopes.ostf](../samples/38_dependency_scopes.ostf) | `/extensions/com.example.object-state.v1/dependencies/refs/1/type` |
| 3 | `#/$defs/ref/properties/type/enum` = `"clip"` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/appearance/objectColors/0/target/type` |
| 4 | `#/$defs/ref/properties/type/enum` = `"note"` | [17_appearance.ostf](../samples/17_appearance.ostf) | `/extensions/org.ostf.appearance.v1/data/appearance/objectColors/1/target/type` |
| 5 | `#/$defs/ref/properties/type/enum` = `"chord"` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/inputs/0/ref/type` |
| 6 | `#/$defs/ref/properties/type/enum` = `"scale"` | [38_dependency_scopes.ostf](../samples/38_dependency_scopes.ostf) | `/extensions/com.example.object-state.v1/dependencies/refs/5/type` |
| 7 | `#/$defs/ref/properties/type/enum` = `"soundSlot"` | [38_dependency_scopes.ostf](../samples/38_dependency_scopes.ostf) | `/extensions/com.example.object-state.v1/dependencies/refs/6/type` |
| 8 | `#/$defs/ref/properties/type/enum` = `"drumKit"` | [71_multilingual_tracks_and_multiple_drum_kits.ostf](../samples/71_multilingual_tracks_and_multiple_drum_kits.ostf) | `/extensions/com.example.kit-notes.v1/dependencies/refs/0/type` |
| 9 | `#/$defs/ref/properties/type/enum` = `"lyricDocument"` | [38_dependency_scopes.ostf](../samples/38_dependency_scopes.ostf) | `/extensions/com.example.object-state.v1/dependencies/refs/7/type` |
| 10 | `#/$defs/ref/properties/type/enum` = `"lyricPhrase"` | [38_dependency_scopes.ostf](../samples/38_dependency_scopes.ostf) | `/extensions/com.example.object-state.v1/dependencies/refs/8/type` |
| 11 | `#/$defs/ref/properties/type/enum` = `"lyricUnit"` | [38_dependency_scopes.ostf](../samples/38_dependency_scopes.ostf) | `/extensions/com.example.object-state.v1/dependencies/refs/9/type` |
| 12 | `#/$defs/ref/properties/type/enum` = `"lyricAlignment"` | [38_dependency_scopes.ostf](../samples/38_dependency_scopes.ostf) | `/extensions/com.example.object-state.v1/dependencies/refs/10/type` |
| 13 | `#/$defs/ref/properties/type/enum` = `"resource"` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/inputs/2/ref/type` |
| 14 | `#/$defs/spelledPitchClass/properties/step/enum` = `"A"` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/chords/1/root/step` |
| 15 | `#/$defs/spelledPitchClass/properties/step/enum` = `"B"` | [35_pitch_class_spellings.ostf](../samples/35_pitch_class_spellings.ostf) | `/harmony/chords/5/bass/step` |
| 16 | `#/$defs/spelledPitchClass/properties/step/enum` = `"C"` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/chords/0/root/step` |
| 17 | `#/$defs/spelledPitchClass/properties/step/enum` = `"D"` | [13_relative_scale.ostf](../samples/13_relative_scale.ostf) | `/harmony/scales/0/tonic/step` |
| 18 | `#/$defs/spelledPitchClass/properties/step/enum` = `"E"` | [34_all_core_fields.ostf](../samples/34_all_core_fields.ostf) | `/harmony/chords/0/bass/step` |
| 19 | `#/$defs/spelledPitchClass/properties/step/enum` = `"F"` | [35_pitch_class_spellings.ostf](../samples/35_pitch_class_spellings.ostf) | `/harmony/chords/25/bass/step` |
| 20 | `#/$defs/spelledPitchClass/properties/step/enum` = `"G"` | [34_all_core_fields.ostf](../samples/34_all_core_fields.ostf) | `/harmony/chords/1/bass/step` |
| 21 | `#/$defs/meter/properties/denominator/enum` = `1` | [36_all_meter_denominators.ostf](../samples/36_all_meter_denominators.ostf) | `/timeline/meterChanges/0/denominator` |
| 22 | `#/$defs/meter/properties/denominator/enum` = `2` | [36_all_meter_denominators.ostf](../samples/36_all_meter_denominators.ostf) | `/timeline/meterChanges/1/denominator` |
| 23 | `#/$defs/meter/properties/denominator/enum` = `4` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline/meterChanges/0/denominator` |
| 24 | `#/$defs/meter/properties/denominator/enum` = `8` | [11_meter_tempo_gaps.ostf](../samples/11_meter_tempo_gaps.ostf) | `/timeline/meterChanges/1/denominator` |
| 25 | `#/$defs/meter/properties/denominator/enum` = `16` | [36_all_meter_denominators.ostf](../samples/36_all_meter_denominators.ostf) | `/timeline/meterChanges/4/denominator` |
| 26 | `#/$defs/meter/properties/denominator/enum` = `32` | [36_all_meter_denominators.ostf](../samples/36_all_meter_denominators.ostf) | `/timeline/meterChanges/5/denominator` |
| 27 | `#/$defs/meter/properties/denominator/enum` = `64` | [36_all_meter_denominators.ostf](../samples/36_all_meter_denominators.ostf) | `/timeline/meterChanges/6/denominator` |
| 28 | `#/$defs/track/properties/trackType/enum` = `"melodic"` | [62_melodic_piano_roll.ostf](../samples/62_melodic_piano_roll.ostf) | `/tracks/0/trackType` |
| 29 | `#/$defs/track/properties/trackType/enum` = `"drum"` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/tracks/0/trackType` |
| 30 | `#/$defs/track/properties/trackType/enum` = `"mixed"` | [63_mixed_track.ostf](../samples/63_mixed_track.ostf) | `/tracks/0/trackType` |
| 31 | `#/$defs/track/properties/preferredView/enum` = `"auto"` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/tracks/0/preferredView` |
| 32 | `#/$defs/track/properties/preferredView/enum` = `"pianoRoll"` | [62_melodic_piano_roll.ostf](../samples/62_melodic_piano_roll.ostf) | `/tracks/0/preferredView` |
| 33 | `#/$defs/track/properties/preferredView/enum` = `"drumGrid"` | [64_custom_drum_mapping.ostf](../samples/64_custom_drum_mapping.ostf) | `/tracks/0/preferredView` |
| 34 | `#/$defs/resource/properties/kind/enum` = `"audio"` | [16_generation_context.ostf](../samples/16_generation_context.ostf) | `/resources/0/kind` |
| 35 | `#/$defs/resource/properties/kind/enum` = `"midi"` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/resources/0/kind` |
| 36 | `#/$defs/resource/properties/kind/enum` = `"text"` | [16_generation_context.ostf](../samples/16_generation_context.ostf) | `/resources/1/kind` |
| 37 | `#/$defs/resource/properties/kind/enum` = `"other"` | [37_resource_kinds.ostf](../samples/37_resource_kinds.ostf) | `/resources/3/kind` |
| 38 | `#/$defs/dependencies/oneOf/0/properties/scope/enum` = `"document"` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/dependencies/scope` |
| 39 | `#/$defs/dependencies/oneOf/0/properties/scope/enum` = `"none"` | [18_opaque_precision.ostf](../samples/18_opaque_precision.ostf) | `/extensions/com.example.precision.v1/dependencies/scope` |
| 40 | `#/$defs/extension/properties/status/enum` = `"current"` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/status` |
| 41 | `#/$defs/extension/properties/status/enum` = `"stale"` | [14_stale_source.ostf](../samples/14_stale_source.ostf) | `/extensions/org.ostf.relative-phrase.v1/status` |
| 42 | `#/$defs/extension/properties/status/enum` = `"unverified"` | [15_unverified_source.ostf](../samples/15_unverified_source.ostf) | `/extensions/org.ostf.relative-phrase.v1/status` |
| 43 | `#/$defs/relativeAssignment/properties/basis/enum` = `"chordTone"` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/data/assignments/0/basis` |
| 44 | `#/$defs/relativeAssignment/properties/basis/enum` = `"scaleDegree"` | [13_relative_scale.ostf](../samples/13_relative_scale.ostf) | `/extensions/org.ostf.relative-phrase.v1/data/assignments/0/basis` |
| 45 | `#/$defs/midiMapping/properties/standard/enum` = `"gm1"` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/soundSlots/0/midiMapping/standard` |
| 46 | `#/$defs/midiMapping/properties/standard/enum` = `"custom"` | [64_custom_drum_mapping.ostf](../samples/64_custom_drum_mapping.ostf) | `/soundSlots/0/midiMapping/standard` |
| 47 | `#/$defs/soundSource/properties/kind/enum` = `"unassigned"` | [68_empty_declared_drum_track.ostf](../samples/68_empty_declared_drum_track.ostf) | `/tracks/0/soundSource/kind` |
| 48 | `#/$defs/soundSource/properties/kind/enum` = `"gm1"` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/tracks/0/soundSource/kind` |
| 49 | `#/$defs/soundSource/properties/kind/enum` = `"externalMidi"` | [70_external_and_host_sources.ostf](../samples/70_external_and_host_sources.ostf) | `/tracks/0/soundSource/kind` |
| 50 | `#/$defs/soundSource/properties/kind/enum` = `"plugin"` | [64_custom_drum_mapping.ostf](../samples/64_custom_drum_mapping.ostf) | `/tracks/0/soundSource/kind` |
| 51 | `#/$defs/soundSource/properties/kind/enum` = `"hostManaged"` | [70_external_and_host_sources.ostf](../samples/70_external_and_host_sources.ostf) | `/tracks/1/soundSource/kind` |
| 52 | `#/$defs/soundSource/allOf/0/if/properties/kind/enum` = `"gm1"` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/tracks/0/soundSource/kind` |
| 53 | `#/$defs/soundSource/allOf/0/if/properties/kind/enum` = `"unassigned"` | [68_empty_declared_drum_track.ostf](../samples/68_empty_declared_drum_track.ostf) | `/tracks/0/soundSource/kind` |

## Constants / 定数

| # | Schema declaration / value | Example `.ostf` | At (JSON pointer) |
| ---: | --- | --- | --- |
| 1 | `#/$defs/chord/properties/intervals/contains/const` = `0` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/chords/0/intervals/0` |
| 2 | `#/$defs/scale/properties/intervals/contains/const` = `0` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/scales/0/intervals/0` |
| 3 | `#/$defs/track/allOf/0/if/properties/trackType/const` = `"melodic"` | [62_melodic_piano_roll.ostf](../samples/62_melodic_piano_roll.ostf) | `/tracks/0/trackType` |
| 4 | `#/$defs/dependencies/oneOf/1/properties/scope/const` = `"objects"` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/com.example.generator-state.v1/dependencies/scope` |
| 5 | `#/$defs/relativeAssignment/allOf/0/if/properties/basis/const` = `"scaleDegree"` | [13_relative_scale.ostf](../samples/13_relative_scale.ostf) | `/extensions/org.ostf.relative-phrase.v1/data/assignments/0/basis` |
| 6 | `#/$defs/legacyData/properties/sourceVersion/const` = `"2.3.0"` | [45_legacy_import_archive.ostf](../samples/45_legacy_import_archive.ostf) | `/extensions/org.ostf.legacy-import.v1/data/sourceVersion` |
| 7 | `#/$defs/extensions/properties/org.ostf.relative-phrase.v1/allOf/1/if/properties/version/const` = `"1.0.0-draft.1"` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/version` |
| 8 | `#/$defs/extensions/properties/org.ostf.generation-context.v1/allOf/1/if/properties/version/const` = `"1.0.0-draft.1"` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/version` |
| 9 | `#/$defs/extensions/properties/org.ostf.appearance.v1/allOf/1/if/properties/version/const` = `"1.0.0-draft.1"` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/version` |
| 10 | `#/$defs/extensions/properties/org.ostf.legacy-import.v1/allOf/1/if/properties/version/const` = `"1.0.0-draft.1"` | [45_legacy_import_archive.ostf](../samples/45_legacy_import_archive.ostf) | `/extensions/org.ostf.legacy-import.v1/version` |
| 11 | `#/$defs/extensions/properties/org.ostf.phrase-library.v1/allOf/1/if/properties/version/const` = `"1.0.0-draft.1"` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/version` |
| 12 | `#/$defs/extensions/properties/org.ostf.clip-choices.v1/allOf/1/if/properties/version/const` = `"1.0.0-draft.1"` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1/version` |
| 13 | `#/$defs/midiMapping/allOf/0/if/properties/standard/const` = `"gm1"` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/soundSlots/0/midiMapping/standard` |
| 14 | `#/properties/format/const` = `"OSTF"` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/format` |
| 15 | `#/properties/version/const` = `"3.1.0"` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/version` |

## Named schema definitions / 定義

| # | Schema declaration / value | Example `.ostf` | At (JSON pointer) |
| ---: | --- | --- | --- |
| 1 | `#/$defs/id` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/appearance/customRoleColors/role-verse` |
| 2 | `#/$defs/nonnegative` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/targetRange/start` |
| 3 | `#/$defs/positive` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/targetRange/duration` |
| 4 | `#/$defs/signed` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/clips/0/notes/0/start` |
| 5 | `#/$defs/pitch` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/data/assignments/0/anchorPitch` |
| 6 | `#/$defs/ref` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/appearance/objectColors/0/target` |
| 7 | `#/$defs/range` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/targetRange` |
| 8 | `#/$defs/spelledPitchClass` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/chords/0/root` |
| 9 | `#/$defs/song` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/song` |
| 10 | `#/$defs/section` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline/sections/0` |
| 11 | `#/$defs/tempo` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline/tempoChanges/0` |
| 12 | `#/$defs/meter` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline/meterChanges/0` |
| 13 | `#/$defs/timeline` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/timeline` |
| 14 | `#/$defs/chord` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/chords/0` |
| 15 | `#/$defs/scale` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/scales/0` |
| 16 | `#/$defs/harmony` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony` |
| 17 | `#/$defs/instrument` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/instrument` |
| 18 | `#/$defs/note` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/clips/0/notes/0` |
| 19 | `#/$defs/clip` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/clips/0` |
| 20 | `#/$defs/track` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0` |
| 21 | `#/$defs/soundSlot` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/soundSlots/0` |
| 22 | `#/$defs/lyricDocument` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/documents/0` |
| 23 | `#/$defs/lyricPhrase` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/phrases/0` |
| 24 | `#/$defs/lyricUnit` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/units/0` |
| 25 | `#/$defs/lyricAlignment` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/alignments/0` |
| 26 | `#/$defs/lyrics` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics` |
| 27 | `#/$defs/sha256` | [16_generation_context.ostf](../samples/16_generation_context.ostf) | `/resources/0/sha256` |
| 28 | `#/$defs/resource` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/resources/0` |
| 29 | `#/$defs/dependencies` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/dependencies` |
| 30 | `#/$defs/extension` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1` |
| 31 | `#/$defs/relativeAssignment` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/data/assignments/0` |
| 32 | `#/$defs/relativeData` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/data` |
| 33 | `#/$defs/generator` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/generator` |
| 34 | `#/$defs/generationInput` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0/inputs/0` |
| 35 | `#/$defs/generationProcess` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data/processes/0` |
| 36 | `#/$defs/generationData` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1/data` |
| 37 | `#/$defs/color` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/appearance/customRoleColors/role-verse` |
| 38 | `#/$defs/roleDefinition` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/roleDefinitions/0` |
| 39 | `#/$defs/roleColorMap` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/appearance/roleColors` |
| 40 | `#/$defs/customRoleColorMap` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/appearance/customRoleColors` |
| 41 | `#/$defs/objectColor` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data/appearance/objectColors/0` |
| 42 | `#/$defs/appearanceData` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/data` |
| 43 | `#/$defs/legacyData` | [45_legacy_import_archive.ostf](../samples/45_legacy_import_archive.ostf) | `/extensions/org.ostf.legacy-import.v1/data` |
| 44 | `#/$defs/extensions` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions` |
| 45 | `#/$defs/phraseTemplate` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/templates/0` |
| 46 | `#/$defs/phraseNoteMapping` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/instances/0/noteMap/0` |
| 47 | `#/$defs/phraseInstance` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/instances/0` |
| 48 | `#/$defs/phraseLibraryData` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data` |
| 49 | `#/$defs/clipCandidate` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1/data/groups/0/candidates/0` |
| 50 | `#/$defs/clipChoiceGroup` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1/data/groups/0` |
| 51 | `#/$defs/clipChoicesData` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1/data` |
| 52 | `#/$defs/midiMapping` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/soundSlots/0/midiMapping` |
| 53 | `#/$defs/soundSource` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/tracks/0/soundSource` |
| 54 | `#/$defs/localizedNames` | [71_multilingual_tracks_and_multiple_drum_kits.ostf](../samples/71_multilingual_tracks_and_multiple_drum_kits.ostf) | `/drumKits/0/localizedNames` |
| 55 | `#/$defs/drumKit` | [71_multilingual_tracks_and_multiple_drum_kits.ostf](../samples/71_multilingual_tracks_and_multiple_drum_kits.ostf) | `/drumKits/0` |
| 56 | `#/$defs/phraseSourceNote` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/templates/0/notes/0` |

## Structural branches / 構造分岐

| # | Schema declaration / value | Example `.ostf` | At (JSON pointer) |
| ---: | --- | --- | --- |
| 1 | `#/$defs/chord/dependentRequired` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/harmony/chords/0` |
| 2 | `#/$defs/note/oneOf` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0/clips/0/notes/0` |
| 3 | `#/$defs/track/allOf` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0` |
| 4 | `#/$defs/track/allOf/0/if` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0` |
| 5 | `#/$defs/track/allOf/0/then` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/tracks/0` |
| 6 | `#/$defs/lyricPhrase/dependentRequired` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/phrases/0` |
| 7 | `#/$defs/lyricUnit/dependentRequired` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/lyrics/units/0` |
| 8 | `#/$defs/dependencies/oneOf` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1/dependencies` |
| 9 | `#/$defs/relativeAssignment/allOf` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/data/assignments/0` |
| 10 | `#/$defs/relativeAssignment/allOf/0/if` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/data/assignments/0` |
| 11 | `#/$defs/relativeAssignment/allOf/0/then` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1/data/assignments/0` |
| 12 | `#/$defs/extensions/properties/org.ostf.relative-phrase.v1/allOf` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1` |
| 13 | `#/$defs/extensions/properties/org.ostf.relative-phrase.v1/allOf/1/if` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1` |
| 14 | `#/$defs/extensions/properties/org.ostf.relative-phrase.v1/allOf/1/then` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.relative-phrase.v1` |
| 15 | `#/$defs/extensions/properties/org.ostf.generation-context.v1/allOf` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1` |
| 16 | `#/$defs/extensions/properties/org.ostf.generation-context.v1/allOf/1/if` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1` |
| 17 | `#/$defs/extensions/properties/org.ostf.generation-context.v1/allOf/1/then` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.generation-context.v1` |
| 18 | `#/$defs/extensions/properties/org.ostf.appearance.v1/allOf` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1` |
| 19 | `#/$defs/extensions/properties/org.ostf.appearance.v1/allOf/1/if` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1` |
| 20 | `#/$defs/extensions/properties/org.ostf.appearance.v1/allOf/1/then` | [01_four_part_sketch.ostf](../samples/01_four_part_sketch.ostf) | `/extensions/org.ostf.appearance.v1` |
| 21 | `#/$defs/extensions/properties/org.ostf.legacy-import.v1/allOf` | [45_legacy_import_archive.ostf](../samples/45_legacy_import_archive.ostf) | `/extensions/org.ostf.legacy-import.v1` |
| 22 | `#/$defs/extensions/properties/org.ostf.legacy-import.v1/allOf/1/if` | [45_legacy_import_archive.ostf](../samples/45_legacy_import_archive.ostf) | `/extensions/org.ostf.legacy-import.v1` |
| 23 | `#/$defs/extensions/properties/org.ostf.legacy-import.v1/allOf/1/then` | [45_legacy_import_archive.ostf](../samples/45_legacy_import_archive.ostf) | `/extensions/org.ostf.legacy-import.v1` |
| 24 | `#/$defs/extensions/properties/org.ostf.phrase-library.v1/allOf` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1` |
| 25 | `#/$defs/extensions/properties/org.ostf.phrase-library.v1/allOf/1/if` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1` |
| 26 | `#/$defs/extensions/properties/org.ostf.phrase-library.v1/allOf/1/then` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1` |
| 27 | `#/$defs/extensions/properties/org.ostf.clip-choices.v1/allOf` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1` |
| 28 | `#/$defs/extensions/properties/org.ostf.clip-choices.v1/allOf/1/if` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1` |
| 29 | `#/$defs/extensions/properties/org.ostf.clip-choices.v1/allOf/1/then` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1` |
| 30 | `#/$defs/clipChoiceGroup/properties/selectedCandidateId/anyOf` | [25_choice_shared_muted.ostf](../samples/25_choice_shared_muted.ostf) | `/extensions/org.ostf.clip-choices.v1/data/groups/0/selectedCandidateId` |
| 31 | `#/$defs/midiMapping/allOf` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/soundSlots/0/midiMapping` |
| 32 | `#/$defs/midiMapping/allOf/0/if` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/soundSlots/0/midiMapping` |
| 33 | `#/$defs/midiMapping/allOf/0/then` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/soundSlots/0/midiMapping` |
| 34 | `#/$defs/soundSource/allOf` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/tracks/0/soundSource` |
| 35 | `#/$defs/soundSource/allOf/0/if` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/tracks/0/soundSource` |
| 36 | `#/$defs/soundSource/allOf/0/then` | [61_gm1_drum_grid.ostf](../samples/61_gm1_drum_grid.ostf) | `/tracks/0/soundSource` |
| 37 | `#/$defs/phraseSourceNote/oneOf` | [22_phrase_library.ostf](../samples/22_phrase_library.ostf) | `/extensions/org.ostf.phrase-library.v1/data/templates/0/notes/0` |

