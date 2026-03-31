---
title: "ソフトウェアのセットアップ"
description: "uConsole向けOpenterface KVM拡張のソフトウェアセットアップ完全ガイド。"
keywords: "Openterface アプリ インストール, uConsole ソフトウェア, KVM セットアップ, uConsole 設定"
---

# **ソフトウェアのセットアップ** | Openterface KVM拡張 for uConsole

## インストール概要

Openterfaceアプリにより、uConsoleをKVMインターフェースとして使用でき、内蔵の画面・キーボード・トラックボールでターゲット機器を操作できます。

!!! note "要件"
    - **uConsole**: Openterfaceアプリのインストールが必要
    - **ターゲット**: アプリ不要 — Windows, macOS, Linux, Android, iOS対応
    - **映像**: 標準のHDMIケーブルを使用してください。電源付きのHDMIコンバータを使用すると、**VGA**や**DP**などの形式にも対応します。*ヒント: コンバータに十分な電力が供給されていることを確認してください。供給不足だと黒画面になる場合があります。*

    - **推奨ビデオバックエンド**: arm64 GPU（例: Raspberry Pi）でのパフォーマンスと互換性を高めるため、ビデオバックエンドに**GStreamer**を推奨します。ただし、**Kali Linux**ではGStreamerのサポートが不十分な場合があります。

## インストール方法

### **オプション1: GitHub Releasesからダウンロード（arm64推奨）**

最新のOpenterfaceアプリ（**arm64**）を当プロジェクトの[GitHub Releases](https://github.com/TechxArtisanStudio/Openterface_QT/releases)から直接ダウンロードしてください。

1. [Openterface_QT Releases](https://github.com/TechxArtisanStudio/Openterface_QT/releases)ページにアクセスします。
2. **arm64**用の最新の`.deb`パッケージをダウンロードします（例: `openterfaceqt_*_arm64.deb`）。
3. パッケージをインストールします:
   ```bash
   sudo apt install ./openterfaceqt_*_arm64.deb
   ```
   *(実際のファイル名に置き換えてください)*

---

### **オプション2: Flatpakでのインストール**

詳細は[Flatpakインストールガイド](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md)を参照してください。

---

### **オプション3: コミュニティリポジトリ**

Rexがメンテナンスするコミュニティビルドを利用する場合：

1. **リポジトリを追加**:
    ```bash
    wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
    sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
    ```

2. **パッケージをインストール**:
    ```bash
    sudo apt update
    sudo apt install openterfaceqt
    ```

!!! warning "リポジトリについて"
    これらのコマンドは`sudo`が必要です。リポジトリはarm64 Bookwormパッケージを対象としているため、導入前にデバイスの互換性を確認してください。

## 重要な注意点

!!! tip "電源と初回セットアップ"
    - **uConsoleが十分に充電されているか、安定した電源に接続されていることを確認してください。** 電力不足は不安定な動作や接続問題を引き起こす可能性があります。
    - **初回にターゲットを制御できない場合:**
        1. uConsoleを完全にシャットダウンします。
        2. 少なくとも10秒待ちます。
        3. 再度起動して試してください。

!!! tip "シリアル通信のボーレート"
    - シリアル通信では**9600ボーレート**を使用してください。uConsoleは115200を安定して維持するのに十分な電力を供給できないことが多く、エラー率が上がるためです。

## 使用手順

### **KVMセッションの開始**
1. uConsoleでOpenterfaceアプリを起動します
2. アプリがKVM拡張ボードを自動検出します
3. HDMIでターゲット機器を接続します
4. uConsole内蔵のキーボードとトラックボールでターゲットを操作します

### **制御機能**
- **キーボード**: マルチメディアキーを含むフルキーボードエミュレーション
- **マウス**: 絶対および相対位置指定
- **オーディオ**: HDMIオーディオをuConsoleスピーカーにパススルー

### **高度な機能**
- **テキスト転送**: キーストロークをエミュレートしてテキストを素早く送信—ユーザー名、パスワード、コード断片に最適
- **切替可能なUSB**: ホストアプリでuConsoleとターゲット間のUSBアクセスを切り替え可能
---
title: "ソフトウェアセットアップ"
description: "Openterface KVM Extension for uConsole の完全なソフトウェアセットアップガイド。シームレスな KVM 機能のために uConsole に Openterface App をインストールして設定する方法を学びます。"
keywords: "Openterfaceアプリインストール, uConsoleソフトウェアセットアップ, KVMアプリセットアップ, uConsoleアプリ設定, ソフトウェアインストールガイド"
---

# **ソフトウェアセットアップ** | Openterface KVM Extension for uConsole

## インストール概要

Openterface App により、uConsole が KVM インターフェースとして機能し、内蔵画面、キーボード、トラックボールを使用してターゲットデバイスを制御できます。

!!! note "要件"
    - **uConsole**：Openterface App のインストールが必要
    - **ターゲット**：アプリ不要 - Windows、macOS、Linux、Android、iOS をサポート
    - **ビデオ**：標準 HDMI ケーブルを使用してください。標準 HDMI ケーブルを使用してください。電源付き HDMI コンバーターを使用すると、**VGA**、**DP** などの他のフォーマットもサポートします。*ヒント：コンバーターが適切に電源供給されていることを確認してください。そうしないと、黒い画面が表示される可能性があります。*

## インストール方法

### **オプション 1：Flatpak インストール**

詳細なセットアップ手順については、[Flatpak インストールガイド](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md) に従ってください。

### **オプション 2：コミュニティリポジトリ（推奨）**

Rex が管理するコミュニティビルドを希望する場合：

1. **リポジトリの追加**：
```bash
wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
```

2. **パッケージのインストール**：
```bash
sudo apt update
sudo apt install openterfaceqt
```

!!! warning "リポジトリの注意事項"
    これらのコマンドには sudo が必要です。リポジトリは arm64 Bookworm パッケージを対象としています。インストール前にデバイスとの互換性を確認してください。

## 使用方法

### **KVM セッションの開始**
1. uConsole で Openterface App を起動
2. アプリは自動的に KVM Extension ボードを検出
3. HDMI でターゲットデバイスを接続
4. uConsole の内蔵キーボードとトラックボールを使用してターゲットデバイスを制御

### **制御機能**
- **キーボード**：マルチメディアキーを含む完全なキーボードエミュレーション
- **マウス**：絶対および相対マウス位置
- **オーディオ**：HDMI オーディオを uConsole スピーカーにパススルー

### **高度な機能**
- **テキスト転送**：キーストロークをシミュレートしてテキストを迅速に転送—ユーザー名、パスワード、コードスニペットに最適
- **切り替え可能 USB**：ホストアプリを使用して uConsole とターゲットデバイス間で USB アクセスを簡単に切り替え
