# Pressure Check

天気痛向けの気圧チェック PWA。保存した地点（GPSで取得）の気圧予報を、その場で取得して表示します。

- 公開URL: https://arvelt.github.io/pressure-check/
- インストール: スマホのブラウザでURLを開き、メニューから「アプリをインストール／ホーム画面に追加」

## 仕様

- データ: Open-Meteo Forecast API（1時間ごとの地上気圧 `surface_pressure`）。日本域は気象庁の数値予報モデルが元データ。APIキー不要
- 地点: 初回に GPS（Geolocation API）で取得し、ブラウザの localStorage にのみ保存。サーバーには送られない（予報取得のリクエストに座標が含まれるのみ）
- 判定基準: 3時間で2〜4hPa低下＝注意、4hPa以上＝警戒、6時間で6hPa以上低下＝警戒（連続する該当時間を「窓」としてまとめて表示）
- 取得失敗時: 前回取得データを「取得失敗・最終取得時刻」つきで明示して表示
- 通知機能なし（通知は別途、毎朝の気圧アラートが担当）

## 構成

- `index.html` — 本体（HTML/CSS/JS 1ファイル、グラフは Canvas 自前描画）
- `manifest.webmanifest` — PWA 定義
- `sw.js` — Service Worker（アプリ本体のキャッシュと更新）
- `icon-192.png` / `icon-512.png` — アイコン

## 更新

リポジトリへ push すると GitHub Pages に自動反映され、インストール済み PWA は次回起動時に更新されます。
