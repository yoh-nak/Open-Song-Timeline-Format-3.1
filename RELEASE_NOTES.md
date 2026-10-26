# OSTF 3.1.0 — Official specification release notes / 正式公開ノート

**Publication decision: GO (specification + bilingual full manual/reference + 100-file sample distribution).**  
**Software/interoperability verification: NOT PERFORMED.** No schema validator, reader program, DAW, Max for Live, MIDI converter, or external plugin was executed or tested in preparing this release, at the owner's request.

## Release contents

- **100 files exactly**, including manifest; each file is GitHub-ready and the **76 complete 3.1 `.ostf` examples** are standalone UTF-8 JSON documents.
- **Bilingual normative specifications** (`docs/FORMAT_SPECIFICATION.*.md`) and **complete manuals** (`docs/COMPLETE_MANUAL.*.md`).
- **Bilingual comprehensive parameter references** (`docs/PARAMETER_REFERENCE.*.md`) and a **static field/enum/structure → actual `.ostf` witness index** (`docs/COVERAGE.md`).
- **Schemas:** 3.1.0, unchanged 3.0.0, unchanged 3.0 Draft 1/2 for the included historical reader.
- **Examples:** 76 authored 3.1 plus three byte-preserved 3.0.0 inputs; the 2.3 source is maintained in its separate repository rather than copied here.
- **Reference library:** `ostf3.py` only; former full editor/CLI and MIDI adapter tools are not bundled due to the 100-file packaging requirement.

## Normative Core amendment

1. Track category and advisory view (`trackType`, `preferredView`) for melodic/drum/mixed music; original names/order/IDs preserved.
2. Optional BCP47-like localized names/titles; names stay distinct from identities and routing.
3. Variable global Sound Slots and multiple optional `drumKits`, explicit `drumKitId` references and `midiMapping`; no implicit GM1 matching from `midiNote`.
4. An inert `soundSource` category hint; **no standardized Program Change, Bank Select, synth presets, CC, pitch bend or aftertouch**.
5. **Optional performed-note `velocity`: JSON integer 1–127** on every actual Core note, including primary melody and drums; omitted notes remain omitted. Never placed on harmonic Note Profile or the frozen phrase source profile.
6. Existing 3.0 Core fields and all six provisional standard optional-profile versions remain unchanged; 3.1 readers must support 3.0.0 without silent upgrade.
7. Host-facing mapping and export-time fallback must disclose any information loss. Direct `.mid` export or host-automation support is not included.

## Static evidence and caveats / 静的資料と制約

The parameter index traces **194 canonical declarations, 18 conditional overlays, 53 enum alternatives, 15 constants, 56 definitions, and 37 structural schema branches** to authored samples. This is a **source occurrence** index only: not evidence of semantic correctness, automated validation, rendered audio, successful MIDI output, or interoperability. Unbounded strings, values, arbitrary vendor extension payloads and all parameter combinations cannot be covered by finitely many examples.

All shipped samples and schemas are JSON files that can be inspected as text. Exact published SHA-256 checksums are in `PACKAGE_MANIFEST.json`, which excludes itself. External standards/software owners do not thereby endorse OSTF or implement it.

## Release recommendation / 公開判定

**GO for public GitHub publication of OSTF 3.1.0 as an exchange-format specification.** Do not claim actual Ableton, REAPER, Logic, Cubase, FL Studio or third-party plugin compatibility has been verified. A validator pass or successful DAW round-trip is a separate future milestone, not a prerequisite imposed by this owner's publication scope. This archive was not pushed to GitHub; suggested release tag `v3.1.0`.

**日本語要約：** コード進行・主旋律・歌詞・曲構成と、任意の軽量アレンジノートを交換する**フォーマットの正式仕様として公開可能**です。演奏Velocityは任意の1～127。ドラムのSound Slot、Kit、多言語トラック名、表示ヒント、3.0互換を定義します。一方、音源プリセット・MIDI CC・Bend・AT・高度なDAW編集はCoreには含めません。ご指定により**動作検証は一切行っていません**。
