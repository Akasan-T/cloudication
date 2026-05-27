# ☁️ クモニケーション / cloudication

> 匿名で「雲」を投稿・共有できるWebアプリケーション — *Clouds, Shared Anonymously*

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat-square&logo=express&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=flat-square&logo=prisma&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![AWS S3](https://img.shields.io/badge/AWS_S3-FF9900?style=flat-square&logo=amazons3&logoColor=white)

---

## 📌 概要

「雲」をテーマにした匿名投稿Webアプリです。  
ユーザーはアカウント登録不要で気軽に投稿でき、Mapboxの地図上に雲のように投稿が広がっていくUIが特徴です。  
フロントエンド・バックエンドを分離したモノレポ構成で、TypeScriptで統一されたコードベースを実現しています。

---

## 🏗️ アーキテクチャ

```
cloudication/
├── apps/
│   ├── api/    # Express + Prisma + PostgreSQL（REST API）
│   └── web/    # Next.js + Mapbox GL（フロントエンド）
├── packages/
│   └── shared-types/  # フロント・バック共通の型定義
└── docker-compose.yml
```

**モノレポ構成**でフロント・バックエンドの型を`shared-types`パッケージで共有し、型安全な開発を実現しています。

---

## 🛠️ 技術スタック

| カテゴリ | 使用技術 |
|---|---|
| フロントエンド | Next.js / React / TypeScript |
| 地図表示 | Mapbox GL / react-map-gl |
| バックエンド | Express.js / TypeScript |
| ORM | Prisma |
| データベース | PostgreSQL |
| ファイルストレージ | AWS S3（multerによるアップロード） |
| セキュリティ | Helmet / express-rate-limit |
| インフラ | Docker / Docker Compose |
| デプロイ | Railway |

---

## ✨ 主な機能・実装のポイント

- **匿名投稿** ― ユーザー登録不要で投稿を作成・共有
- **地図UI** ― Mapboxを使用した投稿の地図上ビジュアライゼーション
- **ファイルアップロード** ― multer + AWS S3による画像ストレージ
- **型安全** ― shared-typesで API の req/res 型をフロント・バック間で共通化
- **セキュリティ** ― Helmet（HTTPヘッダー保護）・レートリミット実装
- **コンテナ化** ― Docker Composeでローカル環境を完全再現

---

## 🚀 ローカル環境構築

### 1. リポジトリのクローン

```bash
git clone https://github.com/Akasan-T/cloudication.git
cd cloudication
```

### 2. 環境変数の設定

`.env` をルートディレクトリに作成（`.env.example` をコピーすれば動作可能）

```env
# database
POSTGRES_USER="user"
POSTGRES_PASSWORD="password"
POSTGRES_DB="appdb"
DATABASE_URL="postgresql://user:password@db:5432/appdb"

# backend
BACKEND_PORT="8000"

# frontend
FRONTEND_PORT="3000"
NEXT_PUBLIC_API_URL="http://localhost:8000"
```

### 3. 起動

```bash
make up        # コンテナ起動
make migrate   # マイグレーション & Prisma Client 生成
make seed      # 仮データ投入
```

| コマンド | 説明 |
|---|---|
| `make up` | 全コンテナ起動 |
| `make down` | コンテナ停止 |
| `make dev` | 開発モードで起動 |
| `make prisma` | Prisma Studio 起動 |
| `make logs` | ログ確認 |
