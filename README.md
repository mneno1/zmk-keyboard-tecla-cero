
# TECLA-CERO
分割キーボード用のZMKファームウェア

## 特徴
- ロータス配列
- 38キー
- 左側にロータリーエンコーダー
- 右側にトラックボール（PAW3222）搭載
- BMP Boost使用
- BLE/USB両対応
- keymap-editor / ZMK Studio対応 

## ビルド

GitHub Actionsで自動ビルドされます。pushするとビルドが実行され、Artifactsからuf2ファイルをダウンロードできます。

### ビルドアーティファクト

| ファイル名 | 説明 |
|-----------|------|
| `tecla_cero_right_central` | 右側（セントラル）- トラックボール搭載側 |
| `tecla_cero_left_peripheral` | 左側（ペリフェラル） |
| `tecla_cero_left_central` | 左側（セントラル）- 左側をUSBに接続する場合 |
| `tecla_cero_right_peripheral` | 右側（ペリフェラル）- 左側をUSBに接続する場合 |
| `settings_reset` | 設定リセット用 |

## 書き込み

`_central`がついているuf2をトラックボールがついている方（右側）に、`_peripheral`を反対側（左側）に書き込んでください。

## キーマップ編集

- [ZMK Studio](https://zmk.studio/)やkeymap-editorで編集可能
- `config/keymap.keymap`を直接編集してpushすることも可能
- ロータリーエンコーダのバインディングはZMK Studioでは現在編集できません。`config/keymap.keymap`の各レイヤーの`sensor-bindings`を直接編集するかkeymap-editorで変更してください。
