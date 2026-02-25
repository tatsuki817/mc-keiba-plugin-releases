Japanese / English


# HorseRacingPlugin (Alpha)

A **horse racing mini-game plugin** for Minecraft (Paper 1.21).  
It provides a full gameplay loop: course building, race running, betting, payouts, and scheduled races.

> ⚠️ This is an **alpha release**. Specifications, data compatibility, and balance may change frequently. Testing on a staging server is strongly recommended.

---

## Features

- In-game course creation (checkpoint-based)
- Gate / goal line / spawn point setup
- Race operation (manual start and forced next-race start)
- Betting GUI (Win, Place, Quinella, Exacta, Trio, Trifecta)
- Vault economy integration for bet purchases and payouts
- AI profile switching and AI debug display
- Horse data management (acquire, rename, retire, records)
- Automatic race schedule generation and operation

---

## Requirements

- **Minecraft / Paper**: `1.21.x` (`paper-api 1.21-R0.1-SNAPSHOT`)
- **Java**: `21`
- **Recommended dependencies**:
  - Vault
  - An economy plugin (e.g. EssentialsX Economy)

> If Vault integration is unavailable, betting features are effectively disabled (no purchases).

---

## Installation

1. Download `horseracing-0.2-SNAPSHOT.jar`
2. Put it into your server `plugins` folder
3. Start the server
4. Edit `plugins/HorseRacingPlugin/config.yml` if needed
5. Prefer a full **server restart** rather than `/reload`

---

## Commands

### For players

- `/racebet` : Open the betting GUI

### For admins (mainly `/race`)

- `/race create <course_name>` : Enter course creation mode
- `/race save` : Save current editing data
- `/race cancel` : Cancel current setup/edit mode
- `/race undo` : Undo recent operation (course/spawn/etc.)
- `/race list` : List available courses
- `/race setgoal <course_name>` : Set goal line
- `/race setgate <course_name>` : Set gate area
- `/race setspawn <course_name>` : Set spawn points
- `/race setwidth <course_name> <width>` : Set course width
- `/race setdirection <course_name> <clockwise|counterclockwise>` : Set lap direction
- `/race tpgate <course_name>` : Teleport to gate
- `/race cleargrass <course_name> [height_offset]` : Clear grass
- `/race clearglass <edit|apply|undo|cancel>` : Edit grass-clear region
- `/race standby <course_name> <horse_count> [track]` : Prepare a race
- `/race start <course_name>` : Start race
- `/race end <course_name>` : End race
- `/race next [start]` : Show next race / force-start next race
- `/race schedule <start|end|status>` : Control schedule operation
- `/race debug <gate|spawns|ai|off> ...` : Debug display tools
- `/race reloadai` : Reload AI settings
- `/race horse <list|info|name|retire|get>` : Manage owned horses

---

## Permissions

- `horseracing.race` : Access to `/race` (default: OP)
- `horseracing.race.admin` : Administrative `/race` operations (default: OP)
- `horseracing.bet` : Access to `/racebet` (default: true)

---

## About Horse AI

CPU horses in races are controlled by the plugin's AI system.  
You can tune behavior in `config.yml` based on your server style.

- `race-mode`: AI mode (`physics` / `style` / `simple`)
  - `physics`: richer movement with pathing, cornering, and slope influence
  - `style`: easier-to-read behavior based on running styles
  - `simple`: lightweight baseline behavior
- `ai-profile`: loads AI parameter sets from `ai-profiles/<name>.yml`
- `strategy-common`: shared coefficients (pace, positioning, final spurt, stamina drain)
- `physics-strategy`: physics-only coefficients (inner-lane preference, overtaking, slope/corner effects)

### AI operation tips

- Run `/race reloadai` after tuning values
- Use `/race debug ai <course_name> [horse_number]` to inspect behavior
- AI balance is still being tuned during alpha; adjusting values per server policy is recommended

---

## Main config keys (`config.yml`)

- `language`: display language (`ja` / `en`)
- `debug`: debug logging
- `race-mode`: AI mode (`physics` / `style` / `simple`)
- `ai-profile`: AI profile name
- `horse-data.limits.*`: horse-data limits
- `economy.enabled`: enable/disable Vault integration
- `odds-system.*`: odds and virtual bettor settings
- `race-schedule.*`: race interval and betting window

For schedule generation details, see `generator_settings.yml`.

---

## Alpha notes

- Config keys and command behavior may change
- Internal data changes may break compatibility
- Test on smaller/staging servers first
- When reporting issues, include your `config.yml` and reproduction steps

---

## Known assumptions

- Betting requires Vault + an economy plugin
- Races may fail if course setup (gate/goal/spawns) is incomplete

---

## Planned improvements (examples)

- Better GUI and race presentation effects
- AI and odds balance tuning
- Expanded operator/admin tooling

Feedback is welcome. Since this is an alpha release, your reports and balancing notes are highly appreciated!




# HorseRacingPlugin（アルファ版）

Minecraft（Paper 1.21系）向けの**競馬ミニゲームプラグイン**です。  
コース作成、出走、ベット、払戻し、スケジュール開催まで一通り遊べます。

> ⚠️ 本バージョンは**アルファ版**です。仕様変更・データ互換性の変更・不具合修正が頻繁に入る可能性があります。検証サーバーでの利用を推奨します。

---

## できること

- コースをゲーム内で作成（チェックポイント方式）
- ゲート／ゴール／スポーン地点の設定
- レース開催（手動開始・次レース強制開始）
- ベットGUI（単勝・複勝・馬連・馬単・3連複・3連単）
- Vault経済連携による購入＆払戻し
- AIプロファイル切替・AIデバッグ表示
- 馬データの管理（獲得・命名・引退・戦績表示）
- レース番組の自動生成・スケジュール運用

---

## 対応環境

- **Minecraft / Paper**: `1.21.x`（`paper-api 1.21-R0.1-SNAPSHOT`）
- **Java**: `21`
- **依存プラグイン（推奨）**:
  - Vault
  - 経済プラグイン（EssentialsX Economy など）

> Vault連携が使えない場合、ベット関連機能は実質無効になります（購入不可）。

---

## 導入方法

1. `horseracing-0.2-SNAPSHOT.jar` をダウンロード
2. サーバーの `plugins` フォルダへ配置
3. サーバー起動
4. 必要に応じて `plugins/HorseRacingPlugin/config.yml` を編集
5. `/reload` ではなく**サーバー再起動**を推奨

---

## コマンド

### プレイヤー向け

- `/racebet` : ベットGUIを開く

### 管理者向け（主に `/race`）

- `/race create <コース名>` : コース作成モード開始
- `/race save` : 作成中データを保存
- `/race cancel` : 各種設定モードをキャンセル
- `/race undo` : 直前操作の取り消し（コース・スポーン等）
- `/race list` : コース一覧
- `/race setgoal <コース名>` : ゴール設定
- `/race setgate <コース名>` : ゲート設定
- `/race setspawn <コース名>` : スポーン地点設定
- `/race setwidth <コース名> <幅>` : コース幅設定
- `/race setdirection <コース名> <clockwise|counterclockwise>` : 周回方向設定
- `/race tpgate <コース名>` : ゲートへテレポート
- `/race cleargrass <コース名> [高さオフセット]` : 草除去
- `/race clearglass <edit|apply|undo|cancel>` : 草除去範囲編集
- `/race standby <コース名> <頭数> [馬場]` : レース待機作成
- `/race start <コース名>` : レース開始
- `/race end <コース名>` : レース終了
- `/race next [start]` : 次レース情報表示 / 強制開始
- `/race schedule <start|end|status>` : スケジュール運用
- `/race debug <gate|spawns|ai|off> ...` : デバッグ表示
- `/race reloadai` : AI設定再読み込み
- `/race horse <list|info|name|retire|get>` : 所有馬管理

---

## 権限

- `horseracing.race` : `/race` 利用権限（デフォルト: OP）
- `horseracing.race.admin` : 管理系 `/race` 操作（デフォルト: OP）
- `horseracing.bet` : `/racebet` 利用権限（デフォルト: true）

---

## 馬AIについて

本プラグインでは、レース中のCPU馬の挙動をAIで制御しています。  
運営スタイルに合わせて、`config.yml` でモードやチューニングを変更できます。

- `race-mode`: AIモード切替（`physics` / `style` / `simple`）
  - `physics`: 進路取り・コーナー・坂などを考慮する、よりリッチな挙動
  - `style`: 脚質ベースで分かりやすい挙動
  - `simple`: 軽量で扱いやすい基本挙動
- `ai-profile`: AIパラメータセットを読み込み（`ai-profiles/<name>.yml`）
- `strategy-common`: 全モード共通の係数（巡航・位置取り・終盤スパート・スタミナ消費など）
- `physics-strategy`: physicsモード専用係数（内ラチ志向、追い抜き、坂/コーナー補正など）

### AI運用のヒント

- 調整を反映したいときは `/race reloadai` を実行
- 走り方の確認には `/race debug ai <course_name> [horse_number]` を利用
- アルファ版ではAIバランスを継続調整中のため、サーバー方針に合わせて数値調整を推奨

---

## 主要設定（`config.yml`）

- `language`: 表示言語（`ja` / `en`）
- `debug`: デバッグログ
- `race-mode`: AIモード（`physics` / `style` / `simple`）
- `ai-profile`: AIプロファイル名
- `horse-data.limits.*`: 馬データ上限
- `economy.enabled`: Vault連携有効/無効
- `odds-system.*`: オッズ計算・仮想ベッター設定
- `race-schedule.*`: 開催間隔・受付秒数

自動番組生成の詳細は `generator_settings.yml` で調整できます。

---

## アルファ版としての注意事項

- 設定キーやコマンド仕様が更新で変わる可能性があります
- 内部データ構造の変更により、既存データ互換が崩れる可能性があります
- まずは小規模サーバーやテスト環境での運用を推奨します
- 不具合報告時は、`config.yml` と発生手順を添えてください

---

## 既知の前提

- ベット機能を使う場合は Vault + 経済プラグインが必要です
- コース設定（ゲート・ゴール・スポーン）が未完了のままでは正常に開催できません

---

## 更新予定（例）

- GUI/演出の強化
- バランス調整（AI・オッズ）
- 運営向け管理コマンドの拡張

フィードバック歓迎です。アルファ版のため、ぜひ使用感を教えてください！
