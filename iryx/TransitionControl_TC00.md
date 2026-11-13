# vMix / ATEMコントローラー Iryx Transition Control TC-00 取扱説明書

## 目次

- [1. はじめに](#section-1)
- [2. 安全上のご注意](#section-2)
- [3. 動作環境](#section-3)
  - [3.1 製品の種類（LAN搭載とUSB専用）](#section-3-1)
  - [3.2 動作モード（vMix / ATEM）](#section-3-2)
- [4. 使用方法](#section-4)
  - [4.1 接続方法](#section-4-1)
  - [4.2 メイン画面の表示内容](#section-4-2)
  - [4.3 メニュー内のボタン対応（共通）](#section-4-3)
  - [4.4 メニュー階層](#section-4-4)
    - [4.4.1 メインメニュー](#section-4-4-1)
    - [4.4.2 LAN 配下（LAN搭載モデル）](#section-4-4-2)
    - [4.4.3 USB 配下](#section-4-4-3)
    - [4.4.4 Link Mode（LAN搭載モデル）](#section-4-4-4)
    - [4.4.5 Transition Settings](#section-4-4-5)
    - [4.4.6 Help / License](#section-4-4-6)
    - [4.4.7 ATEM モードのメニュー](#section-4-4-7)
  - [4.5 設定項目と vMix 側の対応](#section-4-5)
  - [4.6 ATEM モードの操作対応](#section-4-6)
  - [4.7 モードの切り替え（vMix / ATEM）](#section-4-7)
- [5. 免責事項](#section-5)
- [6. ライセンス表示について](#section-6)
- [7. よくある質問](#section-7)
- [8. お問い合わせ・フィードバック](#section-8)

<a id="section-1"></a>

## 1. はじめに

本製品は、vMix または Blackmagic ATEM のトランジション制御に特化したコントローラーです。  
vMix と ATEM の制御を検証するための評価用試作機です。  
1 台で **vMix モード**と **ATEM モード**のどちらか一方として動作し、起動時に保存されたモードが使われます。

- **vMix モード**: vMix の状態取得および操作を TCP API 経由で行います。
- **ATEM モード**: Blackmagic ATEM を UDP（ポート 9910）経由で操作します。ATEM 本体の操作パネルや Software Control を使わずに、Cut / Auto / Preview を操作できます。

本製品は、開発者と合意があった企業・個人にのみ限定し頒布しています。  
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

- **vMix モード**
  - vMix 29以降  
    - v28以前のvMixでは、`Stinger5～8`、`OverlayInput5～8`、Mixの選択や一部のTransitionに対応していない可能性があります。
  - (USB接続) USB CDC-NCMに対応したWindows（Windows 10 Version 1903以降、Windows 11）
  - (USB接続) データ転送可能なUSB-Cケーブル(USB 1.1 Full-speed)
  - (LAN接続) 100BASE-TX規格に対応したネットワーク
- **ATEM モード**
  - Blackmagic ATEM スイッチャー（Ethernet 接続、制御ポート UDP 9910 を利用できるもの）
  - 本機と ATEM を同一ネットワークに接続できること
  - 有線LAN搭載モデルであること（USB専用モデルでは ATEM モードを使用できません）

<a id="section-3-1"></a>

### 3.1 製品の種類（LAN搭載とUSB専用）

本体には、次の2種類があります。メニュー構成が一部異なるので、お手元の機種に合わせてください。

| 区分 | 特徴 | ネットワーク |
| :--- | :--- | :--- |
| LAN搭載モデル | 有線LANポート付き | 有線LANとUSB接続のどちらを使うかを選択可能（初期は有線LAN） |
| USB専用モデル | 有線LANポートなし | USB接続のみ |

<a id="section-3-1-lan"></a>

#### LAN搭載モデル

- 起動時は有線LAN側を既定とし、設定でUSB接続に切り替えられます。
- Link Mode で `LAN` と `USB` のどちらかを選び、画面の指示に従って保存すると再起動後に切り替わります。
- LAN メニューでは、有線側の vMix IP、LAN の DHCP／固定IP、固定IPアドレスの編集ができます。
- USB メニューでは、USB側のサブネット（`172.31.x.0/30` の x）の変更ができます。
- 接続方法が USB のとき、LAN 用の vMix IP 画面は保存済みの値の確認のみで、ここからは編集できません。有線LANに戻してから編集してください。
- ATEM モードも使用できます。ATEM モードでは有線LANのみを使用し、USB は給電専用になります。

<a id="section-3-1-usb"></a>

#### USB専用モデル

- 接続方法はUSBのみです。
- メニュー「Settings」の設定項目もLAN搭載モデルとは一部異なります。
- USB 専用の場合、Link Mode は選択できません（`Link` は固定表示）。このとき Settings→System 入口の再起動は `[3]` に表示されます。
- USB メニュー（vMix IP の表示、USB DHCP レンジ）は LAN搭載モデルと同様です。
- PC とはデータ転送対応のUSBケーブルで接続し、本機と vMix 用PCのIPは接続方法の節(`172.31.x.x`)に従います。
- USB 専用モデルは vMix モード専用です。ATEM モードに切り替えても、有線LANがないため ATEM には接続できません。

<a id="section-3-2"></a>

### 3.2 動作モード（vMix / ATEM）

TC-00 は 1 つのファームウェアで vMix 用と ATEM 用の両方の画面・操作を持ち、起動時に選ばれたどちらか一方だけを動かします。vMix と ATEM を同時に操作することはできません。

| モード | 制御対象 | 接続方法 | 主な用途 |
| :--- | :--- | :--- | :--- |
| vMix モード | vMix | 有線LAN または USB | vMix の Cut / Auto / Stinger / Overlay / Transition 操作 |
| ATEM モード | Blackmagic ATEM | 有線LAN のみ（USB は給電専用） | 対象 M/E の Cut / Auto、Preview 1～4 の切り替え |

- モードはメインメニューの `[Cut]` 行から切り替えます。確認画面で `Auto` を押すと保存して再起動します（[4.7](#section-4-7)）。
- 選んだモードは本体に保存され、次回起動時も同じモードで立ち上がります。
- ATEM 設定がまだ保存されていない本体（新品時など）は、ATEM モードで起動します。vMix で使用する場合は vMix モードへ切り替えてください。
- USB 専用モデルを ATEM モードで起動した場合は、メインメニューの `[Cut] Switch to vMix` で vMix モードに戻してください。
- vMix のトランジション設定と ATEM の Target ME は別々に保存されます。モードを切り替えても失われません。
- 接続先 IP は vMix / ATEM で共通の保存値です。モードを切り替えたときは、ATEM の IP を LAN メニューで確認してください（[4.4.7](#section-4-4-7)）。

---

<a id="section-4"></a>

## 4. 使用方法

<a id="section-4-1"></a>

### 4.1 接続方法

<a id="section-4-1-1"></a>

#### 4.1.1 接続方法(vMix・USBモード)

PCと本機を、データ転送対応のUSBケーブルで接続してください。  
イーサネットアダプターとして認識され、IPに `172.31.x.2` が設定されます（サブネットの第3オクテット `x` は設定で変更可能です）。  
複数台を同一PCに接続する場合はIPの重複を避けるため、設定画面で第3オクテット（`x`）を変更してください。

<a id="section-4-1-2"></a>

#### 4.1.2 接続方法(vMix・LANモード)

本機にUSBで給電し、LANケーブルを接続してください。DHCP対応環境の場合、自動的にIPが設定されます。  
設定画面からvMixのIPを設定し、接続してください。  
DHCPに対応していない環境の場合、IPを手動設定する必要があります。  
詳しくは[4.4.2 LAN 配下（LAN搭載モデル）](#section-4-4-2) をご確認ください。

<a id="section-4-1-3"></a>

#### 4.1.3 接続方法(ATEMモード)

本機にUSBで給電し、ATEM と同じネットワークへLANケーブルで接続してください。  
ATEM モードは有線LAN専用です。USB は給電専用で、PC にはネットワークアダプターやストレージとして認識されません。

1. ATEM 本体の IP アドレスを確認します（ATEM Software Control などで確認できます）。
2. 本機の `Settings → LAN → 1: ATEM IP` で、接続先の ATEM IP を設定します。
3. 本機の LAN 側 IP は、通常は DHCP で自動取得されます。固定IPにする場合は `Settings → LAN → 2: IP` で `Static` を選び、`3: Static IP` で値を設定します。
4. 接続できると、メイン画面の `Status` が `ready` になります。

ATEM IP の初期値は `192.168.1.10` です。ATEM の制御ポートは UDP 9910 を使用します。  
vMix モードから切り替えた場合、vMix モードで設定していた接続先 IP がそのまま ATEM IP として使われます。ATEM に接続する前に、必ず LAN メニューで ATEM IP を確認してください。

<a id="section-4-2"></a>

### 4.2 メイン画面の表示内容

<a id="section-4-2-1"></a>

#### 4.2.1 vMixモード

電源投入後、通常は Status 画面が表示されます。

| 表示行 | 内容 | 補足 |
| :--- | :--- | :--- |
| Status | `connected` / `disconnected` | vMixとの接続状態。接続中でも選択Mixが使えない場合は `connected (!mix)` となることがあります |
| Controller IP | 本機のIPv4 | 未取得時は `---.---.---.---` |
| vMix IP | 接続先vMixのIP | 設定値 |
| vMix Version | vMixのバージョン | 未取得時は `-` |
| Mix | Main または Mix 2～Mix 16 | 操作対象のMix。はMixが利用できない際は`(!mix)`と表示されます |
| PRV / PGM | プレビュー・プログラムの入力番号 | Mixが使えないときは `N/A`。未取得は `-` |

Status 画面での操作:

- Cut、Auto、Custom 1～4 は vMix へコマンドを送ります。
  - Custom 1~4 の動作は、[4.4.5 Transition Settings](#section-4-4-5) をご確認ください。
  - ShiftとCustomを同時押しすると、Stinger／Overlay の5～8番など、Shift対応の割り当てになります。
- Menu でメインメニューに入れます（下の条件を満たすときだけ）。
- Back はメニューから戻るときや、オーバーレイを閉じるときに使います。

<a id="section-4-2-2"></a>

#### 4.2.2 ATEMモード

電源投入後、ATEM の状態画面が表示されます。画面左上のタイトルは `ATEM` です。

| 表示行 | 内容 | 補足 |
| :--- | :--- | :--- |
| ATEM Control | 画面名 | 常に表示されます |
| Status | `ready` / `connecting` / `disconnected` | `ready` は緑、`connecting` は黄、`disconnected` は赤で表示されます |
| Controller IP | 本機のIPv4 | 未取得時は `---.---.---.---` |
| ATEM IP | 接続先ATEMのIP | 設定値 |
| Target ME | 操作対象のM/E | `ME1 / 2` のように、選択中のM/EとATEMが持つM/E数を表示します。M/E数が未取得のときは `ME1` のみ表示されます |
| Next | 次に実行されるトランジション | `Next: Mix 25f` のように種別とレート（フレーム）を表示します。未取得時は `Next: ---` |

Status画面での操作:

- Custom 1～4 は、選択中のM/EのPreview入力を1～4に切り替えます。`Status` が `ready` のときだけ動作します。
- Cut は選択中のM/EでCut、Auto は選択中のM/EでAutoトランジションを実行します。
- Menu でメインメニューに入れます。Back はメニューから戻るときに使います。
- Shift はATEMモードでは使用しません。
- トランジションの種別と時間はATEM側の設定が使われます。本機からは変更できません。画面の `Next` はATEMから取得した次回トランジションの表示です。

Menuボタンでメインメニューが開きます。

<a id="section-4-3"></a>

### 4.3 メニュー内のボタン対応（共通）

メニューや設定画面では、画面下のヒントに合わせて次のように割り当てられます。

| 物理ボタン | おおよその意味 |
| :--- | :--- |
| Custom 1 | Input1（選択1、カーソル上など） |
| Custom 2 | Input2（選択2、カーソル下など） |
| Custom 3 | Input3（値を減らす、切り替えなど） |
| Custom 4 | Input4（値を増やす、次の選択など） |
| Auto | 確定・適用・Yes など（画面に Auto: と表示） |
| Cut | 5行目の項目を選ぶ（メインメニューの `[Cut] Switch to ...` など） |

<a id="section-4-4"></a>

### 4.4 メニュー階層

以下のツリーは、vMix モードかつ LAN搭載モデルを基準にしています。USB専用モデルでは一部存在しない項目が存在します。ATEM モードのメニューは [4.4.7](#section-4-4-7) を参照してください。

<a id="section-4-4-1"></a>

#### 4.4.1 メインメニュー

| 行 | 選択 | 遷移先 |
| :--- | :--- | :--- |
| [1] | Settings | Settings → System（システム設定の入口） |
| [2] | Help (URL) | マニュアルURLとQR |
| [3] | License | 利用しているオープンソースソフトウェアのライセンス抜粋 |
| [4] | Reboot | 再起動の確認 |
| [Cut] | Switch to ATEM | モード切替の確認画面。`Auto` で ATEM モードに切り替わり、再起動します |

<a id="section-4-4-2"></a>

#### 4.4.2 LAN 配下（LAN搭載モデル）

LAN メニュー

- 1: vMix IP → LAN 経由の vMix IP 編集（接続がLANのときはオクテット編集と Auto で保存・再接続）
- 2: IP: DHCP または Static → LAN IP モードの切替と適用
- 3: Static IP → 固定IPの編集と Auto で適用

<a id="section-4-4-3"></a>

#### 4.4.3 USB 配下

USB メニュー

- 1: vMix IP → USBテザー時のPC側アドレスを表示（読み取り専用）
- 2: USB DHCP → `172.31.x.0/30` の x を変更。`Auto save+reboot`で保存し再起動

<a id="section-4-4-4"></a>

#### 4.4.4 Link Mode（LAN搭載モデル）

LAN と USB を選択し、`Auto+reboot`で保存して再起動。Backでキャンセル。

<a id="section-4-4-5"></a>

#### 4.4.5 Transition Settings

Settings / Transition Settingsで設定可能な項目の一覧です。

| 行 | 項目 | 内容 |
| :--- | :--- | :--- | 
| 0 | Mix | Main または Mix 2～16
| 1 | Cut mode | `Cut`/`CutDirect`の選択
| 2 | Cut: when | Cutを実行するタイミングです。Press(押下時) / Release(リリース時) |
| 3 | Auto: when | 同上 | 
| 4 | Custom 1-4: when | 同上 | 
| 5 | Custom button function | `Stinger`/`Overlay`/`Transition Buttons`の選択。Main Mixのみ対応 | 
| 6 | Auto type | Auto ボタン用のトランジション種別 |
| 7 | Auto type (Shift) | Shift+Auto 用 |
| 8 | Auto duration | Auto Transitionの時間（10ms単位）|
| 9 | Auto duration (Shift) | Shift 側の時間 | 
| 10 | Factory reset | 初期値に戻す（確認画面へ） | 

Autoで選べるトランジション名の例: `Fade`, `Merge`, `Zoom`, `Wipe`, `Slide`, `Fly`, `CrossZoom`, `FlyRotate`, `Cube`, `CubeZoom`, `VerticalWipe`, `VerticalSlide`, `WipeReverse`, `SlideReverse`, `VerticalWipeReverse`, `VerticalSlideReverse`, `BarnDoor`, `RollerDoor`, `AlphaFade`

<a id="section-4-4-6"></a>

#### 4.4.6 Help / License

Help はマニュアルURLとQRコードを表示します。  
License は主要なOSS名とライセンス種別を抜粋して表示します。

<a id="section-4-4-7"></a>

#### 4.4.7 ATEM モードのメニュー

ATEM モードのメニューは次のとおりです。項目の選択は Custom 1～4、5行目は Cut、確定は Auto です。

メインメニュー

| 行 | 選択 | 内容 |
| :--- | :--- | :--- |
| [1] | Settings | ATEM の設定メニュー |
| [2] | Developer | ビルド情報。Auto でライセンス一覧を開きます |
| [3] | License | 利用しているオープンソースソフトウェアのライセンス一覧 |
| [4] | Reboot | 再起動の確認 |
| [Cut] | Switch to vMix | モード切替の確認画面。`Auto` で vMix モードに切り替わり、再起動します |

Settings

- [1] LAN → LAN メニュー
  - 1: ATEM IP → 接続先 ATEM IP の編集。Custom 1/2 で桁を移動、Custom 3/4 で値を変更、Auto で保存して再接続します。
  - 2: IP: DHCP / Static → LAN 側 IP の切替。Custom 1 で DHCP／Static を切り替え、Custom 2 で適用します。適用すると再起動します。
  - 3: Static IP → 固定IPの編集。Custom 1/2 で桁を移動、Custom 3/4 で値を変更、Auto で適用して再起動します。
- [2] Target ME → 操作対象の M/E を選択。Custom 3/4 で変更し、Auto で保存します。ATEM から M/E 数が取得できている場合は、その範囲内でのみ選択できます。
- [3] Restart → 再起動の確認

ATEM モードには USB メニュー、vMix IP、Link Mode、Transition Settings はありません。LAN IP の適用とモード切替では本体が再起動します。

<a id="section-4-5"></a>

### 4.5 設定項目と vMix 側の対応

| 項目 | 設定内容 | 備考 | 機能説明 |
| :--- | :--- | :--- | :--- |
| 対象Mix | Main Mix, Mix 2～16 | デフォルトは Main Mixを使用。 | Main以外の場合に一部の動作が変更 |
| Cut動作 | `Cut`, `CutDirect` | Main Mix のみ。Mix 2～16 は `Cut` 固定 | `Cut`はPreviewとProgramを入れ替え。`CutDirect`ではProgramのみ変更 |
| Auto | トランジション種別・継続時間 | 通常とShiftで別々に設定可能 | 
| Custom button function| カスタムボタンの動作内容 | `Stinger`で`Stinger1~8`, `Overlay`で`OverlayInput1~8`, `Transition buttons`で`Transition1~4`(Shift非対応)を起動。`Overlay`,`Transition buttons`はMix2~16指定時は使用不可能。| Transition1~4の際はvMixのUI上のトランジションボタンを起動 | 

Mixによる制約や各Functionの詳細は、vMix公式の[Shortcut Function Reference](https://www.vmix.com/help29/ShortcutFunctionReference.html)を参照してください。

<a id="section-4-6"></a>

### 4.6 ATEM モードの操作対応

ATEM モードで本機のボタンが行う操作は次のとおりです。操作対象は `Settings → Target ME` で選んだ M/E です。

| 本機の操作 | ATEM 側の動作 | 備考 |
| :--- | :--- | :--- |
| Custom 1～4 | 対象M/EのPreview入力を1～4へ変更 | `Status` が `ready` のときのみ動作 |
| Cut | 対象M/EのCut | `Status` が `ready` のときのみ動作 |
| Auto | 対象M/EのAutoトランジション | 種別・時間はATEM側の設定が使われます |
| Menu | メインメニューを開く | |
| Back | メニューから戻る | |
| Shift | 未使用 | |

- vMix モードの `Cut mode`、`Cut: when`、`Auto duration`、`Custom button function` は、ATEM モードには適用されません。
- ATEM のトランジション種別・時間・Stinger などは、ATEM 本体または ATEM Software Control で設定してください。
- 画面の `Next` は、ATEM から取得した次回トランジションの種別とレートです。

<a id="section-4-7"></a>

### 4.7 モードの切り替え（vMix / ATEM）

モードはメインメニューの `[Cut]` 行から切り替えます。切り替えると本体が再起動し、選んだモードの画面になります。

| 現在のモード | メインメニューの操作 | 確認画面 | 切替後 |
| :--- | :--- | :--- | :--- |
| vMix | `[Cut] Switch to ATEM` | `Switch to ATEM?` → `Auto: Yes` / `Back: No` | ATEM モードで再起動 |
| ATEM | `[Cut] Switch to vMix` | `Switch to vMix?` → `Auto: Yes` / `Back: No` | vMix モードで再起動 |

- 切り替え中は、現在のモードの接続（vMix または ATEM）が切れます。本番中はモードを切り替えないでください。
- vMix モードの設定（Transition Settings など）と ATEM モードの Target ME は、それぞれ保存されたまま残ります。
- 接続先 IP は vMix / ATEM で共通です。ATEM モードへ切り替えたあとは、`Settings → LAN → ATEM IP` を確認してください。
- モードは本体に保存されるため、次回起動時も同じモードで立ち上がります。

---

<a id="section-5"></a>

## 5. 免責事項

本機は将来的な製品化に向けたデータ収集を目的とした評価試験機です。  
本機を使用したことによる本番配信の停止、vMix や ATEM のフリーズ、接続PCの故障、その他一切の二次的損害について、開発者は責任を負いかねます。  
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
  A1. vMix と Blackmagic ATEM に対応しています。その他のソフトウェア・機器には対応していません。

- Q2. vMixに接続ができません。  
  A2. USBモードの場合、ネットワークアダプタとして認識されているかご確認ください。IPモードの場合はStatus の vMix IP が正しいかを確認してください。

- Q3. Mix 2~16で Cut や Custom の種別が変えられません。  
  A3. Main Mix以外では一部の設定が変更できないようロックを実施しています。

- Q4. ATEM に接続ができません。  
  A4. 有線LAN搭載モデルであること、LANケーブルが ATEM と同じネットワークに接続されていることを確認してください。`Settings → LAN → ATEM IP` が ATEM 本体の IP と一致しているか、`Status` が `ready` になるかも確認してください。ATEM の制御ポート UDP 9910 がファイアウォールなどで遮断されていないかもご確認ください。

- Q5. ATEM モードで PC から USB 機器として見えません。  
  A5. ATEM モードの USB は給電専用です。ネットワークアダプターやストレージとしては認識されません。ATEM とは LAN ケーブルで接続してください。

- Q6. vMix と ATEM を同時に操作できますか？  
  A6. できません。本機は vMix モードと ATEM モードのどちらか一方で動作します。モードを切り替えると再起動します。

- Q7. モードを切り替えると設定は消えますか？  
  A7. vMix のトランジション設定と ATEM の Target ME は、それぞれ保存されたまま残ります。接続先 IP は vMix / ATEM で共通のため、ATEM モードでは LAN メニューで ATEM IP を確認してください。

- Q8. ATEM モードで Cut / Auto の種別や時間を変えられますか？  
  A8. 本機からは変更できません。ATEM 本体または ATEM Software Control で設定してください。本機は次回トランジションの種別とレートを表示します。

---

<a id="section-8"></a>

## 8. お問い合わせ・フィードバック

不具合報告、機能要望、または現場での使用感などのフィードバックを心よりお待ちしております。  
SNSでの投稿は #Iryx をご利用ください。

* 開発元: [未完成成果物研究所](https://mikanseilaboratory.github.io)
* ファームウェア開発: [Flowing](https://github.com/FlowingSPDG)
* 回路設計・基板筐体制作: [mizuyoukan](https://github.com/mizuyoukanao)
* Contact: [ruk1ium@gmail.com](mailto:ruk1ium@gmail.com)

---
