# プロジェクト構造

## ルートディレクトリ
```
├── client/           # Vue.jsフロントエンドアプリケーション
├── server/           # Bun WebSocketサーバー
├── item-images/      # アイテム画像生成サービス
├── docs/             # プロジェクトドキュメント
├── scripts/          # ビルド・デプロイメントスクリプト
├── docker/           # Dockerボリュームとデータ
├── .kiro/            # Kiro IDE設定とステアリング
├── launch.ts         # 開発ランチャースクリプト
└── docker-compose.yml # マルチサービスオーケストレーション
```

## クライアント構造 (`client/`)
```
├── src/
│   ├── components/   # ゲームオブジェクトとUIのVueコンポーネント
│   ├── views/        # ページレベルのVueコンポーネント
│   ├── stores/       # Pinia状態管理
│   ├── systems/      # ゲームロジックシステム (物理、インベントリなど)
│   ├── utils/        # ユーティリティ関数とヘルパー
│   ├── assets/       # 静的アセット (画像、CSS)
│   └── composables/  # Vue composition関数
├── public/           # 静的パブリックアセット
├── iac/              # デプロイメント用Infrastructure as Code
└── package.json      # フロントエンド依存関係とスクリプト
```

## サーバー構造 (`server/`)
```
├── handlers/         # WebSocketメッセージハンドラー
├── state/            # データ永続化レイヤー (DynamoDB)
├── utils/            # サーバーユーティリティ関数
├── llm/              # AI統合 (Bedrock、プロンプト)
├── mocks/            # テスト用モックデータ
├── iac/              # Infrastructure as Code
├── __tests__/        # テストファイル
└── server.ts         # メインサーバーエントリーポイント
```

## アイテム画像サービス (`item-images/`)
```
├── handlers/         # HTTPリクエストハンドラー
├── lib/              # コア画像生成ロジック
├── state/            # ベクターデータベースとRedis統合
├── scripts/          # ユーティリティスクリプト
├── iac/              # Infrastructure as Code
└── server.ts         # HTTPサーバーエントリーポイント
```

## 主要なアーキテクチャパターン

### クライアントアーキテクチャ
- **コンポーネントベースUI**: 全てのゲーム要素がVueコンポーネント
- **システムベースロジック**: ゲームロジックが独立したシステムに分離
- **イベント駆動通信**: システム間はイベントで通信
- **サーバー駆動状態**: WebSocketイベントが状態変更を駆動

### サーバーアーキテクチャ
- **メッセージハンドラーパターン**: 各WebSocketメッセージタイプに専用ハンドラー
- **状態抽象化**: データベース操作は状態モジュールを通じて抽象化
- **AI統合レイヤー**: LLMインタラクションは`/llm`ディレクトリに集約

### ファイル命名規則
- **kebab-case**: ファイルとディレクトリ名
- **PascalCase**: Vueコンポーネント
- **camelCase**: TypeScript関数と変数
- **SCREAMING_SNAKE_CASE**: 環境変数

### インポート整理
- 外部依存関係を最初に
- 内部モジュールを次に
- 相対インポートを最後に
- 可能な場合は機能別にグループ化

### テスト構造
- テストはソースと同じ場所の`__tests__/`ディレクトリに配置
- テストファイルは`*.test.ts`命名規則に従う
- モックデータは専用の`mocks/`ディレクトリに保存