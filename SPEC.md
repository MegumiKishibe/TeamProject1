# TeamProject1

PHP (Laravel) + MySQL + Docker (Laravel Sail) の開発環境

---

## 🚀 環境構築手順

### 1. 前提条件
- Docker Desktop がインストールされていること  
  - Windows の場合は **WSL2** を有効化しておく  
- Node.js (推奨 v18 以上)  
- npm (確認: `npm -v`)

---

### 2. プロジェクトのセットアップ
```bash
# リポジトリをクローン
git clone git@github.com:<MegumiKishibe>/TeamProject1.git
cd TeamProject1/example-app

# Sail をバックグラウンドで起動
./vendor/bin/sail up -d

# PHP の依存パッケージをインストール
./vendor/bin/sail composer install

# .env を作成
cp .env.example .env

# アプリキー生成
./vendor/bin/sail artisan key:generate

# DB マイグレーション
./vendor/bin/sail artisan migrate
```
### 3. フロントエンド環境
```bash
# npm パッケージをインストール
./vendor/bin/sail npm install

# 開発サーバー起動
./vendor/bin/sail npm run dev
ブラウザで  
👉 [http://localhost](http://localhost) にアクセスして Laravel の画面が表示されれば成功です 🎉  
```

### 4. データベースの初期化（任意）
Seeder が用意されている場合：
```bash
./vendor/bin/sail artisan db:seed
```

### 5. よく使うコマンド
```bash
# コンテナ起動
./vendor/bin/sail up -d

# コンテナ停止
./vendor/bin/sail down

# artisan コマンド
./vendor/bin/sail artisan <command>

# composer コマンド
./vendor/bin/sail composer <command>

# npm コマンド
./vendor/bin/sail npm <command>
```
## 🔧 ブランチ運用ルール
- main ブランチは直接 push 禁止（保護ルールあり）  
- 開発は以下のフローで進める  
- `feature/<機能名>` ブランチ作成  
- 作業 → push → Pull Request 作成  
- PR レビュー後、main に squash merge  



## 📂 ディレクトリ構成（主要部分）
```text
example-app/
├── app/              # アプリケーション本体
├── bootstrap/        # 初期化処理
├── config/           # 設定ファイル
├── database/         # マイグレーション / Seeder
├── public/           # 公開ディレクトリ（入口）
├── resources/        # フロントリソース (Blade, CSS, JS)
├── routes/           # ルーティング定義
├── storage/          # キャッシュ / ログ
├── tests/            # テストコード
└── vendor/           # Composer が管理（Git には含めない）
```
## ✅ 注意点

- `vendor/` と `node_modules/` は Git に含めません（`.gitignore` 済み）  
- 初回セットアップ時は必ず以下を実行してください  
  ```bash
  ./vendor/bin/sail composer install
  ./vendor/bin/sail npm install
  ```
main ブランチへの直接 push はできません（保護ルールあり）

作業は必ず feature/<機能名> ブランチを切って進めてください

DB の構造変更は マイグレーションで管理し、既存のマイグレーションファイルは書き換えずに新規追加してください

