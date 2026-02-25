# Custom Chat (FiveM)

## 概要

FiveM の標準 `chat` リソースをベースに、**Tab補完機能**を追加した改修版です。  
あわせて、リソース名を `chat` 以外（例: `chat-local`）に変更しても動作するように調整しています。

### この配布版のポイント
- **チャット入力中の Tab補完** に対応（`/` コマンド入力補助）
- **リソース名変更対応**（`chat-local` / `chat-custom` など）
- **チャット終了後のフォーカス残り対策** 済み
- **配布向け軽量構成**（ビルド不要でそのまま使える想定）

---

## 導入方法（配布版）

### 1. フォルダを配置
配布フォルダをそのまま `resources` 配下へ配置します。

例:
```txt
resources/[local]/chat-local
```

> フォルダ名は `chat-local` を推奨（`chat` だと内蔵リソースと競合しやすいため）

---

### 2. `server.cfg` を設定
内蔵 `chat` は使わず、配布版を起動するように設定します。

```cfg
# デフォルトchatは使わない（コメントアウト）
# ensure chat

# 配布版chat
ensure chat-local
```

---

### 3. サーバーコンソールで反映
サーバー起動中に追加した場合は、コンソールで `refresh` 後に起動してください。

```txt
refresh
ensure chat-local
```

---

## 使い方

### チャットを開く
- `T` キーでチャットを開く（FiveM標準）

### Tab補完
- `/` から始まるコマンド入力中に **Tab** で補完候補を巡回
- 例: `/ca` → `Tab` で `/car` など

> ※ 環境やコマンド登録状況によって候補の内容は変わります

---

## 配布版の注意点

### 1) ビルド不要版です
この配布版は **ビルド済み（`dist/` 同梱）** 前提です。  
通常の利用では `yarn` / `webpack` は不要です。

### 2) リソース名を変える場合
`chat-local` 以外の名前でも動作します（例: `chat-custom`）。

その場合は `server.cfg` の `ensure` 名も合わせて変更してください。

例:
```cfg
ensure chat-custom
```

---

## 配布フォルダ構成（参考）

```txt
chat-local/
├─ fxmanifest.lua
├─ cl_chat.lua
├─ sv_chat.lua
├─ dist/
│  ├─ ui.html
│  ├─ index.css
│  └─ chat.js
└─ html/
   └─ vendor/
      ├─ *.css
      └─ fonts/
```

---

## トラブルシュート

### Q. `T` で一度チャットを開くと、その後キー操作できなくなる
- この配布版では対策済みです
- もし発生する場合は、別の `chat` リソース（内蔵版）が起動していないか確認してください

### Q. `chat-local` が認識されない
- `refresh` を実行してから `ensure chat-local`
- フォルダ構成を確認（`fxmanifest.lua` が直下にあるか）
- `dist/ui.html` が存在するか確認

### Q. `webpack.config.js がない` と出る
- 配布版でそのエラーが出る場合、`fxmanifest.lua` が開発版のものになっている可能性があります
- 配布版の `fxmanifest.lua` に差し替えてください

---

## ベースリソースについて

このリソースは Cfx.re / `cfx-server-data` の `chat` をベースにしています。  
配布・公開時は必要に応じて元リソースのライセンス/クレジット表記を確認してください。
