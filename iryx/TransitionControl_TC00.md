# vMixコントローラー Iryx Transition Control TC-00 取扱説明書

## 目次

- [1. はじめに](#section-1)
- [2. 安全上のご注意](#section-2)
- [3. 動作環境](#section-3)
  - [3.1 製品の種類（LAN搭載とUSB専用）](#section-3-1)
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
  - [4.5 設定項目と vMix 側の対応](#section-4-5)
- [5. 免責事項](#section-5)
- [6. ライセンス表示について](#section-6)
- [7. よくある質問](#section-7)
- [8. お問い合わせ・フィードバック](#section-8)

<a id="section-1"></a>

## 1. はじめに

本製品は、vMixのトランジション制御に特化したコントローラーです。  
vMixの状態取得および操作をTCP API経由で行うための評価用試作機です。  
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

- vMix 29以降  
  - v28以前のvMixでは、`Stinger5～8`、`OverlayInput5～8`、Mixの選択や一部のTransitionに対応していない可能性があります。
- (USBモード) USB CDC-NCMに対応したWindows（Windows 10 Version 1903以降、Windows 11）
- (USBモード) データ転送可能なUSB-Cケーブル(USB 1.1 Full-speed)
- (LANモード) 100BASE-TX規格に対応したネットワーク

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

<a id="section-3-1-usb"></a>

#### USB専用モデル

- 接続方法はUSBのみです。
- メニュー「Settings」の設定項目もLAN搭載モデルとは一部異なります。
- USB 専用の場合、Link Mode は選択できません（`Link` は固定表示）。このとき Settings→System 入口の再起動は `[3]` に表示されます。
- USB メニュー（vMix IP の表示、USB DHCP レンジ）は LAN搭載モデルと同様です。
- PC とはデータ転送対応のUSBケーブルで接続し、本機と vMix 用PCのIPは接続方法の節(`172.31.x.x`)に従います。

---

<a id="section-4"></a>

## 4. 使用方法

<a id="section-4-1"></a>

### 4.1 接続方法

<a id="section-4-1-1"></a>

#### 4.1.1 接続方法(USBモード)

PCと本機を、データ転送対応のUSBケーブルで接続してください。  
イーサネットアダプターとして認識され、IPに `172.31.x.2` が設定されます（サブネットの第3オクテット `x` は設定で変更可能です）。  
複数台を同一PCに接続する場合はIPの重複を避けるため、設定画面で第3オクテット（`x`）を変更してください。

<a id="section-4-1-2"></a>

#### 4.1.2 接続方法(LANモード)

本機にUSBで給電し、LANケーブルを接続してください。DHCP対応環境の場合、自動的にIPが設定されます。  
設定画面からvMixのIPを設定し、接続してください。  
DHCPに対応していない環境の場合、IPを手動設定する必要があります。  
詳しくは[4.4.2 LAN 配下（LAN搭載モデル）](#section-4-4-2) をご確認ください。

<a id="section-4-2"></a>

### 4.2 メイン画面の表示内容

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

<a id="section-4-4"></a>

### 4.4 メニュー階層

以下のツリーは、LAN搭載モデルを基準にしています。USB専用モデルでは一部存在しない項目が存在します。

<a id="section-4-4-1"></a>

#### 4.4.1 メインメニュー

| 行 | 選択 | 遷移先 |
| :--- | :--- | :--- |
| [1] | Settings | Settings → System（システム設定の入口） |
| [2] | Help (URL) | マニュアルURLとQR |
| [3] | License | 利用しているオープンソースソフトウェアのライセンス抜粋 |
| [4] | Reboot | 再起動の確認 |

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

<a id="section-4-5"></a>

### 4.5 設定項目と vMix 側の対応

| 項目 | 設定内容 | 備考 | 機能説明 |
| :--- | :--- | :--- | :--- |
| 対象Mix | Main Mix, Mix 2～16 | デフォルトは Main Mixを使用。 | Main以外の場合に一部の動作が変更 |
| Cut動作 | `Cut`, `CutDirect` | Main Mix のみ。Mix 2～16 は `Cut` 固定 | `Cut`はPreviewとProgramを入れ替え。`CutDirect`ではProgramのみ変更 |
| Auto | トランジション種別・継続時間 | 通常とShiftで別々に設定可能 | 
| Custom button function| カスタムボタンの動作内容 | `Stinger`で`Stinger1~8`, `Overlay`で`OverlayInput1~8`, `Transition buttons`で`Transition1~4`(Shift非対応)を起動。`Overlay`,`Transition buttons`はMix2~16指定時は使用不可能。| Transition1~4の際はvMixのUI上のトランジションボタンを起動 | 

Mixによる制約や各Functionの詳細は、vMix公式の[Shortcut Function Reference](https://www.vmix.com/help29/ShortcutFunctionReference.html)を参照してください。

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
  A2. USBモードの場合、ネットワークアダプタとして認識されているかご確認ください。IPモードの場合はStatus の vMix IP が正しいかを確認してください。

- Q3. Mix 2~16で Cut や Custom の種別が変えられません。  
  A3. Main Mix以外では一部の設定が変更できないようロックを実施しています。

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
