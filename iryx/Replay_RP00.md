# vMixコントローラー Iryx Replay RP-00 取扱説明書

## 目次

- [1. はじめに](#section-1)
- [2. 安全上のご注意](#section-2)
- [3. 動作環境](#section-3)
  - [3.1 製品の種類（LAN搭載とUSB専用）](#section-3-1)
- [4. 使用方法](#section-4)
  - [4.1 接続方法](#section-4-1)
  - [4.2 メイン画面の表示内容](#section-4-2)
  - [4.3 操作の全体像](#section-4-3)
  - [4.4 メニュー内のボタン対応](#section-4-4)
  - [4.5 メニュー階層](#section-4-5)
  - [4.6 キーマトリクスとショートカット（メイン画面）](#section-4-6)
    - [4.6.1 UserScript の取り扱い](#section-4-6-1)
  - [4.7 回転エンコーダ（ジョグ）](#section-4-7)
  - [4.8 Tバー（スライド）](#section-4-8)
  - [4.9 LEDの意味（目安）](#section-4-9)
- [5. 免責事項](#section-5)
- [6. ライセンス表示について](#section-6)
- [7. よくある質問](#section-7)
- [8. お問い合わせ・フィードバック](#section-8)

<a id="section-1"></a>

## 1. はじめに

本製品は、vMixのリプレイ操作に特化したコントローラーです。  
vMixの状態取得および操作をTCP API経由で行うための評価用試作機です。  
本製品は現在開発中です。完成次第Boothでの頒布を予定しています。  
**本製品の転売・譲渡を固く禁止します。**

---

<a id="section-2"></a>

## 2. 安全上のご注意

本製品は開発中の試作品であり、一般的な市販製品と同等の保護機能を備えていない場合があります。

* 電源: USB-Cから直接給電が可能です。PCのUSBポートに接続してください。
* 環境: ライブ配信現場などの機材密集地で使用する場合、排熱を妨げないように設置してください。
* 異常時: 本体が異常に熱くなる、焦げた臭いがする等の場合は直ちにUSBケーブルを抜いてください。

---

<a id="section-3"></a>

## 3. 動作環境

- vMix 29 Pro Edition
  - 4K以下のEditionや古いバージョンでは、Angleの変更やChannel切り替えに対応していない可能性があります
- (USBモード) USB CDC-NCMに対応したWindows（Windows 10 Version 1903以降、Windows 11）
- (USBモード) データ転送可能なUSB-Cケーブル(USB 1.1 Full-speed)
- (LANモード) 100BASE-TX規格に対応したネットワーク

## 4. 使用方法

<a id="section-4-1"></a>

### 4.1 接続方法

<a id="section-4-1-1"></a>

#### 4.1.1 接続方法(USBモード)

PCと本機を、データ転送対応のUSBケーブルで接続してください。  
イーサネットアダプターとして認識され、本機のIPに `172.31.x.1` が割り当てられます（サブネットの第3オクテット `x` は保存領域の値が使われます）。  
複数台を同一PCに接続する場合はIPの重複を避けるため、別途設定手段で第3オクテットを変えた値を保存してください。

<a id="section-4-1-2"></a>

#### 4.1.2 接続方法(LANモード)

LAN搭載モデルで、接続方法がLANに設定されている場合に限ります。  
本機にUSBで給電し、LANケーブルを接続してください。DHCP対応環境の場合、自動的にIPが設定されます。  
接続先のvMixのIPは保存領域に記録された値が使われます。  
DHCP サーバが無い環境では、約 30 秒待ったあと自動的に `192.168.1.100/24`（ゲートウェイ `192.168.1.1`）にフォールバックします。起動自体は待たされません。vMix 用 PC と同じサブネットで使う場合は、Settings から LAN を Static に切り替え、Static IP を編集してください（ゲートウェイは `.1` 固定）。

<a id="section-4-2"></a>

### 4.2 メイン画面の表示内容

電源投入後、通常は Status 画面が表示されます。

| 表示行 | 内容 | 補足 |
| :--- | :--- | :--- |
| （見出し） | `Iryx Replay` | 製品名 |
| Status | `connected` / `disconnected` | vMixとの接続状態 |
| Target | `vMixのIP` | 接続先vMixのIP |
| Iryx IP | 本機のIPv4 | 未取得時は `0.0.0.0` など |
| Link | `LAN` または `USB` | 現在の接続方法 |
| Version | vMixから取得した文字列 | 未取得時は `Version: —` |
| Menu | `Menu: open menu` | メニュー操作の案内 |

<a id="section-4-3"></a>

### 4.3 操作の全体像

- 各種操作キー、ジョグ、スライダーがあります。
- Shiftキーを他のキーと組み合わせると、別のショートカットになります。

<a id="section-4-4"></a>

### 4.4 メニュー内のボタン対応

メニュー表示中は、次のように割り当てられます。

| 物理ボタン | 意味 |
| :--- | :--- |
| Up/Down | カーソル上／下 |
| Menu | メニューを開く |
| Back | 戻る |
| Enter | 決定 |

<a id="section-4-5"></a>

### 4.5 メニュー階層

<a id="section-4-5-1"></a>

#### 4.5.1 メインメニュー

| 行 | 選択 | 遷移先 |
| :--- | :--- | :--- |
| [1] | Settings | システム設定へ |
| [2] | Reset replay defaults | [初期値に戻す確認画面へ](#section-4-5-2) |
| [3] | Help (URL) | ヘルプ（表示内容は書き込み済みの機種により異なります） |
| [4] | License | ライセンス抜粋の案内 |
| [5] | Reboot | 本体の再起動 |

<a id="section-4-5-2"></a>

#### 4.5.2 Reset replay defaults（確認画面）

「Reset replay tuning to firmware defaults?」と表示されます。  
Enter で確定すると、リプレイ関連の内部パラメータ（ジョグの刻み幅、クイッククリップの秒数、複合シーケンスの待ち時間など）が初期値に戻り、保存領域へ書き込まれます。Back でキャンセルします。

Settings では、Link Mode（LAN/USB）、USB DHCP 第3オクテット、LAN の DHCP/Static 切替と Static IP 編集（ゲートウェイは `.1` 固定）、vMix IP 編集（LAN時のみ編集可）、および再起動ができます。

※ USB 専用（LAN非搭載）の場合、Link Mode は選択できません（`Link: USB fixed` 表示）。このとき Settings→System の入口では、再起動は `[3]` に表示されます。

<a id="section-4-5-3"></a>

#### 4.5.3 Settings（システム設定）

Settings は、本体内の保存領域（ネットワーク設定・接続先など）を変更する画面です。  
メニュー表示中は [4.4](#section-4-4) の通り、Up/Down/Back/Enter を使って操作します。

**LAN搭載モデル（LAN/USB 切替可能）**

- System（入口）
  - `[1] LAN`: LAN 側の設定（vMix IP / LAN DHCP-Static / Static IP）
  - `[2] USB`: USB 側の設定（USB DHCP 第3オクテット / vMix IP 表示）
  - `[3] Link Mode`: 接続方法（LAN/USB）の切替（保存で再起動）
  - `[4] Restart`: 再起動
- LAN
  - `1: vMix IP`: LAN 時のみ編集可（オクテットを変更して確定すると保存・再接続）
  - `2: IP: DHCP/Static`: 切替と適用
  - `3: Static IP`: 固定IPの編集と適用（ゲートウェイは `.1` 固定）
- USB
  - `1: vMix IP`: USB テザー時の PC 側アドレス表示（読み取り専用）
  - `2: USB DHCP`: `172.31.x.0/30` の `x`（第3オクテット）を変更して保存

**USB専用モデル（LAN非搭載）**

- System（入口）
  - `[1] USB`
  - `LAN: disabled`（表示のみ）
  - `Link: USB fixed`（表示のみ）
  - `[3] Restart`

<a id="section-4-6"></a>

### 4.6 キー動作

| ボタン名 | 機能説明 | 対応Function | Shift押下時Function |
| :--- | :--- | :--- | :--- |
| **Shift**（修飾キー） | 修飾キー | — | — |
| **Clip 前** | 前のイベントへ／Shift で先頭へ | `ReplaySelectPreviousEvent` | `ReplaySelectFirstEvent` |
| **Clip 後** | 次のイベントへ／Shift で末尾へ | `ReplaySelectNextEvent` | `ReplaySelectLastEvent` |
| **UserScript1～3**（[4.6.1](#section-4-6-1)） | ユーザー定義スクリプト | `ScriptStart`（`Value=Iryx_RP00_UserScript1`～`3`） | `ScriptStart`（`Value=Iryx_RP00_UserScript5`～`7`） |
| **Channel A～D** | チャンネル選択 | `ReplaySelectChannelA`～`ReplaySelectChannelD` | 同左 |
| **UserScript4**（[4.6.1](#section-4-6-1)） | ユーザー定義スクリプト | `ScriptStart`（`Value=Iryx_RP00_UserScript4`） | `ScriptStart`（`Value=Iryx_RP00_UserScript8`） |
| **Jump In** | 選択中のクリップの In 点へ | `ReplayJumpToSelectedInPoint` | 同左 |
| **Jump Out** | 選択中クリップの Out 点へ | `ReplayJumpToSelectedOutPoint` | 同左 |
| **Play** | 再生 | `ReplayPlay` | 送信なし（Playのみ有効） |
| **Pause** | 一時停止 | `ReplayPause` | 同左 |
| **Play Out**（[詳細](#section-4-6-play-out)） | リプレイの起動・再生準備 | `ReplayPlayAllEvents`→`ReplayPause` | `ReplayPlayAllEvents` のみ |
| **Rec** | 録画開始／停止 | `ReplayStartRecording` | `ReplayStopRecording` |
| **Angle 1～6** | カメラアングル | `ReplayCamera1`～`ReplayCamera6` | `ReplaySelectedEventSingleCameraOn`（値1～6） |
| **Angle 7～8** | カメラアングル | `ReplayCamera7`～`ReplayCamera8` | `ReplaySelectedEventSingleCameraOn`（値7～8） |
| **Mark In** | In 点の設定／更新 | `ReplayMarkIn` | `ReplayUpdateSelectedInPoint` |
| **Mark Out** | Out 点の設定／更新 | `ReplayMarkOut` | `ReplayUpdateSelectedOutPoint` |
| **Jump To Now**（[詳細](#section-4-6-jump-to-now)） | 現在時間へジャンプ | `ReplayJumpToNow`→`ReplayJumpFrames`→`ReplayPlay` | `ReplayJumpToNow` のみ |
| **Quick Clip**（[詳細](#section-4-6-quick-clip)） | ワンボタンクリップ | `ReplayMarkInOut` | 押下で `ReplayMarkIn`、離しで `ReplayMarkOut` |
| **Copy** | コピー／複製 | `ReplayCopySelectedEvent` | `ReplayDuplicateSelectedEvent` |
| **Delete** | 削除 | 送信なし | `ReplayDeleteSelectedEvent` |
| **Menu** | メニュー表示 | — | — |
| **Back** | メニュー操作（戻る） | — | — |
| **Enter** | メニュー操作（決定） | — | — |

各Functionの詳細は、vMix公式の[Shortcut Function Reference](https://www.vmix.com/help29/ShortcutFunctionReference.html)を参照してください。

<a id="section-4-6-1"></a>

#### 4.6.1 UserScript の取り扱い

本機は vMix の `ScriptStart` 関数を、クエリ `Value=Iryx_RP00_UserScriptN`（N は 1～8）で呼び出します。

物理キーの UserScript は 1～4 のみです。Shift 押下時は 1～4 が 5～8 に読み替えられます。

**vMix 側の設定**

- vMixのSettings→Scriptingから、名前を `Iryx_RP00_UserScript1` ～ `Iryx_RP00_UserScript8` としたScriptを作成し、実行したい処理を登録してください。  
Mixによる制約や各Functionの詳細は、vMix公式の[Scripting and Automation](https://www.vmix.com/help29/WebScripting.html)、[Shortcut Function Reference](https://www.vmix.com/help29/ShortcutFunctionReference.html)を参照してください。  
また、本デバイスの接続時にUSBストレージデバイスとして認識されます。`Scripts`フォルダにリプレイ・ハイライトオペレーションで使用可能なスクリプト集を纏めています。合わせてご活用ください。  

<a id="section-4-6-play-out"></a>

#### Play Out

リプレイの起動・再生準備に使用するボタンです。  
`ReplayPlayAllEvents`, `ReplayPause` を実行します。  
Shift押下時は`ReplayPlayAllEvents`のみ送信します。  
各種Functionごとに数ミリ秒の待機処理を挟んでいます(設定で変更が可能です)。

<a id="section-4-6-jump-to-now"></a>

#### Jump To Now

リプレイを現在時間にジャンプさせるボタンです、  
`ReplayJumpToNow`, `ReplayJumpFrames`, `ReplayPlay` を実行します。  
Shift押下時は `ReplayJumpToNow` のみです。  
各種Functionごとに数ミリ秒の待機処理を挟んでいます(設定で変更が可能です)。

<a id="section-4-6-quick-clip"></a>

#### Quick Clip

ワンボタンクリップを行うボタンです。  
`ReplayMarkInOut` を実行します。  
Shift押下時は、ボタン押下時に`ReplayMarkIn`が、離したときに `ReplayMarkOut` が送られます。  
`ReplayMarkInOut` でクリップする秒数は設定で変更が可能です。  

<a id="section-4-7"></a>

### 4.7 ジョグ

フレーム送りに使用します。  
回転した分だけ `ReplayJumpFrames` が送られます。  
Shiftを押しながら回すと、1ステップあたりのフレーム数が大きくなります。  
ステップごとに移動するフレーム数は設定で変更が可能です。  

<a id="section-4-8"></a>

### 4.8 スライド

再生速度の制御に使用します。  
`ReplaySetSpeed` を送ります。値は0.0から1.0の範囲です。

<a id="section-4-9"></a>

---

<a id="section-5"></a>

## 5. 免責事項

本機は将来的な製品化に向けたデータ収集を目的とした評価試験機です。  
本機を使用したことによる本番配信の停止、vMixのフリーズ、接続PCの故障、その他一切の二次的損害について、開発者は責任を負いかねます。  
重要な現場で使用される際は、必ず事前の検証とバックアップ体制の確保をお願いいたします。

**本機の分解、解析、および内蔵ソフトウェアの抽出・転用、転売・譲渡を固く禁止します。**

---

<a id="section-6"></a>

## 6. ライセンス表示について

本機のソフトウェアは、多数のオープンソースソフトウェアを利用して構築されています。MITまたはApache 2.0等のライセンスに基づき、著作権表示を条件に利用を許可されています。  
画面上の License に主要名の抜粋が表示されます。詳細な一覧やライセンス全文が必要な場合は、下記の連絡先までご請求ください。

---

<a id="section-7"></a>

## 7. よくある質問

- Q1. vMix以外のソフトウェアには対応していますか？  
  A1. 対応していません。

- Q2. vMixに接続ができません。  
  A2. USBモードの場合、ネットワークアダプタとして認識されているかご確認ください。LANモードの場合は、保存された接続先が正しいか、ケーブルやルータ側の設定を確認してください。

- Q3. ボタン操作が効かない  
  A3. シャットダウン後もUSBの電源を供給するPCの場合に、稀に応答が不安定になることがあります。電源を抜き差しし、再起動してください。

---

<a id="section-8"></a>

## 8. お問い合わせ・フィードバック

不具合報告、機能要望、または現場での使用感などのフィードバックを心よりお待ちしております。  
SNSでの投稿は #Iryx をご利用ください。

* 開発元: [未完成成果物研究所](https://incomplete-outputs-lab.github.io)
* ファームウェア開発: [Flowing](https://github.com/FlowingSPDG)
* 回路設計・基板筐体制作: [mizuyoukan](https://github.com/mizuyoukanao)
* Contact: [ruk1ium@gmail.com](mailto:ruk1ium@gmail.com)

---
