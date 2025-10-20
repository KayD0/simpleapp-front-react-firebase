# React SPA Go Postgres アプリケーション

Firebase認証を使用したReact SPAとGoバックエンドのウェブアプリケーション

## 目次

- [概要](#概要)
- [主な機能](#主な機能)
- [技術スタック](#技術スタック)
- [システムアーキテクチャ](#システムアーキテクチャ)
- [セットアップ手順](#セットアップ手順)
  - [前提条件](#前提条件)
  - [APIキーの取得](#apiキーの取得)
  - [バックエンドのセットアップ](#バックエンドのセットアップ)
  - [フロントエンドのセットアップ](#フロントエンドのセットアップ)
- [開発ガイド](#開発ガイド)
- [使用方法](#使用方法)
- [プロジェクト構造](#プロジェクト構造)
- [トラブルシューティング](#トラブルシューティング)
- [ライセンス](#ライセンス)

## 概要

このアプリケーションは、ユーザーがFirebase認証でログインし、プロフィール情報を管理できるシンプルなウェブアプリケーションです。バックエンドはGoで実装され、フロントエンドはReact（Vite）とBootstrapで構築されています。データベースにはPostgreSQLを使用しています。

## 主な機能

- **ユーザー認証**: Firebase Authenticationを使用したユーザー登録・ログイン機能
- **認証トークン検証**: バックエンドでのFirebase IDトークン検証
- **レスポンシブUI**: モバイルデバイスにも対応したユーザーインターフェース
- **プロフィール管理**: ユーザープロフィール情報の管理機能

## 技術スタック

### フロントエンド

- **React**: UIライブラリ
- **Vite**: モジュールバンドラー・開発サーバー
- **Bootstrap 5**: UIコンポーネントとレスポンシブデザイン
- **Firebase SDK**: 認証とIDトークン管理
- **SCSS**: スタイリングの拡張機能

### クラウドサービス

- **Firebase Authentication**: ユーザー認証

## システムアーキテクチャ

このアプリケーションは以下のコンポーネントで構成されています：

1. **フロントエンド（React SPA）**: ユーザーインターフェースを提供し、Firebase SDKを使用して認証を処理します。
2. **バックエンド（Go API）**: フロントエンドからのリクエストを処理し、データベースとの通信を行います。
3. **データベース（PostgreSQL）**: ユーザープロフィールなどのデータを永続化します。
4. **Firebase Authentication**: ユーザー認証サービスを提供します。

## セットアップ手順

### 前提条件

- Node.js 14以上
- npm または yarn
- PostgreSQL
- Google Cloudアカウント
- Firebaseプロジェクト

#### Firebase設定

1. [Firebase Console](https://console.firebase.google.com/)にアクセス
2. プロジェクトを作成または選択
3. Authentication機能を有効化し、メール/パスワード認証を設定
4. プロジェクト設定からWebアプリを追加
5. 提供されるFirebase設定オブジェクトをコピー
6. プロジェクト設定 > サービスアカウントから新しい秘密鍵を生成

### フロントエンドのセットアップ

1. リポジトリをクローン:
   ```bash
   git clone <repository-url>
   cd <repository-name>
   ```

2. フロントエンドディレクトリに移動:
   ```bash
   cd front
   ```

3. 依存関係をインストール:
   ```bash
   npm install
   # または
   yarn
   ```

4. `.env.example`をコピーして`.env`ファイルを作成:
   ```bash
   cp .env.example .env
   ```

5. `.env`ファイルを編集し、Firebase設定を追加:
   ```
   VITE_FIREBASE_API_KEY=あなたのapiKey
   VITE_FIREBASE_AUTH_DOMAIN=あなたのauthDomain
   VITE_FIREBASE_PROJECT_ID=あなたのprojectId
   VITE_FIREBASE_STORAGE_BUCKET=あなたのstorageBucket
   VITE_FIREBASE_MESSAGING_SENDER_ID=あなたのmessagingSenderId
   VITE_FIREBASE_APP_ID=あなたのappId
   
   VITE_API_BASE_URL=http://localhost:8080
   ```

6. 開発サーバーを起動:
   ```bash
   npm run dev
   # または
   yarn dev
   ```
   フロントエンドは`http://localhost:5173`で実行されます。

## 開発ガイド

### フロントエンド開発

- **コンポーネントの追加**:
  1. `front/src/components/`に新しいコンポーネントファイルを作成
  2. 必要なJSXとロジックを実装
  3. 他のコンポーネントやページからインポートして使用

- **ページの追加**:
  1. `front/src/pages/`に新しいページファイルを作成
  2. App.jsxにルートを追加

- **サービスの追加**:
  1. `front/src/services/`または`front/src/js/services/`に新しいサービスファイルを作成
  2. APIとの通信ロジックを実装

- **スタイルの追加**:
  1. `front/src/css/`にスタイルを追加
  2. SCSSを使用する場合は`main.scss`に追加

## 使用方法

1. アプリケーションにアクセス: `http://localhost:5173`
2. ログインまたは新規ユーザー登録
3. ホームページでアプリケーションの機能を利用
4. プロフィールページでユーザー情報を管理
5. 認証テストページで認証状態とトークンを確認可能

## プロジェクト構造

```
プロジェクトルート/
├── front/                    # フロントエンドアプリケーション
│   ├── src/
│   │   ├── components/       # 再利用可能なコンポーネント
│   │   │   └── NavBar.jsx
│   │   ├── contexts/         # Reactコンテキスト
│   │   │   └── AuthContext.jsx
│   │   ├── css/              # スタイルシート
│   │   │   ├── main.scss     # メインSCSSファイル
│   │   │   └── style.css     # カスタムスタイル
│   │   ├── js/               # JavaScriptファイル
│   │   │   ├── services/     # APIサービス
│   │   │   │   ├── auth-api-service.js
│   │   │   │   ├── firebase.js
│   │   │   │   └── profile-api-service.js
│   │   │   ├── utils/        # ユーティリティ関数
│   │   │   │   └── auth-test.js
│   │   │   ├── bootstrap.js  # Bootstrap初期化
│   │   │   └── main.js       # メインJavaScriptファイル
│   │   ├── pages/            # ページコンポーネント
│   │   │   ├── AboutPage.jsx
│   │   │   ├── AuthTestPage.jsx
│   │   │   ├── ContactPage.jsx
│   │   │   ├── HomePage.jsx
│   │   │   ├── LoginPage.jsx
│   │   │   ├── ProfilePage.jsx
│   │   │   └── RegisterPage.jsx
│   │   ├── services/         # サービス
│   │   │   └── api.js
│   │   ├── App.jsx           # メインReactコンポーネント
│   │   └── main.jsx          # Reactエントリーポイント
│   ├── public/               # 静的ファイル
│   │   └── _redirects        # Netlify用リダイレクト設定
│   ├── etc/                  # その他の設定ファイル
│   ├── index.html            # メインHTMLファイル
│   ├── package.json          # npm依存関係
│   ├── package-lock.json     # npm依存関係ロック
│   ├── vite.config.js        # Vite設定
│   └── .env.example          # 環境変数のサンプル
│
└── LICENSE                   # ライセンスファイル
```

## トラブルシューティング

### Firebase認証エラー

- **auth/configuration-not-found エラー**:
  1. `.env`ファイルが正しく設定されているか確認
  2. Firebase Consoleで認証機能が有効になっているか確認
  3. ブラウザのキャッシュとCookieをクリア
  4. 開発サーバーを再起動

- **トークン検証エラー**:
  1. バックエンドとフロントエンドのFirebase設定が同じプロジェクトを指しているか確認
  2. Firebase Admin SDKの秘密鍵が正しく設定されているか確認

### API接続エラー

- **CORS エラー**:
  1. バックエンドの`CORS_ORIGIN`設定がフロントエンドのURLと一致しているか確認
  2. フロントエンドの`VITE_API_BASE_URL`がバックエンドのURLと一致しているか確認

## ライセンス

このプロジェクトはMITライセンスの下で公開されています。詳細は[LICENSE](LICENSE)ファイルを参照してください。
