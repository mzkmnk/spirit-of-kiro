# 技術スタック

## ランタイム & ビルドシステム
- **Bun**: メインのJavaScriptランタイム及びパッケージマネージャー
- **Docker/Podman**: コンテナ化された開発・デプロイメント
- **Docker Compose**: マルチサービスオーケストレーション

## フロントエンド (Client)
- **Vue.js 3**: Composition APIを使用したフロントエンドフレームワーク
- **TypeScript**: 型安全なJavaScript開発
- **Vite**: ビルドツール及び開発サーバー
- **Pinia**: 状態管理
- **Vue Router**: クライアントサイドルーティング
- **Vitest**: ユニットテストフレームワーク
- **ESLint + Prettier**: コードリンティング及びフォーマット

## バックエンド (Server)
- **Bun**: WebSocketサーバーランタイム
- **WebSocket (ws)**: リアルタイムクライアント・サーバー通信
- **TypeScript**: サーバーサイド型安全性
- **AWS SDK**: クラウドサービス統合

## インフラストラクチャ & サービス
- **AWS Bedrock**: AIモデル統合 (Nova Pro, Claude Sonnet, Nova Canvas)
- **Amazon Cognito**: ユーザー認証
- **DynamoDB**: ゲーム状態の永続化
- **S3**: アイテム画像ストレージ
- **CloudFront**: コンテンツ配信
- **MemoryDB**: 画像類似性のためのベクターデータベース
- **Redis**: キャッシュレイヤー

## 開発コマンド

### ルートレベル
```bash
# クライアントとサーバーを開発モードで起動
bun dev

# 全パッケージの依存関係をインストール
bun install
```

### クライアント開発
```bash
cd client
bun run dev          # 開発サーバーを起動
bun run build        # プロダクションビルド
bun run test:unit    # ユニットテストを実行
bun run lint         # コードをリント・修正
bun run format       # Prettierでコードをフォーマット
```

### サーバー開発
```bash
cd server
bun --watch server.ts    # ホットリロード付きでサーバーを起動
bun test                 # テストを実行
bun run bootstrap-dynamodb  # ローカルDynamoDBテーブルをセットアップ
```

### Docker開発
```bash
# コンテナでフルスタック起動
docker compose build && docker compose up --watch --remove-orphans --timeout 0 --force-recreate

# コンテナ内でDynamoDBテーブルをブートストラップ
docker exec server bun run /app/bootstrap-local-dynamodb.js
```

## コードスタイル
- 全体でTypeScriptを使用
- Options APIよりもVue Composition APIを優先
- ESLint設定を強制
- 一貫したフォーマットのためのPrettier
- ゲームロジック分離のためのシステムベースアーキテクチャ