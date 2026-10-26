# Open Song Timeline Format — OSTF 3.1.0

**GitHub正式公開用・100ファイル以内・UTF-8 JSON形式（`.ostf`）**

OSTFは、**コード進行・曲構成・メインメロディー・歌詞・必要最小限のアレンジ**を作曲支援ソフト間で交換するための共通フォーマットです。DAWプロジェクトやプラグインの音色設定を再現することは目的としません。音符の高度な編集、生成、歌唱、ミキシングなどは各ソフトウェア側に任せます。

[English README](README.md)

## 正式仕様と全網羅資料

| 資料 | 日本語 | English |
| --- | --- | --- |
| **規範仕様（データの意味と保存規則）** | [正式仕様書](docs/FORMAT_SPECIFICATION.ja.md) | [Specification](docs/FORMAT_SPECIFICATION.en.md) |
| **全網羅マニュアル（使い方・概念・編集上の注意）** | [完全マニュアル](docs/COMPLETE_MANUAL.ja.md) | [Complete manual](docs/COMPLETE_MANUAL.en.md) |
| **全パラメーターの定義・型・範囲** | [パラメーターリファレンス](docs/PARAMETER_REFERENCE.ja.md) | [Parameter reference](docs/PARAMETER_REFERENCE.en.md) |
| **全パラメーターと実例の対応表** | [全項目→サンプル対応表](docs/COVERAGE.md) | [サンプル索引](samples/INDEX.md) |

[3.0→3.1互換・移行指針](docs/MIGRATION_3_0_TO_3_1.md)、[GM1ドラムマップ](docs/GM1_DRUM_MAP.json)、[3.1 JSON Schema](schema/ostf-3.1.0.schema.json)、[3.0原典Schema](schema/ostf-3.0.0.schema.json)、[ライセンス](LICENSE.md)、[公開判定と制約](RELEASE_NOTES.md)を収録します。

## `.ostf`サンプルの入口

| 学習したい内容 | サンプル |
| --- | --- |
| 最小構成 | [02_empty_sketch.ostf](samples/02_empty_sketch.ostf) |
| コード進行のみ | [03_harmony_only.ostf](samples/03_harmony_only.ostf) |
| 主旋律のみ | [04_melody_only.ostf](samples/04_melody_only.ostf) |
| 歌詞とノートの対応 | [20_lyric_alignment.ostf](samples/20_lyric_alignment.ostf) |
| 作曲の統合例 | [58_complete_workflow.ostf](samples/58_complete_workflow.ostf) |
| GM1ドラム | [61_gm1_drum_grid.ostf](samples/61_gm1_drum_grid.ostf) |
| カスタムドラム割当 | [64_custom_drum_mapping.ostf](samples/64_custom_drum_mapping.ostf) |
| 多言語トラック名・複数キット | [71_multilingual_tracks_and_multiple_drum_kits.ostf](samples/71_multilingual_tracks_and_multiple_drum_kits.ostf) |
| Melody・DrumsのVelocity | [74](samples/74_velocity_melody_optional.ostf)、[75](samples/75_velocity_drum_accents.ostf) |

**独立した`.ostf`形式の3.1サンプル76件をすべて保持**しています。3.0原典の未変更サンプル3件も収録しました。全194項目・18条件付き項目・53列挙値・15定数・56定義・37構造分岐の*記載箇所*を[対応表](docs/COVERAGE.md)で確認できます。全組合せ・全音楽表現・任意の独自拡張までは有限例で列挙できません。記載は動作検証合格を意味しません。

## OSTF 3.1の確定範囲

- トラック数とSound Slot数は固定しません。`trackType`は`melodic`/`drum`/`mixed`、`preferredView`は`auto`/`pianoRoll`/`drumGrid`です。表示形式は希望であり、DAWの画面を強制操作しません。
- トラックID・元のUnicode名称・配列順を保存し、任意の`localizedNames`/`localizedTitles`で複数言語の表示を補えます。音源・キット・Sound Slotの表示名も同様です。
- ドラムは任意の`drumKits[]`からSound Slot IDを参照します。GM1のMIDIノート番号は`midiMapping`で明示する場合だけ意味を持ちます。
- `instrument`は楽器の**説明情報**、`soundSource`は実際の音源を強制しないヒントです。Program Change、Bank Select、音源Preset、CC、Pitch Bend、Aftertouchやミキサー状態はCoreの対象外です。
- `velocity`は**演奏ノートの任意整数（1～127）**です。未指定の場合は元のOSTFに書き足しません。主旋律・ドラム・通常アレンジに共通で、和声のコード構成音や旧フレーズ原型には追加しません。
- `song.primaryMelodyTrackId`は**主旋律を最大1本指定**します。ハモリ・対旋律・バックコーラスは必要なら通常のアレンジトラックを利用します。メロディーや歌詞の自動生成・歌唱合成は行いません。
- 3.1対応Readerは3.0のファイルを勝手に書き換えず読み込みます。旧版へのダウングレードでは3.1独自情報の損失を報告します。

## 適合と公開の注意

データ構造はJSON Schema、参照の整合性・時間・編集保護などは正式仕様を参照します。任意の独自拡張を理解できないソフトも、情報損失なしを主張するなら元データを保持しなければなりません。

`ostf3.py`は4種類のSchemaを参照する**補助的なPythonライブラリ**であり、DAW操作、`.mid`ファイル書出、音源再生を行うツールではありません。`jsonschema`が必要な場合は別途導入します。100ファイル以内にするため、旧編集・移行CLIおよびMIDIアダプターは同梱せず、規則だけをマニュアルに収録しています。

**リリース判定：仕様書・リファレンス・マニュアル・Schema・サンプルの公開はGO。** ご希望どおりSchema Validatorの実行やPythonコードの動作試験、DAW/Max for Liveでの確認、他社製品との交換検証は行っていません。動作の適合を保証するGOではありません。詳細は[RELEASE_NOTES.md](RELEASE_NOTES.md)をご覧ください。

配布ZIPを展開して、中身をGitHubリポジトリ直下に登録してください。**ちょうど100ファイル（マニフェスト含む）**です。GitHubへコミット・タグ・リリースを作成したわけではありません。推奨タグは`v3.1.0`です。
