# OSTF 3.1.0 全パラメーターリファレンス

Core `3.1.0` と、同梱する6種類の任意profileの正確な版 `1.0.0-draft.1` を対象とします。この文書はSchemaの全定義・宣言フィールド・選択値・分岐・制約を参照する辞典です。使い方は[全網羅マニュアル](COMPLETE_MANUAL.ja.md)、規範的な意味は[仕様本文](FORMAT_SPECIFICATION.ja.md)、具体的なファイルは[サンプル索引](../samples/INDEX.md)を参照してください。

**列挙した項目の範囲**：宣言パラメーター 194件、条件による再制約 18件、名前付き定義56件、enum 12組（値の出現数53）。枝ごとの同名フィールドは別宣言として数えます。同じ定義を使う複数の場所は、その定義を重複計上しません。任意文字列・数値・ベンダーJSONの全組合せを有限個の例で列挙する意味ではありません。

このリファレンス本文に、全項目のSchema JSON Pointer、展開したinstance path、型・制約を掲載しています。[COVERAGE.md](COVERAGE.md)から各項目を実際の`.ostf`サンプルへ追えます。これは文書作成用の静的な棚卸しであり、実行検証や適合性の合格結果ではありません。


> 正式100ファイル版では、この資料自体が全パラメーターの公開リファレンスです。旧生成スクリプトとJSONカタログは同梱せず、[COVERAGE.md](COVERAGE.md)に全項目と`.ostf`実例の所在を収録しています。

## 読み方と共通規則

- 「必須」はキーが必要という意味です。任意でも`null`が許されるとは限りません。標準の明示的nullは`selectedCandidateId`の未選択です。
- `additionalProperties: false`は未宣言キーの禁止です。Core3.1の演奏ノートの`velocity`は正式宣言済み（1～127）ですが、それ以外の未定義項目は追加できません。
- `default`はSchema注釈であり、自動挿入しません。track/clipの`enabled`だけは仕様上、省略を`true`として解釈します。
- `minimum`/`maximum`は両端を含み、`exclusiveMinimum`はその値を除きます。`uniqueItems`は配列要素の重複禁止です。
- 整数フィールドにはJSON整数tokenを使います。`1.0`、`1e0`、`true`は整数フィールドの正しい記述ではありません。
- `oneOf`は一つだけ、`anyOf`は少なくとも一つ、`allOf`はすべての規則に一致します。`if`は条件検査、`then`は条件成立時の追加制約です。
- 任意profileの解釈はnamespaceと正確な版で決めます。未知版の`data`は共通envelope内で保持し、旧版payload規則を適用しません。
- instance pathの`[*]`は配列要素または動的な辞書キーを表します。パスの列挙だけで条件分岐の成立を意味しません。

Schema SHA-256: `3f648348117581b2e28237402cab251d0a6fbd991ac0e1c6158bc201f5fc6630`.

出典: [ostf-3.1.0.schema.json](../schema/ostf-3.1.0.schema.json).

## 型・オブジェクト索引

- [root](#def-root) — 文書全体。11個のrootキーはすべて必須。
- [id](#def-id) — IDの字句形式。Core全体での一意性と、profile内の局所IDの一意性は別の意味規則。
- [nonnegative](#def-nonnegative) — 非負の整数tick・回数添字。
- [positive](#def-positive) — 正の整数tick・回数。
- [signed](#def-signed) — 符号付き整数。ノートの局所開始位置に使用。
- [pitch](#def-pitch) — 半音単位の音高番号。60=C4、69=A4。
- [ref](#def-ref) — Coreオブジェクトへの型付き参照。typeとidの両方が一致する必要がある。
- [range](#def-range) — 曲全体のtick座標による区間。終了位置の加算にも上限を適用する。
- [spelledPitchClass](#def-spelledpitchclass) — 綴りを持つ音名。オクターブを含まず、異名同音の綴りを保持する。
- [song](#def-song) — 曲名と主旋律の指定。未命名の曲には空のtitleを使用できる。
- [section](#def-section) — 曲構成の区間。隙間は許すが区間同士は重ならない。
- [tempo](#def-tempo) — そのtick以後のテンポ。BPMは拍子によらず四分音符毎分。
- [meter](#def-meter) — そのtick以後の拍子。変更点を暗黙の小節境界へ移動しない。
- [timeline](#def-timeline) — 曲構成、テンポ変更、拍子変更の配列。
- [chord](#def-chord) — 和音の意味情報。labelだけでも有効で、演奏ボイシングを生成しない。
- [scale](#def-scale) — 音階の意味情報。Coreノートの使用可能音を制限しない。
- [harmony](#def-harmony) — 和音と音階の配列。演奏はCoreノートとして別に保存する。
- [instrument](#def-instrument) — 楽器の表示情報。プラグイン状態や音源を指定する契約ではない。
- [note](#def-note) — 実演奏Coreノート。発音対象・局所開始・ゲートと任意のNote On Velocity（1～127）。原型phrase sourceとは別定義。
- [clip](#def-clip) — トラック上の配置・編集単位。durationはノートを切るマスクではない。
- [track](#def-track) — 名前、役割、楽器説明、クリップと任意のトラック種別・表示ヒントを持つ。
- [soundSlot](#def-soundslot) — 打楽器の発音先。IDが同一性を持ち、MIDI番号やroleは同一性ではない。
- [lyricDocument](#def-lyricdocument) — 歌詞文書の識別と補助情報。
- [lyricPhrase](#def-lyricphrase) — 表示用の歌詞フレーズ。分割単位の連結と同じ文字列である必要はない。
- [lyricUnit](#def-lyricunit) — 歌詞の分割・対応づけの単位。
- [lyricAlignment](#def-lyricalignment) — 歌詞単位とCoreノートの順序付き多対多対応。
- [lyrics](#def-lyrics) — 歌詞文書、フレーズ、単位、対応の四配列。
- [sha256](#def-sha256) — 小文字16進数64桁のSHA-256値。
- [resource](#def-resource) — 生成素材などへの参照。読込時の取得・実行・音声再生指示ではない。
- [dependencies](#def-dependencies) — 拡張が依存するCoreの範囲。二つのoneOf構造で三種類のscopeを表す。
- [extension](#def-extension) — 既知・未知のすべての拡張に共通する閉じたenvelope。
- [relativeAssignment](#def-relativeassignment) — Coreの有音高ノートと、和音・音階の構成音との対応。
- [relativeData](#def-relativedata) — 相対音高の対応一覧。読込時にCoreを書き換えない。
- [generator](#def-generator) — 生成器の識別子と版。アルゴリズムの再現を保証するものではない。
- [generationInput](#def-generationinput) — 一つの入力役割、Core参照、任意の読取範囲。
- [generationProcess](#def-generationprocess) — 生成入力・出力・保護ノートなどの関係記録。
- [generationData](#def-generationdata) — 複数の生成工程の記録。
- [color](#def-color) — RGB色。#に続く大文字または小文字の16進数6桁。
- [roleDefinition](#def-roledefinition) — 表示用の独自セクション役割の定義。
- [roleColorMap](#def-rolecolormap) — 任意のrole文字列からRGB色への辞書。
- [customRoleColorMap](#def-customrolecolormap) — 定義済み独自role IDからRGB色への辞書。
- [objectColor](#def-objectcolor) — 型付きCore参照に対する個別色。
- [appearanceData](#def-appearancedata) — 独自役割、セクションへの割当、色の表示情報。演奏には影響しない。
- [legacyData](#def-legacydata) — 2.3原文とSHA-256、移行記録の保存。Coreを書き戻す指示ではない。
- [extensions](#def-extensions) — namespaceをキーに持つ拡張辞書。正確なnamespaceと版でpayload構造を選ぶ。
- [phraseTemplate](#def-phrasetemplate) — 再利用する具体的ノート列。durationは反復周期。
- [phraseNoteMapping](#def-phrasenotemapping) — source noteと反復番号から、実体化済みCoreノートへの対応。
- [phraseInstance](#def-phraseinstance) — templateと一つのCore clipの完全対応。
- [phraseLibraryData](#def-phraselibrarydata) — 具体的phrase templatesと実体化済みinstances。読込時に展開しない。
- [clipCandidate](#def-clipcandidate) — 候補の局所IDと、その候補で有効にするCore clips。
- [clipChoiceGroup](#def-clipchoicegroup) — 候補群と保存済み選択。Coreのenabled状態との一致を記録する。
- [clipChoicesData](#def-clipchoicesdata) — 独立したクリップ選択グループの配列。
- [midiMapping](#def-midimapping) — gm1またはcustomの明示的MIDI1ノート割当。
- [soundSource](#def-soundsource) — 任意の音源割当ヒント。音色再現・プラグイン復元は保証しない。
- [localizedNames](#def-localizednames) — 言語タグをキーとする任意の多言語表示名の辞書。元の名前は変更しない。
- [drumKit](#def-drumkit) — 名前付きの順序付きグローバルSound Slot参照集合。音源やGMプログラムではない。
- [phraseSourceNote](#def-phrasesourcenote) — 旧1.0.0-draft.1の原型フレーズ・ノート型。Velocityを含まない（profile版を勝手に変更しない）。

<a id="def-root"></a>

## root

文書全体。11個のrootキーはすべて必須。

Schema: `#`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `format`<br>`#/properties/format` | 必須 | const=`"OSTF"` | 形式識別子。正確にOSTF。 |
| `version`<br>`#/properties/version` | 必須 | const=`"3.1.0"` | Core wire版。正確に3.1.0。 |
| `ppq`<br>`#/properties/ppq` | 必須 | `"integer"`; minimum=`1`; maximum=`960000` | 四分音符あたりの整数tick数。推奨960だが宣言値を使用する。 |
| `song`<br>`#/properties/song` | 必須 | [song](#def-song); `"object"`; 追加キー禁止 | 曲情報。 |
| `timeline`<br>`#/properties/timeline` | 必須 | [timeline](#def-timeline); `"object"`; 追加キー禁止 | セクション・テンポ・拍子。 |
| `harmony`<br>`#/properties/harmony` | 必須 | [harmony](#def-harmony); `"object"`; 追加キー禁止 | 和音・音階の意味情報。 |
| `tracks`<br>`#/properties/tracks` | 必須 | `"array"`; items: [track](#def-track); `"object"`; 追加キー禁止; allOf（下記構造規則） | 表示順を保持する演奏トラック配列。 |
| `soundSlots`<br>`#/properties/soundSlots` | 必須 | `"array"`; items: [soundSlot](#def-soundslot); `"object"`; 追加キー禁止 | 打楽器の発音先一覧。 |
| `lyrics`<br>`#/properties/lyrics` | 必須 | [lyrics](#def-lyrics); `"object"`; 追加キー禁止 | 歌詞とノートへの対応。 |
| `resources`<br>`#/properties/resources` | 必須 | `"array"`; items: [resource](#def-resource); `"object"`; 追加キー禁止 | 参照素材の一覧。自動取得しない。 |
| `extensions`<br>`#/properties/extensions` | 必須 | [extensions](#def-extensions); `"object"`; additionalProperties: [extension](#def-extension); `"object"`; 追加キー禁止; propertyNames=`{"pattern":"^[a-z][a-z0-9-]*(?:\\.[a-z][a-z0-9-]*){2,}$","not":{"pattern":"[\\r\\n\\u2028\\u2029]"}}` | 標準profileと独自データのnamespace辞書。 |
| `drumKits`<br>`#/properties/drumKits` | 任意 | `"array"`; items: [drumKit](#def-drumkit); `"object"`; 追加キー禁止 | 任意のドラムキット定義配列。 |

<a id="def-id"></a>

## id

IDの字句形式。Core全体での一意性と、profile内の局所IDの一意性は別の意味規則。

Schema: `#/$defs/id`

`"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}`.

使用箇所（構造上のパス）:

- `$.drumKits[*].id`
- `$.drumKits[*].soundSlotIds[*]`
- `$.extensions["org.ostf.appearance.v1"].data.appearance.customRoleColors.<key>`
- `$.extensions["org.ostf.appearance.v1"].data.appearance.objectColors[*].target.id`
- `$.extensions["org.ostf.appearance.v1"].data.roleDefinitions[*].id`
- `$.extensions["org.ostf.appearance.v1"].data.sectionRoleAssignments.<key>`
- `$.extensions["org.ostf.appearance.v1"].data.sectionRoleAssignments[*]`
- `$.extensions["org.ostf.appearance.v1"].dependencies.refs[*].id`
- `$.extensions["org.ostf.clip-choices.v1"].data.groups[*].candidates[*].clipIds[*]`
- `$.extensions["org.ostf.clip-choices.v1"].data.groups[*].candidates[*].id`
- `$.extensions["org.ostf.clip-choices.v1"].data.groups[*].id`
- `$.extensions["org.ostf.clip-choices.v1"].data.groups[*].selectedCandidateId`
- `$.extensions["org.ostf.clip-choices.v1"].dependencies.refs[*].id`
- `$.extensions["org.ostf.generation-context.v1"].data.processes[*].id`
- `$.extensions["org.ostf.generation-context.v1"].data.processes[*].inputs[*].ref.id`
- `$.extensions["org.ostf.generation-context.v1"].data.processes[*].outputs[*].id`
- `$.extensions["org.ostf.generation-context.v1"].data.processes[*].protectedNoteIds[*]`
- `$.extensions["org.ostf.generation-context.v1"].dependencies.refs[*].id`
- `$.extensions["org.ostf.legacy-import.v1"].dependencies.refs[*].id`
- `$.extensions["org.ostf.phrase-library.v1"].data.instances[*].clipId`
- `$.extensions["org.ostf.phrase-library.v1"].data.instances[*].id`
- `$.extensions["org.ostf.phrase-library.v1"].data.instances[*].noteMap[*].noteId`
- `$.extensions["org.ostf.phrase-library.v1"].data.instances[*].noteMap[*].templateNoteId`
- `$.extensions["org.ostf.phrase-library.v1"].data.instances[*].templateId`
- `$.extensions["org.ostf.phrase-library.v1"].data.templates[*].id`
- `$.extensions["org.ostf.phrase-library.v1"].data.templates[*].notes[*].id`
- `$.extensions["org.ostf.phrase-library.v1"].data.templates[*].notes[*].soundSlotId`
- `$.extensions["org.ostf.phrase-library.v1"].dependencies.refs[*].id`
- `$.extensions["org.ostf.relative-phrase.v1"].data.assignments[*].contextId`
- `$.extensions["org.ostf.relative-phrase.v1"].data.assignments[*].noteId`
- `$.extensions["org.ostf.relative-phrase.v1"].dependencies.refs[*].id`
- `$.extensions[*].dependencies.refs[*].id`
- `$.harmony.chords[*].id`
- `$.harmony.scales[*].id`
- `$.lyrics.alignments[*].id`
- `$.lyrics.alignments[*].noteIds[*]`
- `$.lyrics.alignments[*].unitIds[*]`
- `$.lyrics.documents[*].id`
- `$.lyrics.phrases[*].documentId`
- `$.lyrics.phrases[*].id`
- `$.lyrics.units[*].id`
- `$.lyrics.units[*].phraseId`
- `$.resources[*].id`
- `$.song.primaryMelodyTrackId`
- `$.soundSlots[*].id`
- `$.timeline.sections[*].id`
- `$.tracks[*].clips[*].id`
- `$.tracks[*].clips[*].notes[*].id`
- `$.tracks[*].clips[*].notes[*].soundSlotId`
- `$.tracks[*].drumKitId`
- `$.tracks[*].id`

構造・分岐規則（Schema原文）:

```json
{
  "not": {
    "pattern": "[\\r\\n\\u2028\\u2029]"
  }
}
```

<a id="def-nonnegative"></a>

## nonnegative

非負の整数tick・回数添字。

Schema: `#/$defs/nonnegative`

`"integer"`; minimum=`0`; maximum=`9007199254740991`.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.generation-context.v1"].data.processes[*].inputs[*].readRange.start`
- `$.extensions["org.ostf.generation-context.v1"].data.processes[*].targetRange.start`
- `$.extensions["org.ostf.phrase-library.v1"].data.instances[*].noteMap[*].repeatIndex`
- `$.harmony.chords[*].start`
- `$.harmony.scales[*].start`
- `$.lyrics.phrases[*].start`
- `$.lyrics.units[*].start`
- `$.timeline.meterChanges[*].at`
- `$.timeline.sections[*].start`
- `$.timeline.tempoChanges[*].at`
- `$.tracks[*].clips[*].start`

<a id="def-positive"></a>

## positive

正の整数tick・回数。

Schema: `#/$defs/positive`

`"integer"`; minimum=`1`; maximum=`9007199254740991`.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.generation-context.v1"].data.processes[*].inputs[*].readRange.duration`
- `$.extensions["org.ostf.generation-context.v1"].data.processes[*].targetRange.duration`
- `$.extensions["org.ostf.phrase-library.v1"].data.instances[*].repeatCount`
- `$.extensions["org.ostf.phrase-library.v1"].data.templates[*].duration`
- `$.extensions["org.ostf.phrase-library.v1"].data.templates[*].notes[*].duration`
- `$.harmony.chords[*].duration`
- `$.harmony.scales[*].duration`
- `$.lyrics.phrases[*].duration`
- `$.lyrics.units[*].duration`
- `$.timeline.sections[*].duration`
- `$.tracks[*].clips[*].duration`
- `$.tracks[*].clips[*].notes[*].duration`

<a id="def-signed"></a>

## signed

符号付き整数。ノートの局所開始位置に使用。

Schema: `#/$defs/signed`

`"integer"`; minimum=`-9007199254740991`; maximum=`9007199254740991`.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.phrase-library.v1"].data.templates[*].notes[*].start`
- `$.tracks[*].clips[*].notes[*].start`

<a id="def-pitch"></a>

## pitch

半音単位の音高番号。60=C4、69=A4。

Schema: `#/$defs/pitch`

`"integer"`; minimum=`0`; maximum=`127`.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.phrase-library.v1"].data.templates[*].notes[*].pitch`
- `$.extensions["org.ostf.relative-phrase.v1"].data.assignments[*].anchorPitch`
- `$.soundSlots[*].midiMapping.note`
- `$.soundSlots[*].midiNote`
- `$.tracks[*].clips[*].notes[*].pitch`

<a id="def-ref"></a>

## ref

Coreオブジェクトへの型付き参照。typeとidの両方が一致する必要がある。

Schema: `#/$defs/ref`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.appearance.v1"].data.appearance.objectColors[*].target`
- `$.extensions["org.ostf.appearance.v1"].dependencies.refs[*]`
- `$.extensions["org.ostf.clip-choices.v1"].dependencies.refs[*]`
- `$.extensions["org.ostf.generation-context.v1"].data.processes[*].inputs[*].ref`
- `$.extensions["org.ostf.generation-context.v1"].data.processes[*].outputs[*]`
- `$.extensions["org.ostf.generation-context.v1"].dependencies.refs[*]`
- `$.extensions["org.ostf.legacy-import.v1"].dependencies.refs[*]`
- `$.extensions["org.ostf.phrase-library.v1"].dependencies.refs[*]`
- `$.extensions["org.ostf.relative-phrase.v1"].dependencies.refs[*]`
- `$.extensions[*].dependencies.refs[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `type`<br>`#/$defs/ref/properties/type` | 必須 | enum=`["section","track","clip","note","chord","scale","soundSlot","drumKit","lyricDocument","lyricPhrase","lyricUnit","lyricAlignment","resource"]` | 参照先のCoreオブジェクト種別。 |
| `id`<br>`#/$defs/ref/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | typeで指定した種別のCore ID。 |

<a id="def-range"></a>

## range

曲全体のtick座標による区間。終了位置の加算にも上限を適用する。

Schema: `#/$defs/range`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.generation-context.v1"].data.processes[*].inputs[*].readRange`
- `$.extensions["org.ostf.generation-context.v1"].data.processes[*].targetRange`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `start`<br>`#/$defs/range/properties/start` | 必須 | [nonnegative](#def-nonnegative); `"integer"`; minimum=`0`; maximum=`9007199254740991` | 開始tick。座標系はこの型の説明を参照。 |
| `duration`<br>`#/$defs/range/properties/duration` | 必須 | [positive](#def-positive); `"integer"`; minimum=`1`; maximum=`9007199254740991` | 正の長さtick。終了位置の加算にも意味上の上限がある。 |

<a id="def-spelledpitchclass"></a>

## spelledPitchClass

綴りを持つ音名。オクターブを含まず、異名同音の綴りを保持する。

Schema: `#/$defs/spelledPitchClass`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.harmony.chords[*].bass`
- `$.harmony.chords[*].root`
- `$.harmony.scales[*].tonic`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `step`<br>`#/$defs/spelledPitchClass/properties/step` | 必須 | enum=`["A","B","C","D","E","F","G"]` | 自然音の文字名A〜G。 |
| `alter`<br>`#/$defs/spelledPitchClass/properties/alter` | 必須 | `"integer"`; minimum=`-2`; maximum=`2` | 半音単位の変化量。-2から2。 |

<a id="def-song"></a>

## song

曲名と主旋律の指定。未命名の曲には空のtitleを使用できる。

Schema: `#/$defs/song`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.song`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `title`<br>`#/$defs/song/properties/title` | 必須 | `"string"` | 表示用の題名。 |
| `primaryMelodyTrackId`<br>`#/$defs/song/properties/primaryMelodyTrackId` | 任意 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | 主旋律として指定する既存Core trackのID。 |
| `localizedTitles`<br>`#/$defs/song/properties/localizedTitles` | 任意 | [localizedNames](#def-localizednames); `"object"`; additionalProperties: `"string"`; minLength=`1`; propertyNames=`{"type":"string","pattern":"^(?:[A-Za-z]{2,3}\|[A-Za-z]{5,8})(?:-[A-Za-z0-9]{2,8})*$"}` | 曲名の多言語代替。元のsong.titleを保持。 |

<a id="def-section"></a>

## section

曲構成の区間。隙間は許すが区間同士は重ならない。

Schema: `#/$defs/section`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.timeline.sections[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/section/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | このレコードのID。適用される一意性の範囲は型の説明を参照。 |
| `name`<br>`#/$defs/section/properties/name` | 必須 | `"string"`; minLength=`1` | 表示名。IDの代用にはしない。 |
| `start`<br>`#/$defs/section/properties/start` | 必須 | [nonnegative](#def-nonnegative); `"integer"`; minimum=`0`; maximum=`9007199254740991` | 曲全体のセクション開始tick。 |
| `duration`<br>`#/$defs/section/properties/duration` | 必須 | [positive](#def-positive); `"integer"`; minimum=`1`; maximum=`9007199254740991` | セクションの区間長。区間端でノートを切らない。 |
| `role`<br>`#/$defs/section/properties/role` | 任意 | `"string"` | 用途・役割を表す文字列。固定enumではない。 |
| `localizedNames`<br>`#/$defs/section/properties/localizedNames` | 任意 | [localizedNames](#def-localizednames); `"object"`; additionalProperties: `"string"`; minLength=`1`; propertyNames=`{"type":"string","pattern":"^(?:[A-Za-z]{2,3}\|[A-Za-z]{5,8})(?:-[A-Za-z0-9]{2,8})*$"}` | 言語タグ別の翻訳表示名。元のnameが必ず残る。 |

<a id="def-tempo"></a>

## tempo

そのtick以後のテンポ。BPMは拍子によらず四分音符毎分。

Schema: `#/$defs/tempo`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.timeline.tempoChanges[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `at`<br>`#/$defs/tempo/properties/at` | 必須 | [nonnegative](#def-nonnegative); `"integer"`; minimum=`0`; maximum=`9007199254740991` | 曲全体の変更tick。各変更配列は0から始まり厳密昇順。 |
| `bpm`<br>`#/$defs/tempo/properties/bpm` | 必須 | `"number"`; exclusiveMinimum=`0`; maximum=`1000` | 四分音符毎分。0より大きく1000以下の有限数。 |

<a id="def-meter"></a>

## meter

そのtick以後の拍子。変更点を暗黙の小節境界へ移動しない。

Schema: `#/$defs/meter`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.timeline.meterChanges[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `at`<br>`#/$defs/meter/properties/at` | 必須 | [nonnegative](#def-nonnegative); `"integer"`; minimum=`0`; maximum=`9007199254740991` | 曲全体の変更tick。各変更配列は0から始まり厳密昇順。 |
| `numerator`<br>`#/$defs/meter/properties/numerator` | 必須 | `"integer"`; minimum=`1`; maximum=`64` | 拍子の分子。 |
| `denominator`<br>`#/$defs/meter/properties/denominator` | 必須 | `"integer"`; enum=`[1,2,4,8,16,32,64]` | 拍子の分母。列挙された2の累乗だけを使用。 |

<a id="def-timeline"></a>

## timeline

曲構成、テンポ変更、拍子変更の配列。

Schema: `#/$defs/timeline`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.timeline`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `sections`<br>`#/$defs/timeline/properties/sections` | 必須 | `"array"`; items: [section](#def-section); `"object"`; 追加キー禁止 | 非重複・開始位置順の構成区間。空・隙間を許す。 |
| `tempoChanges`<br>`#/$defs/timeline/properties/tempoChanges` | 必須 | `"array"`; minItems=`1`; items: [tempo](#def-tempo); `"object"`; 追加キー禁止 | tick 0から始まるテンポの区分一定変更列。 |
| `meterChanges`<br>`#/$defs/timeline/properties/meterChanges` | 必須 | `"array"`; minItems=`1`; items: [meter](#def-meter); `"object"`; 追加キー禁止 | tick 0から始まる拍子変更列。 |

<a id="def-chord"></a>

## chord

和音の意味情報。labelだけでも有効で、演奏ボイシングを生成しない。

Schema: `#/$defs/chord`

`"object"`; 追加キー禁止; dependentRequired（下記構造規則）.

使用箇所（構造上のパス）:

- `$.harmony.chords[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/chord/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | このレコードのID。適用される一意性の範囲は型の説明を参照。 |
| `start`<br>`#/$defs/chord/properties/start` | 必須 | [nonnegative](#def-nonnegative); `"integer"`; minimum=`0`; maximum=`9007199254740991` | 開始tick。座標系はこの型の説明を参照。 |
| `duration`<br>`#/$defs/chord/properties/duration` | 必須 | [positive](#def-positive); `"integer"`; minimum=`1`; maximum=`9007199254740991` | 正の長さtick。終了位置の加算にも意味上の上限がある。 |
| `label`<br>`#/$defs/chord/properties/label` | 必須 | `"string"`; minLength=`1` | 必須の空でない表示コード名。非構造的な文字列だけでも有効。 |
| `root`<br>`#/$defs/chord/properties/root` | 任意；intervalsがある場合は必須 | [spelledPitchClass](#def-spelledpitchclass); `"object"`; 追加キー禁止 | 綴りを保持する根音。intervalsと同時に指定。 |
| `intervals`<br>`#/$defs/chord/properties/intervals` | 任意；rootがある場合は必須 | `"array"`; minItems=`1`; maxItems=`36`; uniqueItems=`true`; items: `"integer"`; minimum=`0`; maximum=`35`; contains=`{"const":0}` | 根音または主音からの半音差。0を含み、厳密昇順・重複なし。 |
| `bass`<br>`#/$defs/chord/properties/bass` | 任意 | [spelledPitchClass](#def-spelledpitchclass); `"object"`; 追加キー禁止 | 任意の綴り付きベース音名。低音ノートを生成しない。 |

構造・分岐規則（Schema原文）:

```json
{
  "dependentRequired": {
    "root": [
      "intervals"
    ],
    "intervals": [
      "root"
    ]
  }
}
```

<a id="def-scale"></a>

## scale

音階の意味情報。Coreノートの使用可能音を制限しない。

Schema: `#/$defs/scale`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.harmony.scales[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/scale/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | このレコードのID。適用される一意性の範囲は型の説明を参照。 |
| `start`<br>`#/$defs/scale/properties/start` | 必須 | [nonnegative](#def-nonnegative); `"integer"`; minimum=`0`; maximum=`9007199254740991` | 開始tick。座標系はこの型の説明を参照。 |
| `duration`<br>`#/$defs/scale/properties/duration` | 必須 | [positive](#def-positive); `"integer"`; minimum=`1`; maximum=`9007199254740991` | 正の長さtick。終了位置の加算にも意味上の上限がある。 |
| `label`<br>`#/$defs/scale/properties/label` | 任意 | `"string"` | 任意の表示用音階名。 |
| `tonic`<br>`#/$defs/scale/properties/tonic` | 必須 | [spelledPitchClass](#def-spelledpitchclass); `"object"`; 追加キー禁止 | 綴りを保持する主音。 |
| `intervals`<br>`#/$defs/scale/properties/intervals` | 必須 | `"array"`; minItems=`1`; maxItems=`12`; uniqueItems=`true`; items: `"integer"`; minimum=`0`; maximum=`11`; contains=`{"const":0}` | 根音または主音からの半音差。0を含み、厳密昇順・重複なし。 |

<a id="def-harmony"></a>

## harmony

和音と音階の配列。演奏はCoreノートとして別に保存する。

Schema: `#/$defs/harmony`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.harmony`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `chords`<br>`#/$defs/harmony/properties/chords` | 必須 | `"array"`; items: [chord](#def-chord); `"object"`; 追加キー禁止; dependentRequired（下記構造規則） | 開始位置順の和音区間。重なりを許す。 |
| `scales`<br>`#/$defs/harmony/properties/scales` | 必須 | `"array"`; items: [scale](#def-scale); `"object"`; 追加キー禁止 | 開始位置順の音階区間。重なりを許す。 |

<a id="def-instrument"></a>

## instrument

楽器の表示情報。プラグイン状態や音源を指定する契約ではない。

Schema: `#/$defs/instrument`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.tracks[*].instrument`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `name`<br>`#/$defs/instrument/properties/name` | 必須 | `"string"` | 表示名。IDの代用にはしない。 |
| `family`<br>`#/$defs/instrument/properties/family` | 任意 | `"string"` | 任意の楽器群の説明。固定分類ではない。 |
| `localizedNames`<br>`#/$defs/instrument/properties/localizedNames` | 任意 | [localizedNames](#def-localizednames); `"object"`; additionalProperties: `"string"`; minLength=`1`; propertyNames=`{"type":"string","pattern":"^(?:[A-Za-z]{2,3}\|[A-Za-z]{5,8})(?:-[A-Za-z0-9]{2,8})*$"}` | 言語タグ別の翻訳表示名。元のnameが必ず残る。 |

<a id="def-note"></a>

## note

実演奏Coreノート。発音対象・局所開始・ゲートと任意のNote On Velocity（1～127）。原型phrase sourceとは別定義。

Schema: `#/$defs/note`

`"object"`; 追加キー禁止; oneOf（下記構造規則）.

使用箇所（構造上のパス）:

- `$.tracks[*].clips[*].notes[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/note/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | Coreでは文書全体で一意。template内ではそのtemplateだけで一意。 |
| `start`<br>`#/$defs/note/properties/start` | 必須 | [signed](#def-signed); `"integer"`; minimum=`-9007199254740991`; maximum=`9007199254740991` | 親clipまたはtemplateの開始に対する符号付きtick。 |
| `duration`<br>`#/$defs/note/properties/duration` | 必須 | [positive](#def-positive); `"integer"`; minimum=`1`; maximum=`9007199254740991` | 発音を保持するゲート長。音源のrelease尾部や記譜音価ではない。 |
| `pitch`<br>`#/$defs/note/properties/pitch` | pitch/soundSlotIdの一方だけ必須 | [pitch](#def-pitch); `"integer"`; minimum=`0`; maximum=`127` | 0〜127の半音番号。60=C4。soundSlotIdとの二者択一。 |
| `soundSlotId`<br>`#/$defs/note/properties/soundSlotId` | pitch/soundSlotIdの一方だけ必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | Core soundSlotのID。pitchとの二者択一。 |
| `velocity`<br>`#/$defs/note/properties/velocity` | 任意 | `"integer"`; minimum=`1`; maximum=`127` | 実演奏Coreノートだけに付ける任意のNote On Velocity（JSON整数1～127）。省略時は省略を保持。 |

構造・分岐規則（Schema原文）:

```json
{
  "oneOf": [
    {
      "required": [
        "pitch"
      ],
      "not": {
        "required": [
          "soundSlotId"
        ]
      }
    },
    {
      "required": [
        "soundSlotId"
      ],
      "not": {
        "required": [
          "pitch"
        ]
      }
    }
  ]
}
```

<a id="def-clip"></a>

## clip

トラック上の配置・編集単位。durationはノートを切るマスクではない。

Schema: `#/$defs/clip`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.tracks[*].clips[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/clip/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | このレコードのID。適用される一意性の範囲は型の説明を参照。 |
| `name`<br>`#/$defs/clip/properties/name` | 任意 | `"string"` | 表示名。IDの代用にはしない。 |
| `start`<br>`#/$defs/clip/properties/start` | 必須 | [nonnegative](#def-nonnegative); `"integer"`; minimum=`0`; maximum=`9007199254740991` | 曲全体の配置開始tick。 |
| `duration`<br>`#/$defs/clip/properties/duration` | 必須 | [positive](#def-positive); `"integer"`; minimum=`1`; maximum=`9007199254740991` | 配置・編集用の参照区間長。pickup・tailを切らない。 |
| `enabled`<br>`#/$defs/clip/properties/enabled` | 任意 | `"boolean"`; default=`true` | 省略時は意味上true。trackとclipが両方trueのときのみノートが有効。 |
| `notes`<br>`#/$defs/clip/properties/notes` | 必須 | `"array"`; items: [note](#def-note); `"object"`; 追加キー禁止; oneOf（下記構造規則） | 開始位置順の具体的ノート配列。同時刻では配列順を保持。 |
| `localizedNames`<br>`#/$defs/clip/properties/localizedNames` | 任意 | [localizedNames](#def-localizednames); `"object"`; additionalProperties: `"string"`; minLength=`1`; propertyNames=`{"type":"string","pattern":"^(?:[A-Za-z]{2,3}\|[A-Za-z]{5,8})(?:-[A-Za-z0-9]{2,8})*$"}` | 言語タグ別の翻訳表示名。元のnameが必ず残る。 |

<a id="def-track"></a>

## track

名前、役割、楽器説明、クリップと任意のトラック種別・表示ヒントを持つ。

Schema: `#/$defs/track`

`"object"`; 追加キー禁止; allOf（下記構造規則）.

使用箇所（構造上のパス）:

- `$.tracks[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/track/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | このレコードのID。適用される一意性の範囲は型の説明を参照。 |
| `name`<br>`#/$defs/track/properties/name` | 必須 | `"string"` | 表示名。IDの代用にはしない。 |
| `role`<br>`#/$defs/track/properties/role` | 任意 | `"string"` | 用途・役割を表す文字列。固定enumではない。 |
| `instrument`<br>`#/$defs/track/properties/instrument` | 任意 | [instrument](#def-instrument); `"object"`; 追加キー禁止 | 任意の楽器表示情報。 |
| `enabled`<br>`#/$defs/track/properties/enabled` | 任意 | `"boolean"`; default=`true` | 省略時は意味上true。trackとclipが両方trueのときのみノートが有効。 |
| `clips`<br>`#/$defs/track/properties/clips` | 必須 | `"array"`; items: [clip](#def-clip); `"object"`; 追加キー禁止 | 開始位置順のclip配列。重なり・同時開始を許す。 |
| `trackType`<br>`#/$defs/track/properties/trackType` | 任意 | enum=`["melodic","drum","mixed"]` | 有音高／打楽器／混在という保存済み対象の意味区分。 |
| `preferredView`<br>`#/$defs/track/properties/preferredView` | 任意 | enum=`["auto","pianoRoll","drumGrid"]`; default=`"auto"` | 表示のみの希望。auto/pianoRoll/drumGrid。演奏は変わらない。 |
| `soundSource`<br>`#/$defs/track/properties/soundSource` | 任意 | [soundSource](#def-soundsource); `"object"`; 追加キー禁止; allOf（下記構造規則） | 楽器名と分離された再生音源の割当ヒント。実体復元の保証はない。 |
| `localizedNames`<br>`#/$defs/track/properties/localizedNames` | 任意 | [localizedNames](#def-localizednames); `"object"`; additionalProperties: `"string"`; minLength=`1`; propertyNames=`{"type":"string","pattern":"^(?:[A-Za-z]{2,3}\|[A-Za-z]{5,8})(?:-[A-Za-z0-9]{2,8})*$"}` | 言語タグ別の翻訳表示名。元のnameが必ず残る。 |
| `drumKitId`<br>`#/$defs/track/properties/drumKitId` | 任意 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | 任意のキット参照。全イベントのSlotはキットに属する必要がある。 |

構造・分岐規則（Schema原文）:

```json
{
  "allOf": [
    {
      "if": {
        "properties": {
          "trackType": {
            "const": "melodic"
          }
        },
        "required": [
          "trackType"
        ]
      },
      "then": {
        "not": {
          "required": [
            "drumKitId"
          ]
        }
      }
    }
  ]
}
```

<a id="def-soundslot"></a>

## soundSlot

打楽器の発音先。IDが同一性を持ち、MIDI番号やroleは同一性ではない。

Schema: `#/$defs/soundSlot`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.soundSlots[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/soundSlot/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | このレコードのID。適用される一意性の範囲は型の説明を参照。 |
| `name`<br>`#/$defs/soundSlot/properties/name` | 必須 | `"string"` | 表示名。IDの代用にはしない。 |
| `role`<br>`#/$defs/soundSlot/properties/role` | 任意 | `"string"` | 用途・役割を表す文字列。固定enumではない。 |
| `midiNote`<br>`#/$defs/soundSlot/properties/midiNote` | 任意 | [pitch](#def-pitch); `"integer"`; minimum=`0`; maximum=`127` | 出力変換の任意のヒント。GM準拠・同一性の宣言ではない。 |
| `midiMapping`<br>`#/$defs/soundSlot/properties/midiMapping` | 任意 | [midiMapping](#def-midimapping); `"object"`; 追加キー禁止; allOf（下記構造規則） | MIDI1へ出すときの明示割当。旧midiNoteはヒントのまま。 |
| `localizedNames`<br>`#/$defs/soundSlot/properties/localizedNames` | 任意 | [localizedNames](#def-localizednames); `"object"`; additionalProperties: `"string"`; minLength=`1`; propertyNames=`{"type":"string","pattern":"^(?:[A-Za-z]{2,3}\|[A-Za-z]{5,8})(?:-[A-Za-z0-9]{2,8})*$"}` | 言語タグ別の翻訳表示名。元のnameが必ず残る。 |

<a id="def-lyricdocument"></a>

## lyricDocument

歌詞文書の識別と補助情報。

Schema: `#/$defs/lyricDocument`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.lyrics.documents[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/lyricDocument/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | このレコードのID。適用される一意性の範囲は型の説明を参照。 |
| `title`<br>`#/$defs/lyricDocument/properties/title` | 任意 | `"string"` | 表示用の題名。 |
| `language`<br>`#/$defs/lyricDocument/properties/language` | 任意 | `"string"` | 補助的な言語文字列。形式は固定しない。 |

<a id="def-lyricphrase"></a>

## lyricPhrase

表示用の歌詞フレーズ。分割単位の連結と同じ文字列である必要はない。

Schema: `#/$defs/lyricPhrase`

`"object"`; 追加キー禁止; dependentRequired（下記構造規則）.

使用箇所（構造上のパス）:

- `$.lyrics.phrases[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/lyricPhrase/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | このレコードのID。適用される一意性の範囲は型の説明を参照。 |
| `documentId`<br>`#/$defs/lyricPhrase/properties/documentId` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | 所属するCore lyricDocumentのID。 |
| `text`<br>`#/$defs/lyricPhrase/properties/text` | 必須 | `"string"` | 表示文字列。発音表記はpronunciationに分離する。 |
| `pronunciation`<br>`#/$defs/lyricPhrase/properties/pronunciation` | 任意 | `"string"` | 発音の補助文字列。音素体系や歌唱エンジンは規定しない。 |
| `start`<br>`#/$defs/lyricPhrase/properties/start` | 任意；durationがある場合は必須 | [nonnegative](#def-nonnegative); `"integer"`; minimum=`0`; maximum=`9007199254740991` | 任意のグローバル開始tick。durationと同時に指定。 |
| `duration`<br>`#/$defs/lyricPhrase/properties/duration` | 任意；startがある場合は必須 | [positive](#def-positive); `"integer"`; minimum=`1`; maximum=`9007199254740991` | 任意の区間長。startと同時に指定。 |

構造・分岐規則（Schema原文）:

```json
{
  "dependentRequired": {
    "start": [
      "duration"
    ],
    "duration": [
      "start"
    ]
  }
}
```

<a id="def-lyricunit"></a>

## lyricUnit

歌詞の分割・対応づけの単位。

Schema: `#/$defs/lyricUnit`

`"object"`; 追加キー禁止; dependentRequired（下記構造規則）.

使用箇所（構造上のパス）:

- `$.lyrics.units[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/lyricUnit/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | このレコードのID。適用される一意性の範囲は型の説明を参照。 |
| `phraseId`<br>`#/$defs/lyricUnit/properties/phraseId` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | 所属するCore lyricPhraseのID。 |
| `text`<br>`#/$defs/lyricUnit/properties/text` | 必須 | `"string"` | 表示文字列。発音表記はpronunciationに分離する。 |
| `pronunciation`<br>`#/$defs/lyricUnit/properties/pronunciation` | 任意 | `"string"` | 発音の補助文字列。音素体系や歌唱エンジンは規定しない。 |
| `start`<br>`#/$defs/lyricUnit/properties/start` | 任意；durationがある場合は必須 | [nonnegative](#def-nonnegative); `"integer"`; minimum=`0`; maximum=`9007199254740991` | 任意のグローバル開始tick。durationと同時に指定。 |
| `duration`<br>`#/$defs/lyricUnit/properties/duration` | 任意；startがある場合は必須 | [positive](#def-positive); `"integer"`; minimum=`1`; maximum=`9007199254740991` | 任意の区間長。startと同時に指定。 |

構造・分岐規則（Schema原文）:

```json
{
  "dependentRequired": {
    "start": [
      "duration"
    ],
    "duration": [
      "start"
    ]
  }
}
```

<a id="def-lyricalignment"></a>

## lyricAlignment

歌詞単位とCoreノートの順序付き多対多対応。

Schema: `#/$defs/lyricAlignment`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.lyrics.alignments[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/lyricAlignment/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | このレコードのID。適用される一意性の範囲は型の説明を参照。 |
| `unitIds`<br>`#/$defs/lyricAlignment/properties/unitIds` | 必須 | `"array"`; minItems=`1`; uniqueItems=`true`; items: [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | 空でなく重複のない、順序付きCore lyricUnit ID列。 |
| `noteIds`<br>`#/$defs/lyricAlignment/properties/noteIds` | 必須 | `"array"`; minItems=`1`; uniqueItems=`true`; items: [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | 空でなく重複のない、順序付きCore note ID列。 |

<a id="def-lyrics"></a>

## lyrics

歌詞文書、フレーズ、単位、対応の四配列。

Schema: `#/$defs/lyrics`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.lyrics`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `documents`<br>`#/$defs/lyrics/properties/documents` | 必須 | `"array"`; items: [lyricDocument](#def-lyricdocument); `"object"`; 追加キー禁止 | 歌詞文書配列。 |
| `phrases`<br>`#/$defs/lyrics/properties/phrases` | 必須 | `"array"`; items: [lyricPhrase](#def-lyricphrase); `"object"`; 追加キー禁止; dependentRequired（下記構造規則） | 歌詞フレーズ配列。 |
| `units`<br>`#/$defs/lyrics/properties/units` | 必須 | `"array"`; items: [lyricUnit](#def-lyricunit); `"object"`; 追加キー禁止; dependentRequired（下記構造規則） | 歌詞単位配列。 |
| `alignments`<br>`#/$defs/lyrics/properties/alignments` | 必須 | `"array"`; items: [lyricAlignment](#def-lyricalignment); `"object"`; 追加キー禁止 | 歌詞単位とノートの対応配列。 |

<a id="def-sha256"></a>

## sha256

小文字16進数64桁のSHA-256値。

Schema: `#/$defs/sha256`

`"string"`; pattern=`"^[0-9a-f]{64}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}`.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.legacy-import.v1"].data.sourceSha256`
- `$.resources[*].sha256`

構造・分岐規則（Schema原文）:

```json
{
  "not": {
    "pattern": "[\\r\\n\\u2028\\u2029]"
  }
}
```

<a id="def-resource"></a>

## resource

生成素材などへの参照。読込時の取得・実行・音声再生指示ではない。

Schema: `#/$defs/resource`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.resources[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/resource/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | このレコードのID。適用される一意性の範囲は型の説明を参照。 |
| `kind`<br>`#/$defs/resource/properties/kind` | 必須 | enum=`["audio","midi","text","other"]` | 参照素材の種別。再生動作は指定しない。 |
| `uri`<br>`#/$defs/resource/properties/uri` | 必須 | `"string"`; minLength=`1` | 空でない参照文字列。読込時には解決・取得しない。 |
| `name`<br>`#/$defs/resource/properties/name` | 任意 | `"string"` | 表示名。IDの代用にはしない。 |
| `sha256`<br>`#/$defs/resource/properties/sha256` | 任意 | [sha256](#def-sha256); `"string"`; pattern=`"^[0-9a-f]{64}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | 参照素材に対する任意のSHA-256。照合は明示的操作。 |

<a id="def-dependencies"></a>

## dependencies

拡張が依存するCoreの範囲。二つのoneOf構造で三種類のscopeを表す。

Schema: `#/$defs/dependencies`

oneOf（下記構造規則）.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.appearance.v1"].dependencies`
- `$.extensions["org.ostf.clip-choices.v1"].dependencies`
- `$.extensions["org.ostf.generation-context.v1"].dependencies`
- `$.extensions["org.ostf.legacy-import.v1"].dependencies`
- `$.extensions["org.ostf.phrase-library.v1"].dependencies`
- `$.extensions["org.ostf.relative-phrase.v1"].dependencies`
- `$.extensions[*].dependencies`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `scope`<br>`#/$defs/dependencies/oneOf/0/properties/scope` | 必須 | enum=`["document","none"]` | document=Core全体、none=Core依存なし、objects=明示参照。 |
| `scope`<br>`#/$defs/dependencies/oneOf/1/properties/scope` | 必須 | const=`"objects"` | document=Core全体、none=Core依存なし、objects=明示参照。 |
| `refs`<br>`#/$defs/dependencies/oneOf/1/properties/refs` | 必須 | `"array"`; minItems=`1`; uniqueItems=`true`; items: [ref](#def-ref); `"object"`; 追加キー禁止 | objects時に必須の空でない、重複なし型付き参照列。 |

構造・分岐規則（Schema原文）:

```json
{
  "oneOf": [
    {
      "type": "object",
      "properties": {
        "scope": {
          "enum": [
            "document",
            "none"
          ]
        }
      },
      "required": [
        "scope"
      ],
      "additionalProperties": false
    },
    {
      "type": "object",
      "properties": {
        "scope": {
          "const": "objects"
        },
        "refs": {
          "type": "array",
          "items": {
            "$ref": "#/$defs/ref"
          },
          "minItems": 1,
          "uniqueItems": true
        }
      },
      "required": [
        "scope",
        "refs"
      ],
      "additionalProperties": false
    }
  ]
}
```

<a id="def-extension"></a>

## extension

既知・未知のすべての拡張に共通する閉じたenvelope。

Schema: `#/$defs/extension`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.appearance.v1"]`
- `$.extensions["org.ostf.clip-choices.v1"]`
- `$.extensions["org.ostf.generation-context.v1"]`
- `$.extensions["org.ostf.legacy-import.v1"]`
- `$.extensions["org.ostf.phrase-library.v1"]`
- `$.extensions["org.ostf.relative-phrase.v1"]`
- `$.extensions[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `version`<br>`#/$defs/extension/properties/version` | 必須 | `"string"`; minLength=`1` | この対象の版。root版・profile版・生成器版は別の識別子。 |
| `status`<br>`#/$defs/extension/properties/status` | 必須 | enum=`["current","stale","unverified"]` | 現在文書との関係の状態。規格の成熟度や再生のon/offではない。 |
| `dependencies`<br>`#/$defs/extension/properties/dependencies` | 必須 | [dependencies](#def-dependencies); oneOf（下記構造規則） | Coreへの依存宣言。親の移動・無効化による影響も含む。 |
| `data`<br>`#/$defs/extension/properties/data` | 必須 | 任意のJSON値 | 未知profileでは任意JSON。既知の正確な版では各payload構造に従う。 |

<a id="def-relativeassignment"></a>

## relativeAssignment

Coreの有音高ノートと、和音・音階の構成音との対応。

Schema: `#/$defs/relativeAssignment`

`"object"`; 追加キー禁止; allOf（下記構造規則）.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.relative-phrase.v1"].data.assignments[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `noteId`<br>`#/$defs/relativeAssignment/properties/noteId` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | 対応先CoreノートのID。 |
| `basis`<br>`#/$defs/relativeAssignment/properties/basis` | 必須 | enum=`["chordTone","scaleDegree"]` | chordToneは和音構成音、scaleDegreeは音階構成音。 |
| `contextId`<br>`#/$defs/relativeAssignment/properties/contextId` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | basisに応じたCore chordまたはscaleのID。 |
| `anchorPitch`<br>`#/$defs/relativeAssignment/properties/anchorPitch` | 必須 | [pitch](#def-pitch); `"integer"`; minimum=`0`; maximum=`127` | オクターブを含む実際の根音・主音番号。 |
| `index`<br>`#/$defs/relativeAssignment/properties/index` | 必須 | `"integer"`; minimum=`1`; maximum=`36` | intervals配列内の1始まり位置。コード名称の度数番号ではない。 |
| `chromaticOffset`<br>`#/$defs/relativeAssignment/properties/chromaticOffset` | 必須 | `"integer"`; minimum=`-24`; maximum=`24` | 選んだ構成音への半音単位の補正。 |

構造・分岐規則（Schema原文）:

```json
{
  "allOf": [
    {
      "if": {
        "properties": {
          "basis": {
            "const": "scaleDegree"
          }
        },
        "required": [
          "basis"
        ]
      },
      "then": {
        "properties": {
          "index": {
            "maximum": 12
          }
        }
      }
    }
  ]
}
```

<a id="def-relativedata"></a>

## relativeData

相対音高の対応一覧。読込時にCoreを書き換えない。

Schema: `#/$defs/relativeData`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.relative-phrase.v1"].data`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `assignments`<br>`#/$defs/relativeData/properties/assignments` | 必須 | `"array"`; items: [relativeAssignment](#def-relativeassignment); `"object"`; 追加キー禁止; allOf（下記構造規則） | Core有音高ノートごとに最大1件の対応。 |

<a id="def-generator"></a>

## generator

生成器の識別子と版。アルゴリズムの再現を保証するものではない。

Schema: `#/$defs/generator`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.generation-context.v1"].data.processes[*].generator`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/generator/properties/id` | 必須 | `"string"`; minLength=`1` | 空でない生成器識別文字列。Core IDの字句制限は適用しない。 |
| `version`<br>`#/$defs/generator/properties/version` | 必須 | `"string"`; minLength=`1` | この対象の版。root版・profile版・生成器版は別の識別子。 |

<a id="def-generationinput"></a>

## generationInput

一つの入力役割、Core参照、任意の読取範囲。

Schema: `#/$defs/generationInput`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.generation-context.v1"].data.processes[*].inputs[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `role`<br>`#/$defs/generationInput/properties/role` | 必須 | `"string"`; minLength=`1` | 用途・役割を表す文字列。固定enumではない。 |
| `ref`<br>`#/$defs/generationInput/properties/ref` | 必須 | [ref](#def-ref); `"object"`; 追加キー禁止 | 型付きCore参照。 |
| `readRange`<br>`#/$defs/generationInput/properties/readRange` | 任意 | [range](#def-range); `"object"`; 追加キー禁止 | 生成時に読んだグローバル範囲。出力区間とは別。 |

<a id="def-generationprocess"></a>

## generationProcess

生成入力・出力・保護ノートなどの関係記録。

Schema: `#/$defs/generationProcess`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.generation-context.v1"].data.processes[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/generationProcess/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | このgeneration-context内で一意な工程ID。 |
| `generator`<br>`#/$defs/generationProcess/properties/generator` | 必須 | [generator](#def-generator); `"object"`; 追加キー禁止 | 生成器の識別・版情報。 |
| `inputs`<br>`#/$defs/generationProcess/properties/inputs` | 必須 | `"array"`; items: [generationInput](#def-generationinput); `"object"`; 追加キー禁止 | 空も複数も許す、役割付きの入力列。 |
| `outputs`<br>`#/$defs/generationProcess/properties/outputs` | 必須 | `"array"`; minItems=`1`; items: [ref](#def-ref); `"object"`; 追加キー禁止 | 空でない型付きCore出力参照列。 |
| `targetRange`<br>`#/$defs/generationProcess/properties/targetRange` | 任意 | [range](#def-range); `"object"`; 追加キー禁止 | 変更を要求したグローバル範囲。pickupやtailを切らない。 |
| `protectedNoteIds`<br>`#/$defs/generationProcess/properties/protectedNoteIds` | 必須 | `"array"`; uniqueItems=`true`; items: [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | 重複なしCore note ID列。操作前に比較対象を固定する。 |
| `vendorExtension`<br>`#/$defs/generationProcess/properties/vendorExtension` | 任意 | `"string"`; minLength=`1` | 同一文書内の別拡張namespace。current時はdocument依存が必須。 |

<a id="def-generationdata"></a>

## generationData

複数の生成工程の記録。

Schema: `#/$defs/generationData`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.generation-context.v1"].data`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `processes`<br>`#/$defs/generationData/properties/processes` | 必須 | `"array"`; items: [generationProcess](#def-generationprocess); `"object"`; 追加キー禁止 | 工程記録配列。 |

<a id="def-color"></a>

## color

RGB色。#に続く大文字または小文字の16進数6桁。

Schema: `#/$defs/color`

`"string"`; pattern=`"^#[0-9A-Fa-f]{6}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}`.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.appearance.v1"].data.appearance.customRoleColors[*]`
- `$.extensions["org.ostf.appearance.v1"].data.appearance.objectColors[*].color`
- `$.extensions["org.ostf.appearance.v1"].data.appearance.roleColors[*]`

構造・分岐規則（Schema原文）:

```json
{
  "not": {
    "pattern": "[\\r\\n\\u2028\\u2029]"
  }
}
```

<a id="def-roledefinition"></a>

## roleDefinition

表示用の独自セクション役割の定義。

Schema: `#/$defs/roleDefinition`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.appearance.v1"].data.roleDefinitions[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/roleDefinition/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | appearance profile内で一意な独自role ID。 |
| `name`<br>`#/$defs/roleDefinition/properties/name` | 必須 | `"string"`; minLength=`1` | 表示名。IDの代用にはしない。 |
| `baseRole`<br>`#/$defs/roleDefinition/properties/baseRole` | 任意 | `"string"` | 任意の基本role文字列。 |

<a id="def-rolecolormap"></a>

## roleColorMap

任意のrole文字列からRGB色への辞書。

Schema: `#/$defs/roleColorMap`

`"object"`; additionalProperties: [color](#def-color); `"string"`; pattern=`"^#[0-9A-Fa-f]{6}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}`.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.appearance.v1"].data.appearance.roleColors`

構造・分岐規則（Schema原文）:

```json
{
  "additionalProperties": {
    "$ref": "#/$defs/color"
  }
}
```

<a id="def-customrolecolormap"></a>

## customRoleColorMap

定義済み独自role IDからRGB色への辞書。

Schema: `#/$defs/customRoleColorMap`

`"object"`; additionalProperties: [color](#def-color); `"string"`; pattern=`"^#[0-9A-Fa-f]{6}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}`; propertyNames=`{"$ref":"#/$defs/id"}`.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.appearance.v1"].data.appearance.customRoleColors`

構造・分岐規則（Schema原文）:

```json
{
  "propertyNames": {
    "$ref": "#/$defs/id"
  },
  "additionalProperties": {
    "$ref": "#/$defs/color"
  }
}
```

<a id="def-objectcolor"></a>

## objectColor

型付きCore参照に対する個別色。

Schema: `#/$defs/objectColor`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.appearance.v1"].data.appearance.objectColors[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `target`<br>`#/$defs/objectColor/properties/target` | 必須 | [ref](#def-ref); `"object"`; 追加キー禁止 | 色を指定するCore対象の型付き参照。 |
| `color`<br>`#/$defs/objectColor/properties/color` | 必須 | [color](#def-color); `"string"`; pattern=`"^#[0-9A-Fa-f]{6}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | 個別RGB色。 |

<a id="def-appearancedata"></a>

## appearanceData

独自役割、セクションへの割当、色の表示情報。演奏には影響しない。

Schema: `#/$defs/appearanceData`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.appearance.v1"].data`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `roleDefinitions`<br>`#/$defs/appearanceData/properties/roleDefinitions` | 必須 | `"array"`; items: [roleDefinition](#def-roledefinition); `"object"`; 追加キー禁止 | 独自roleの定義配列。 |
| `sectionRoleAssignments`<br>`#/$defs/appearanceData/properties/sectionRoleAssignments` | 必須 | `"object"`; additionalProperties: [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}`; propertyNames=`{"$ref":"#/$defs/id"}` | Core section IDをキー、独自role IDを値とする辞書。 |
| `appearance`<br>`#/$defs/appearanceData/properties/appearance` | 必須 | `"object"`; 追加キー禁止 | role・独自role・対象別の色指定。 |
| `roleColors`<br>`#/$defs/appearanceData/properties/appearance/properties/roleColors` | 必須 | [roleColorMap](#def-rolecolormap); `"object"`; additionalProperties: [color](#def-color); `"string"`; pattern=`"^#[0-9A-Fa-f]{6}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | 任意のrole文字列に対応する色辞書。 |
| `customRoleColors`<br>`#/$defs/appearanceData/properties/appearance/properties/customRoleColors` | 必須 | [customRoleColorMap](#def-customrolecolormap); `"object"`; additionalProperties: [color](#def-color); `"string"`; pattern=`"^#[0-9A-Fa-f]{6}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}`; propertyNames=`{"$ref":"#/$defs/id"}` | 定義した独自role IDに対応する色辞書。 |
| `objectColors`<br>`#/$defs/appearanceData/properties/appearance/properties/objectColors` | 必須 | `"array"`; items: [objectColor](#def-objectcolor); `"object"`; 追加キー禁止 | 対象別の色指定配列。 |

内側のオブジェクト `#/$defs/appearanceData/properties/appearance`:

```json
{
  "type": "object",
  "required": [
    "roleColors",
    "customRoleColors",
    "objectColors"
  ],
  "additionalProperties": false
}
```

<a id="def-legacydata"></a>

## legacyData

2.3原文とSHA-256、移行記録の保存。Coreを書き戻す指示ではない。

Schema: `#/$defs/legacyData`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.legacy-import.v1"].data`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `sourceVersion`<br>`#/$defs/legacyData/properties/sourceVersion` | 必須 | const=`"2.3.0"` | 保存した原文の版。正確に2.3.0。 |
| `sourceSha256`<br>`#/$defs/legacyData/properties/sourceSha256` | 必須 | [sha256](#def-sha256); `"string"`; pattern=`"^[0-9a-f]{64}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | sourceTextのUTF-8バイト列に対するSHA-256。 |
| `sourceText`<br>`#/$defs/legacyData/properties/sourceText` | 必須 | `"string"`; minLength=`1` | 元の2.3 JSON全文。空白と文字列を含む原文を保存。 |
| `conversionReport`<br>`#/$defs/legacyData/properties/conversionReport` | 必須 | `"object"` | 移行の対応・損失等の記録。内部項目はこのprofileでは固定しない。 |

<a id="def-extensions"></a>

## extensions

namespaceをキーに持つ拡張辞書。正確なnamespaceと版でpayload構造を選ぶ。

Schema: `#/$defs/extensions`

`"object"`; additionalProperties: [extension](#def-extension); `"object"`; 追加キー禁止; propertyNames=`{"pattern":"^[a-z][a-z0-9-]*(?:\\.[a-z][a-z0-9-]*){2,}$","not":{"pattern":"[\\r\\n\\u2028\\u2029]"}}`.

使用箇所（構造上のパス）:

- `$.extensions`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `org.ostf.relative-phrase.v1`<br>`#/$defs/extensions/properties/org.ostf.relative-phrase.v1` | 任意 | allOf（下記構造規則） | このnamespaceの任意profile。既知payloadを解釈する版は1.0.0-draft.1。 |
| `org.ostf.generation-context.v1`<br>`#/$defs/extensions/properties/org.ostf.generation-context.v1` | 任意 | allOf（下記構造規則） | このnamespaceの任意profile。既知payloadを解釈する版は1.0.0-draft.1。 |
| `org.ostf.appearance.v1`<br>`#/$defs/extensions/properties/org.ostf.appearance.v1` | 任意 | allOf（下記構造規則） | このnamespaceの任意profile。既知payloadを解釈する版は1.0.0-draft.1。 |
| `org.ostf.legacy-import.v1`<br>`#/$defs/extensions/properties/org.ostf.legacy-import.v1` | 任意 | allOf（下記構造規則） | このnamespaceの任意profile。既知payloadを解釈する版は1.0.0-draft.1。 |
| `org.ostf.phrase-library.v1`<br>`#/$defs/extensions/properties/org.ostf.phrase-library.v1` | 任意 | allOf（下記構造規則） | このnamespaceの任意profile。既知payloadを解釈する版は1.0.0-draft.1。 |
| `org.ostf.clip-choices.v1`<br>`#/$defs/extensions/properties/org.ostf.clip-choices.v1` | 任意 | allOf（下記構造規則） | このnamespaceの任意profile。既知payloadを解釈する版は1.0.0-draft.1。 |

構造・分岐規則（Schema原文）:

```json
{
  "propertyNames": {
    "pattern": "^[a-z][a-z0-9-]*(?:\\.[a-z][a-z0-9-]*){2,}$",
    "not": {
      "pattern": "[\\r\\n\\u2028\\u2029]"
    }
  },
  "additionalProperties": {
    "$ref": "#/$defs/extension"
  }
}
```

フィールド内の分岐 `#/$defs/extensions/properties/org.ostf.relative-phrase.v1`:

```json
{
  "allOf": [
    {
      "$ref": "#/$defs/extension"
    },
    {
      "if": {
        "properties": {
          "version": {
            "const": "1.0.0-draft.1"
          }
        },
        "required": [
          "version"
        ]
      },
      "then": {
        "properties": {
          "data": {
            "$ref": "#/$defs/relativeData"
          }
        }
      }
    }
  ]
}
```

フィールド内の分岐 `#/$defs/extensions/properties/org.ostf.generation-context.v1`:

```json
{
  "allOf": [
    {
      "$ref": "#/$defs/extension"
    },
    {
      "if": {
        "properties": {
          "version": {
            "const": "1.0.0-draft.1"
          }
        },
        "required": [
          "version"
        ]
      },
      "then": {
        "properties": {
          "data": {
            "$ref": "#/$defs/generationData"
          }
        }
      }
    }
  ]
}
```

フィールド内の分岐 `#/$defs/extensions/properties/org.ostf.appearance.v1`:

```json
{
  "allOf": [
    {
      "$ref": "#/$defs/extension"
    },
    {
      "if": {
        "properties": {
          "version": {
            "const": "1.0.0-draft.1"
          }
        },
        "required": [
          "version"
        ]
      },
      "then": {
        "properties": {
          "data": {
            "$ref": "#/$defs/appearanceData"
          }
        }
      }
    }
  ]
}
```

フィールド内の分岐 `#/$defs/extensions/properties/org.ostf.legacy-import.v1`:

```json
{
  "allOf": [
    {
      "$ref": "#/$defs/extension"
    },
    {
      "if": {
        "properties": {
          "version": {
            "const": "1.0.0-draft.1"
          }
        },
        "required": [
          "version"
        ]
      },
      "then": {
        "properties": {
          "data": {
            "$ref": "#/$defs/legacyData"
          }
        }
      }
    }
  ]
}
```

フィールド内の分岐 `#/$defs/extensions/properties/org.ostf.phrase-library.v1`:

```json
{
  "allOf": [
    {
      "$ref": "#/$defs/extension"
    },
    {
      "if": {
        "properties": {
          "version": {
            "const": "1.0.0-draft.1"
          }
        },
        "required": [
          "version"
        ]
      },
      "then": {
        "properties": {
          "data": {
            "$ref": "#/$defs/phraseLibraryData"
          }
        }
      }
    }
  ]
}
```

フィールド内の分岐 `#/$defs/extensions/properties/org.ostf.clip-choices.v1`:

```json
{
  "allOf": [
    {
      "$ref": "#/$defs/extension"
    },
    {
      "if": {
        "properties": {
          "version": {
            "const": "1.0.0-draft.1"
          }
        },
        "required": [
          "version"
        ]
      },
      "then": {
        "properties": {
          "data": {
            "$ref": "#/$defs/clipChoicesData"
          }
        }
      }
    }
  ]
}
```

内側のオブジェクト `#/$defs/extensions/properties/org.ostf.relative-phrase.v1/allOf/1/if`:

```json
{
  "required": [
    "version"
  ]
}
```

内側のオブジェクト `#/$defs/extensions/properties/org.ostf.relative-phrase.v1/allOf/1/then`:

```json
{}
```

内側のオブジェクト `#/$defs/extensions/properties/org.ostf.generation-context.v1/allOf/1/if`:

```json
{
  "required": [
    "version"
  ]
}
```

内側のオブジェクト `#/$defs/extensions/properties/org.ostf.generation-context.v1/allOf/1/then`:

```json
{}
```

内側のオブジェクト `#/$defs/extensions/properties/org.ostf.appearance.v1/allOf/1/if`:

```json
{
  "required": [
    "version"
  ]
}
```

内側のオブジェクト `#/$defs/extensions/properties/org.ostf.appearance.v1/allOf/1/then`:

```json
{}
```

内側のオブジェクト `#/$defs/extensions/properties/org.ostf.legacy-import.v1/allOf/1/if`:

```json
{
  "required": [
    "version"
  ]
}
```

内側のオブジェクト `#/$defs/extensions/properties/org.ostf.legacy-import.v1/allOf/1/then`:

```json
{}
```

内側のオブジェクト `#/$defs/extensions/properties/org.ostf.phrase-library.v1/allOf/1/if`:

```json
{
  "required": [
    "version"
  ]
}
```

内側のオブジェクト `#/$defs/extensions/properties/org.ostf.phrase-library.v1/allOf/1/then`:

```json
{}
```

内側のオブジェクト `#/$defs/extensions/properties/org.ostf.clip-choices.v1/allOf/1/if`:

```json
{
  "required": [
    "version"
  ]
}
```

内側のオブジェクト `#/$defs/extensions/properties/org.ostf.clip-choices.v1/allOf/1/then`:

```json
{}
```

<a id="def-phrasetemplate"></a>

## phraseTemplate

再利用する具体的ノート列。durationは反復周期。

Schema: `#/$defs/phraseTemplate`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.phrase-library.v1"].data.templates[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/phraseTemplate/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | このlibrary内で一意なtemplate ID。Core IDではない。 |
| `duration`<br>`#/$defs/phraseTemplate/properties/duration` | 必須 | [positive](#def-positive); `"integer"`; minimum=`1`; maximum=`9007199254740991` | 正の反復周期tick。ノートのゲートを切らない。 |
| `notes`<br>`#/$defs/phraseTemplate/properties/notes` | 必須 | `"array"`; items: [phraseSourceNote](#def-phrasesourcenote); `"object"`; 追加キー禁止; oneOf（下記構造規則） | 開始位置順の具体的ノート配列。同時刻では配列順を保持。 |
| `name`<br>`#/$defs/phraseTemplate/properties/name` | 任意 | `"string"` | 表示名。IDの代用にはしない。 |

<a id="def-phrasenotemapping"></a>

## phraseNoteMapping

source noteと反復番号から、実体化済みCoreノートへの対応。

Schema: `#/$defs/phraseNoteMapping`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.phrase-library.v1"].data.instances[*].noteMap[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `templateNoteId`<br>`#/$defs/phraseNoteMapping/properties/templateNoteId` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | 参照template内のsource note ID。 |
| `repeatIndex`<br>`#/$defs/phraseNoteMapping/properties/repeatIndex` | 必須 | [nonnegative](#def-nonnegative); `"integer"`; minimum=`0`; maximum=`9007199254740991` | 0始まりの反復番号。current時はrepeatCount未満。 |
| `noteId`<br>`#/$defs/phraseNoteMapping/properties/noteId` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | 対応先CoreノートのID。 |

<a id="def-phraseinstance"></a>

## phraseInstance

templateと一つのCore clipの完全対応。

Schema: `#/$defs/phraseInstance`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.phrase-library.v1"].data.instances[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/phraseInstance/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | このlibrary内で一意なinstance ID。 |
| `templateId`<br>`#/$defs/phraseInstance/properties/templateId` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | 同じphrase-library内のtemplate ID。Core IDではない。 |
| `clipId`<br>`#/$defs/phraseInstance/properties/clipId` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | 対応するCore clipのID。 |
| `repeatCount`<br>`#/$defs/phraseInstance/properties/repeatCount` | 必須 | [positive](#def-positive); `"integer"`; minimum=`1`; maximum=`9007199254740991` | 有限の反復回数。空templateでも正整数。 |
| `transpose`<br>`#/$defs/phraseInstance/properties/transpose` | 必須 | `"integer"`; minimum=`-127`; maximum=`127` | 有音高ノートの半音移調量。打楽器slotは変更しない。 |
| `noteMap`<br>`#/$defs/phraseInstance/properties/noteMap` | 必須 | `"array"`; items: [phraseNoteMapping](#def-phrasenotemapping); `"object"`; 追加キー禁止 | 全source note×反復と全clip noteを一対一に結ぶ対応。 |

<a id="def-phraselibrarydata"></a>

## phraseLibraryData

具体的phrase templatesと実体化済みinstances。読込時に展開しない。

Schema: `#/$defs/phraseLibraryData`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.phrase-library.v1"].data`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `templates`<br>`#/$defs/phraseLibraryData/properties/templates` | 必須 | `"array"`; items: [phraseTemplate](#def-phrasetemplate); `"object"`; 追加キー禁止 | 再利用する具体的phrase配列。 |
| `instances`<br>`#/$defs/phraseLibraryData/properties/instances` | 必須 | `"array"`; items: [phraseInstance](#def-phraseinstance); `"object"`; 追加キー禁止 | 実体化済みCore clipsへの対応配列。 |

<a id="def-clipcandidate"></a>

## clipCandidate

候補の局所IDと、その候補で有効にするCore clips。

Schema: `#/$defs/clipCandidate`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.clip-choices.v1"].data.groups[*].candidates[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/clipCandidate/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | 所属group内で一意なcandidate ID。 |
| `clipIds`<br>`#/$defs/clipCandidate/properties/clipIds` | 必須 | `"array"`; uniqueItems=`true`; items: [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | 候補が使う重複なしCore clip ID列。空候補も許す。 |
| `name`<br>`#/$defs/clipCandidate/properties/name` | 任意 | `"string"` | 表示名。IDの代用にはしない。 |

<a id="def-clipchoicegroup"></a>

## clipChoiceGroup

候補群と保存済み選択。Coreのenabled状態との一致を記録する。

Schema: `#/$defs/clipChoiceGroup`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.clip-choices.v1"].data.groups[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/clipChoiceGroup/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | このclip-choices内で一意なgroup ID。 |
| `candidates`<br>`#/$defs/clipChoiceGroup/properties/candidates` | 必須 | `"array"`; minItems=`1`; items: [clipCandidate](#def-clipcandidate); `"object"`; 追加キー禁止 | 1件以上の候補。 |
| `selectedCandidateId`<br>`#/$defs/clipChoiceGroup/properties/selectedCandidateId` | 必須 | anyOf（下記構造規則） | 選択した局所candidate ID、または未選択を表すnull。省略不可。 |
| `name`<br>`#/$defs/clipChoiceGroup/properties/name` | 任意 | `"string"` | 表示名。IDの代用にはしない。 |

フィールド内の分岐 `#/$defs/clipChoiceGroup/properties/selectedCandidateId`:

```json
{
  "anyOf": [
    {
      "$ref": "#/$defs/id"
    },
    {
      "type": "null"
    }
  ]
}
```

<a id="def-clipchoicesdata"></a>

## clipChoicesData

独立したクリップ選択グループの配列。

Schema: `#/$defs/clipChoicesData`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.clip-choices.v1"].data`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `groups`<br>`#/$defs/clipChoicesData/properties/groups` | 必須 | `"array"`; items: [clipChoiceGroup](#def-clipchoicegroup); `"object"`; 追加キー禁止 | 選択グループ配列。別group間のclip管理範囲は重ねない。 |

<a id="def-midimapping"></a>

## midiMapping

gm1またはcustomの明示的MIDI1ノート割当。

Schema: `#/$defs/midiMapping`

`"object"`; 追加キー禁止; allOf（下記構造規則）.

使用箇所（構造上のパス）:

- `$.soundSlots[*].midiMapping`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `standard`<br>`#/$defs/midiMapping/properties/standard` | 必須 | enum=`["gm1","custom"]` | gm1は35–81のみ、customは0–127。 |
| `note`<br>`#/$defs/midiMapping/properties/note` | 必須 | [pitch](#def-pitch); `"integer"`; minimum=`0`; maximum=`127` | 整数MIDIノート番号。両方のhintがあれば値は一致。 |

構造・分岐規則（Schema原文）:

```json
{
  "allOf": [
    {
      "if": {
        "properties": {
          "standard": {
            "const": "gm1"
          }
        },
        "required": [
          "standard"
        ]
      },
      "then": {
        "properties": {
          "note": {
            "type": "integer",
            "minimum": 35,
            "maximum": 81
          }
        }
      }
    }
  ]
}
```

<a id="def-soundsource"></a>

## soundSource

任意の音源割当ヒント。音色再現・プラグイン復元は保証しない。

Schema: `#/$defs/soundSource`

`"object"`; 追加キー禁止; allOf（下記構造規則）.

使用箇所（構造上のパス）:

- `$.tracks[*].soundSource`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `kind`<br>`#/$defs/soundSource/properties/kind` | 必須 | enum=`["unassigned","gm1","externalMidi","plugin","hostManaged"]` | unassigned/gm1/externalMidi/plugin/hostManagedの選択ヒント。 |
| `identifier`<br>`#/$defs/soundSource/properties/identifier` | 任意 | `"string"`; minLength=`1` | 不透明な音源識別名。URIでも取得・実行を自動では行わない。 |

構造・分岐規則（Schema原文）:

```json
{
  "allOf": [
    {
      "if": {
        "properties": {
          "kind": {
            "enum": [
              "gm1",
              "unassigned"
            ]
          }
        },
        "required": [
          "kind"
        ]
      },
      "then": {
        "not": {
          "required": [
            "identifier"
          ]
        }
      }
    }
  ]
}
```

<a id="def-localizednames"></a>

## localizedNames

言語タグをキーとする任意の多言語表示名の辞書。元の名前は変更しない。

Schema: `#/$defs/localizedNames`

`"object"`; additionalProperties: `"string"`; minLength=`1`; propertyNames=`{"type":"string","pattern":"^(?:[A-Za-z]{2,3}\|[A-Za-z]{5,8})(?:-[A-Za-z0-9]{2,8})*$"}`.

使用箇所（構造上のパス）:

- `$.drumKits[*].localizedNames`
- `$.song.localizedTitles`
- `$.soundSlots[*].localizedNames`
- `$.timeline.sections[*].localizedNames`
- `$.tracks[*].clips[*].localizedNames`
- `$.tracks[*].instrument.localizedNames`
- `$.tracks[*].localizedNames`

構造・分岐規則（Schema原文）:

```json
{
  "propertyNames": {
    "type": "string",
    "pattern": "^(?:[A-Za-z]{2,3}|[A-Za-z]{5,8})(?:-[A-Za-z0-9]{2,8})*$"
  },
  "additionalProperties": {
    "type": "string",
    "minLength": 1
  }
}
```

<a id="def-drumkit"></a>

## drumKit

名前付きの順序付きグローバルSound Slot参照集合。音源やGMプログラムではない。

Schema: `#/$defs/drumKit`

`"object"`; 追加キー禁止.

使用箇所（構造上のパス）:

- `$.drumKits[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/drumKit/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | このレコードのID。適用される一意性の範囲は型の説明を参照。 |
| `name`<br>`#/$defs/drumKit/properties/name` | 必須 | `"string"` | 表示名。IDの代用にはしない。 |
| `localizedNames`<br>`#/$defs/drumKit/properties/localizedNames` | 任意 | [localizedNames](#def-localizednames); `"object"`; additionalProperties: `"string"`; minLength=`1`; propertyNames=`{"type":"string","pattern":"^(?:[A-Za-z]{2,3}\|[A-Za-z]{5,8})(?:-[A-Za-z0-9]{2,8})*$"}` | 言語タグ別の翻訳表示名。元のnameが必ず残る。 |
| `soundSlotIds`<br>`#/$defs/drumKit/properties/soundSlotIds` | 必須 | `"array"`; uniqueItems=`true`; items: [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | ID順を維持する。Global Slotの実体は複製しない。 |

<a id="def-phrasesourcenote"></a>

## phraseSourceNote

旧1.0.0-draft.1の原型フレーズ・ノート型。Velocityを含まない（profile版を勝手に変更しない）。

Schema: `#/$defs/phraseSourceNote`

`"object"`; 追加キー禁止; oneOf（下記構造規則）.

使用箇所（構造上のパス）:

- `$.extensions["org.ostf.phrase-library.v1"].data.templates[*].notes[*]`

| パラメーター / Schema Pointer | 必須性 | 型・構造制約 | 意味 |
| --- | --- | --- | --- |
| `id`<br>`#/$defs/phraseSourceNote/properties/id` | 必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | このレコードのID。適用される一意性の範囲は型の説明を参照。 |
| `start`<br>`#/$defs/phraseSourceNote/properties/start` | 必須 | [signed](#def-signed); `"integer"`; minimum=`-9007199254740991`; maximum=`9007199254740991` | 開始tick。座標系はこの型の説明を参照。 |
| `duration`<br>`#/$defs/phraseSourceNote/properties/duration` | 必須 | [positive](#def-positive); `"integer"`; minimum=`1`; maximum=`9007199254740991` | 正の長さtick。終了位置の加算にも意味上の上限がある。 |
| `pitch`<br>`#/$defs/phraseSourceNote/properties/pitch` | pitch/soundSlotIdの一方だけ必須 | [pitch](#def-pitch); `"integer"`; minimum=`0`; maximum=`127` | 0〜127の半音番号。60=C4。soundSlotIdとの二者択一。 |
| `soundSlotId`<br>`#/$defs/phraseSourceNote/properties/soundSlotId` | pitch/soundSlotIdの一方だけ必須 | [id](#def-id); `"string"`; pattern=`"^[A-Za-z0-9][A-Za-z0-9._:-]{0,127}$"`; not=`{"pattern":"[\\r\\n\\u2028\\u2029]"}` | Core soundSlotのID。pitchとの二者択一。 |

構造・分岐規則（Schema原文）:

```json
{
  "oneOf": [
    {
      "required": [
        "pitch"
      ],
      "not": {
        "required": [
          "soundSlotId"
        ]
      }
    },
    {
      "required": [
        "soundSlotId"
      ],
      "not": {
        "required": [
          "pitch"
        ]
      }
    }
  ]
}
```

## 条件付きフィールド再制約の全一覧

既に宣言されたフィールドを条件判断・条件成立後の制約として使う箇所です。新しいパラメーターとして二重計上しません。

| Schema Pointer | 制約 |
| --- | --- |
| `#/$defs/track/allOf/0/if/properties/trackType` | `{"const":"melodic"}` |
| `#/$defs/relativeAssignment/allOf/0/if/properties/basis` | `{"const":"scaleDegree"}` |
| `#/$defs/relativeAssignment/allOf/0/then/properties/index` | `{"maximum":12}` |
| `#/$defs/extensions/properties/org.ostf.relative-phrase.v1/allOf/1/if/properties/version` | `{"const":"1.0.0-draft.1"}` |
| `#/$defs/extensions/properties/org.ostf.relative-phrase.v1/allOf/1/then/properties/data` | `{"$ref":"#/$defs/relativeData"}` |
| `#/$defs/extensions/properties/org.ostf.generation-context.v1/allOf/1/if/properties/version` | `{"const":"1.0.0-draft.1"}` |
| `#/$defs/extensions/properties/org.ostf.generation-context.v1/allOf/1/then/properties/data` | `{"$ref":"#/$defs/generationData"}` |
| `#/$defs/extensions/properties/org.ostf.appearance.v1/allOf/1/if/properties/version` | `{"const":"1.0.0-draft.1"}` |
| `#/$defs/extensions/properties/org.ostf.appearance.v1/allOf/1/then/properties/data` | `{"$ref":"#/$defs/appearanceData"}` |
| `#/$defs/extensions/properties/org.ostf.legacy-import.v1/allOf/1/if/properties/version` | `{"const":"1.0.0-draft.1"}` |
| `#/$defs/extensions/properties/org.ostf.legacy-import.v1/allOf/1/then/properties/data` | `{"$ref":"#/$defs/legacyData"}` |
| `#/$defs/extensions/properties/org.ostf.phrase-library.v1/allOf/1/if/properties/version` | `{"const":"1.0.0-draft.1"}` |
| `#/$defs/extensions/properties/org.ostf.phrase-library.v1/allOf/1/then/properties/data` | `{"$ref":"#/$defs/phraseLibraryData"}` |
| `#/$defs/extensions/properties/org.ostf.clip-choices.v1/allOf/1/if/properties/version` | `{"const":"1.0.0-draft.1"}` |
| `#/$defs/extensions/properties/org.ostf.clip-choices.v1/allOf/1/then/properties/data` | `{"$ref":"#/$defs/clipChoicesData"}` |
| `#/$defs/midiMapping/allOf/0/if/properties/standard` | `{"const":"gm1"}` |
| `#/$defs/midiMapping/allOf/0/then/properties/note` | `{"type":"integer","minimum":35,"maximum":81}` |
| `#/$defs/soundSource/allOf/0/if/properties/kind` | `{"enum":["gm1","unassigned"]}` |

## 全enum・定数索引

| Schema Pointer | 値 |
| --- | --- |
| `#/$defs/ref/properties/type/enum` | `["section","track","clip","note","chord","scale","soundSlot","drumKit","lyricDocument","lyricPhrase","lyricUnit","lyricAlignment","resource"]` |
| `#/$defs/spelledPitchClass/properties/step/enum` | `["A","B","C","D","E","F","G"]` |
| `#/$defs/meter/properties/denominator/enum` | `[1,2,4,8,16,32,64]` |
| `#/$defs/track/properties/trackType/enum` | `["melodic","drum","mixed"]` |
| `#/$defs/track/properties/preferredView/enum` | `["auto","pianoRoll","drumGrid"]` |
| `#/$defs/resource/properties/kind/enum` | `["audio","midi","text","other"]` |
| `#/$defs/dependencies/oneOf/0/properties/scope/enum` | `["document","none"]` |
| `#/$defs/extension/properties/status/enum` | `["current","stale","unverified"]` |
| `#/$defs/relativeAssignment/properties/basis/enum` | `["chordTone","scaleDegree"]` |
| `#/$defs/midiMapping/properties/standard/enum` | `["gm1","custom"]` |
| `#/$defs/soundSource/properties/kind/enum` | `["unassigned","gm1","externalMidi","plugin","hostManaged"]` |
| `#/$defs/soundSource/allOf/0/if/properties/kind/enum` | `["gm1","unassigned"]` |
| `#/$defs/chord/properties/intervals/contains/const` | `[0]` |
| `#/$defs/scale/properties/intervals/contains/const` | `[0]` |
| `#/$defs/track/allOf/0/if/properties/trackType/const` | `["melodic"]` |
| `#/$defs/dependencies/oneOf/1/properties/scope/const` | `["objects"]` |
| `#/$defs/relativeAssignment/allOf/0/if/properties/basis/const` | `["scaleDegree"]` |
| `#/$defs/legacyData/properties/sourceVersion/const` | `["2.3.0"]` |
| `#/$defs/extensions/properties/org.ostf.relative-phrase.v1/allOf/1/if/properties/version/const` | `["1.0.0-draft.1"]` |
| `#/$defs/extensions/properties/org.ostf.generation-context.v1/allOf/1/if/properties/version/const` | `["1.0.0-draft.1"]` |
| `#/$defs/extensions/properties/org.ostf.appearance.v1/allOf/1/if/properties/version/const` | `["1.0.0-draft.1"]` |
| `#/$defs/extensions/properties/org.ostf.legacy-import.v1/allOf/1/if/properties/version/const` | `["1.0.0-draft.1"]` |
| `#/$defs/extensions/properties/org.ostf.phrase-library.v1/allOf/1/if/properties/version/const` | `["1.0.0-draft.1"]` |
| `#/$defs/extensions/properties/org.ostf.clip-choices.v1/allOf/1/if/properties/version/const` | `["1.0.0-draft.1"]` |
| `#/$defs/midiMapping/allOf/0/if/properties/standard/const` | `["gm1"]` |
| `#/properties/format/const` | `["OSTF"]` |
| `#/properties/version/const` | `["3.1.0"]` |

## Schemaだけでは完結しない意味規則

下表は規範仕様への索引です。配列順、参照、計算結果、操作の正しさをSchemaの構造一致だけで証明したとは扱いません。

| 仕様節 | 追加で必要な意味規則 |
| --- | --- |
| [2](FORMAT_SPECIFICATION.ja.md) | UTF-8、BOM禁止、重複キー・非有限値・孤立surrogate禁止。整数は整数tokenで保存。 |
| [2.3 / 9.3](FORMAT_SPECIFICATION.ja.md) | 未知dataの数値精度とinteger/real token区別を保持。未知のprofile版は既知payload schemaで検査しない。 |
| [3.1 / 3.4 / 6.3](FORMAT_SPECIFICATION.ja.md) | 開始・長さだけでなく加算・乗算したendpointもMAX以内。絶対開始は非負。 |
| [3.2 / 3.3](FORMAT_SPECIFICATION.ja.md) | Core ID全体の一意性、参照先の種別、一意性が局所のprofile IDとの区別。 |
| [4.2](FORMAT_SPECIFICATION.ja.md) | sectionsは開始順・非重複。テンポと拍子は0開始・厳密昇順。 |
| [5](FORMAT_SPECIFICATION.ja.md) | harmonyは開始順。intervalsは厳密昇順。label、bass、scaleからノートを生成しない。 |
| [6](FORMAT_SPECIFICATION.ja.md) | clipとnoteの開始順、同時刻での配列順、pickup・tail・重複音の保持。clip長は切断マスクではない。 |
| [6.4](FORMAT_SPECIFICATION.ja.md) | 実効enabledはtrack AND clip。同tickでoffがonより前、同種はnote ID辞書順。 |
| [7](FORMAT_SPECIFICATION.ja.md) | soundSlotの同一性をMIDI番号で置き換えない。resourceを読込時に取得・実行しない。 |
| [8](FORMAT_SPECIFICATION.ja.md) | 歌詞の文書・フレーズ・ノート参照、グローバル時刻、順序付き多対多の対応。 |
| [9](FORMAT_SPECIFICATION.ja.md) | currentの参照は解決が必要。stale/unverifiedでも既知payloadの構造不正はエラー。 |
| [9.2](FORMAT_SPECIFICATION.ja.md) | 既知current profileの全Core直接参照を依存に含める。親から継承する影響も考慮。 |
| [10.1](FORMAT_SPECIFICATION.ja.md) | 相対式、anchorの音名一致、実配列内のindex、重複noteId禁止を確認。 |
| [10.2](FORMAT_SPECIFICATION.ja.md) | 生成工程IDは局所一意。vendorExtensionは自身以外の実在拡張を指し、current時はdocument依存。 |
| [10.3](FORMAT_SPECIFICATION.ja.md) | appearanceのrole割当と色参照を解決し、競合する割当を意味規則に従って扱う。 |
| [10.4](FORMAT_SPECIFICATION.ja.md) | phraseの完全対応、clip所有、source IDs・noteMapの一意性、反復式・移調・範囲。 |
| [10.5](FORMAT_SPECIFICATION.ja.md) | candidateの局所ID、group間の管理clip非重複、選択IDとCore enabledの一致。 |
| [10.6 / 10.7](FORMAT_SPECIFICATION.ja.md) | 生成・選択・template置換・detachは明示的操作。読込時に実行しない。保護対象はbeforeから固定。 |
| [11](FORMAT_SPECIFICATION.ja.md) | 2.3移行は版文字列置換ではない。sourceText、hash、移行記録を保持する。 |
| [17.1](FORMAT_SPECIFICATION.ja.md) | trackTypeは全保存ノートを対象に検査する。欠落時はpitch/soundSlotIdから判定、空ならunknown。 |
| [17.2](FORMAT_SPECIFICATION.ja.md) | preferredViewは非強制のUI表示ヒント。非ドラムノートを隠すUI指定を安全に代替する。 |
| [17.3](FORMAT_SPECIFICATION.ja.md) | GM1は35–81の明示的mappingのみ。legacy midiNoteはGM保証なし、両者指定時は一致必須。 |
| [17.4](FORMAT_SPECIFICATION.ja.md) | instrumentは楽器の意味、soundSourceは音源選択ヒント。プラグイン状態やCCはCoreに含まれない。 |
| [17.5](FORMAT_SPECIFICATION.ja.md) | MIDI変換では明示Velocityを優先し、省略時だけ宣言済み既定値を補完。PPQ,ゲート,無効状態,損失報告はDAW非依存。 |

## 関連資料と再生成

- [Complete manual](COMPLETE_MANUAL.ja.md)
- [Normative specification](FORMAT_SPECIFICATION.ja.md)
- [Explicit operations and CLI/API parameters](COMPLETE_MANUAL.ja.md)
- [2.3 migration](https://github.com/yoh-nak/Open-Song-Timeline-Format-3.0)
- [この全パラメーターリファレンス](PARAMETER_REFERENCE.ja.md)
- [Sample coverage](COVERAGE.md)

この資料は100ファイル以内の正式版に固定して収録したリファレンスです。旧生成スクリプトは同梱していません。
