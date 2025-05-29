# nRF52840 BLE Sniffer Setup

> Convert your nRF52840 USB Dongle into a powerful Bluetooth Low Energy packet analyzer

## 概要

このガイドでは、Nordic Semiconductor社の**nRF52840 USB Dongle**をBLE（Bluetooth Low Energy）パケットスニファーとして設定する方法を説明します。

### 何ができるようになるか

- 📡 BLE通信をリアルタイムでキャプチャ
- 🔍 Wiresharkで詳細なパケット解析
- 🔐 暗号化されたBLE通信の復号（キーがある場合）
- 📊 BLEデバイスの挙動分析とデバッグ

### 対象読者

- BLEデバイスの開発・デバッグを行う開発者
- IoTセキュリティの研究者
- BLE通信の仕組みを学びたい学習者

### 必要なもの

- **nRF52840 USB Dongle**
  - [Nordic公式版](https://www.nordicsemi.com/Products/Development-hardware/nRF52840-Dongle)（約$10）
  - [Switch Science版](https://www.switch-science.com/products/10014)（本ガイドで動作確認済み）
- macOS環境（本ガイドはmacOS向け）
- Python 3（ExtCapスクリプト実行用）
- [Wireshark](https://www.wireshark.org/)（無料）

> ℹ️ **動作確認環境**: Switch Science製「nRF52840 MDBT50Q 開発用USBドングル（Type-Cコネクタ）」で動作確認を行いました。

---

## セットアップ手順

### 1. ファームウェア書き込み

**使用ツール**: [nRF Connect for Desktop](https://www.nordicsemi.com/Products/Development-tools/nRF-Connect-for-Desktop/Download)

**ファームウェア**: [nRF Sniffer for Bluetooth LE](https://www.nordicsemi.com/Products/Development-tools/nRF-Sniffer-for-Bluetooth-LE)

- バージョン: 4.1.1
- ファイル: `nrf_sniffer_for_bluetooth_le_4.1.1.zip`

**書き込み手順**:

1. nRF Connect for Desktopの「Programmer」アプリを起動
2. USB Dongleをリセットボタンを押しながら接続（DFUモード）
3. hexファイル（`sniffer_nrf52840dongle_nrf52840_4.1.1.hex`）をドラッグ&ドロップ
4. 「Write」ボタンで書き込み実行

### 2. Wireshark ExtCap設定

**必要なファイル**:

- `nrf_sniffer_ble.py`
- `SnifferAPI/` フォルダ

**配置場所**: `~/.local/lib/wireshark/extcap/`

**依存関係**（システム全体にインストール）:

```bash
pip3 install pyserial psutil --break-system-packages
```

### 3. 最終的な構成

**保持するもの**:

- nRF Connect for Desktop
- Wireshark ExtCapファイル（`~/.local/lib/wireshark/extcap/`）
- pyserial, psutil（システムPythonパッケージ）

### 4. 使用方法

1. Wiresharkを起動
2. インターフェース一覧で「nRF Sniffer for Bluetooth LE」を選択
3. BLE通信をキャプチャ・解析
