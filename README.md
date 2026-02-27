# agent-article-kit

AI コーディングエージェント（Claude Code / Codex CLI）を使った日本語の記事作成ツールキットです。採用広報・社内広報記事の作成、インタビュー、レビューを対話形式で実行できます。

## 特徴

- `/write-article` - 書きたいこと（テーマや断片メモ）から対話で素材を深掘りし、記事を自動生成
- `/interview` - エンジニアへの対話型インタビューを実施し、採用広報記事を自動生成
- `/review-article` - 記事ドラフトを構成・文章・訴求力の観点でレビューし、改善案を提示
- 日本語の技術文章向け textlint 設定を同梱

## セットアップ

```bash
git clone https://github.com/langcore-dev/agent-article-kit.git
cd agent-article-kit
npm install
```

## 使い方

### 前提

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) がインストールされていること

### 記事を書く

このリポジトリのディレクトリで Claude Code を起動し、スラッシュコマンドを実行します。

**書きたいことから記事を作る:**

```
/write-article
```

テーマや断片的なメモを入力すると、6つの観点（具体性・エピソード・背景/動機・成果/変化・感情/実感・メッセージ性）で対話的に素材を深掘りし、記事ドラフトを生成します。

**インタビューから記事を作る:**

```
/interview
```

対象者の情報を入力すると、5つのカテゴリ（技術/プロダクト・チーム/文化・キャリア/成長・日常/働き方・未来/ビジョン）から質問を動的に生成し、インタビューを進行します。

### 記事をレビューする

```
/review-article
```

`articles/` ディレクトリ内の記事を、構成・文章ルール・視点の一貫性・具体性・訴求力・textlint の6次元でレビューします。

### textlint を手動で実行する

```bash
npm run lint          # チェック
npm run lint:fix      # 自動修正
```

## textlint 設定

日本語の技術文章向けに以下のルールを設定しています。

| ルール | 説明 |
|---|---|
| `preset-ja-technical-writing` | 日本語の技術文章プリセット（一文100文字以内など） |
| `no-doubled-joshi` | 助詞の連続使用を検出 |
| `ja-no-redundant-expression` | 冗長な表現を検出（「することができる」→「できる」） |
| `ja-unnatural-alphabet` | 不自然なアルファベット使用を検出 |

## 記事の管理

生成された記事は `articles/` ディレクトリに `YYYY-MM-DD-{slug}.md` の形式で出力されます。

## カスタマイズ

### テンプレートの変更

- 書きたいことドリブン記事: `.claude/skills/write-article/article-template.md`
- インタビュー記事: `.claude/skills/interview/article-template.md`

### 深掘り対話の調整

- 書きたいことドリブン: `.claude/skills/write-article/writing-guide.md`
- インタビュー: `.claude/skills/interview/interview-guide.md`

### レビュー観点の変更

- `.claude/skills/review-article/review-checklist.md`

### textlint ルールの変更

- `.textlintrc.json` を編集してください

## ディレクトリ構成

```
.claude/
├── agents/          # 記事生成サブエージェント
├── commands/        # スラッシュコマンド定義
└── skills/          # スキル（ワークフロー・テンプレート・ガイド）
articles/            # 記事の出力先
.textlintrc.json     # textlint 設定
package.json         # 依存パッケージ
```

## ライセンス

MIT
