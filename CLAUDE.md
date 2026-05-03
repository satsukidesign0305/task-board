# CLAUDE.md

このファイルはClaude Codeがこのリポジトリで作業する際のガイダンスを定義します。

## プロジェクト概要

タスクボードアプリケーション。タスクの追加・完了切り替え・削除ができ、localStorageで永続化している。

## デプロイ先

https://satsukidesign0305.github.io/task-board/

mainブランチへのプッシュで GitHub Actions が自動ビルド・デプロイする。

## 技術スタック

| 項目 | 内容 |
|------|------|
| フレームワーク | React 19 |
| ビルドツール | Vite 6 |
| 言語 | JavaScript (JSX) |
| スタイリング | CSS（`src/index.css` 1ファイルで管理） |
| 永続化 | localStorage |
| CI/CD | GitHub Actions (`.github/workflows/deploy.yml`) |

## コンポーネント構成と命名規約

```
src/
  App.jsx                  # ルートコンポーネント。state管理とハンドラを集約
  components/
    TaskInput.jsx          # タスク入力フォーム
    TaskList.jsx           # タスク一覧（ TaskItem のリストを描画）
    TaskItem.jsx           # 個別タスク（チェックボックス・削除ボタン）
  index.css                # グローバルスタイル
  main.jsx                 # エントリーポイント
```

### 命名規約

- **コンポーネントファイル**: PascalCase（例: `TaskItem.jsx`）
- **コンポーネント関数**: PascalCase のデフォルトエクスポート（例: `export default function TaskItem`）
- **propsのハンドラ**: `on` プレフィックス（例: `onAdd`, `onToggle`, `onDelete`）
- **CSSクラス名**: kebab-case（例: `.task-item`, `.delete-btn`）
- **localStorageキー**: kebab-case（例: `task-board-tasks`）

## Git運用ルール

**コードを変更するたびに、必ずGitHubへプッシュすること。**

具体的な手順:

1. 変更をステージング: `git add <変更ファイル>`
2. コミット: `git commit -m "変更内容を簡潔に説明するメッセージ"`
3. プッシュ: `git push origin <ブランチ名>`

### コミットメッセージの書き方

- 変更の「何を」「なぜ」を簡潔に記述する
- 日本語・英語どちらでも可
- 例: `fix: ログインボタンのスタイル修正`, `feat: タスク追加機能の実装`

### ブランチ戦略

- `main`: 本番相当のコード
- 機能追加・バグ修正は原則 `main` に直接プッシュ（小規模プロジェクトのため）
- 大きな変更の場合はフィーチャーブランチを切ること

### 注意事項

- `.env` など機密情報を含むファイルはコミットしない
- `node_modules/` はコミットしない（`.gitignore` で除外済みであること）
- プッシュ前にビルド・テストが通ることを確認する

## 開発ガイドライン

- コメントは原則書かない。必要な場合は「なぜそうしているか」だけを1行で記述する
- 不要な抽象化・過剰な設計はしない
- セキュリティ上の脆弱性（XSS、SQLインジェクション等）を導入しない
