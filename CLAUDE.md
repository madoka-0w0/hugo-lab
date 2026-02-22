# CLAUDE.md

## プロジェクト概要

○○大学 理学部物理学科 ○○研究室のホームページ。

- **研究分野**: （例：物性物理学・超伝導）
- **対象読者**: 研究者・学生・メディア・一般

## 技術スタック

- プラットフォーム：Hugo（extended 版）
- テーマ：Congo（Tailwind CSS ベース・MIT License）
- 多言語：Hugo multilingual mode（contentDir 分離方式）
- デプロイ：GitHub Pages（GitHub Actions で自動ビルド）
- アクセス解析：Google Analytics GA4

## スキル

研究室ホームページのコンテンツ・レイアウト設計は、必ず以下のスキルファイルを参照すること：

- `.claude/skills/lab-homepage/SKILL.md` — コンテンツ設計・レイアウト・実装技術のベストプラクティス
- `.claude/skills/lab-homepage/references/` — 国内主要国立大学30以上の調査データ

### スキル参照タイミング

- ページ構成・ナビゲーション設計の判断時
- 各セクション（Research / Members / Publications / News 等）のレイアウト設計時
- 技術スタック選定時

## 開発ワークフロー

**作業開始前:**
`git pull origin main` で main を最新化してからブランチを切ること（ユーザーへの確認不要）。

**作業完了後:**（ユーザーへの確認不要）

1. `git add` → `git commit` → `git push origin <branch>`
2. `gh pr create --head <branch> --base main` で PR を作成
3. PR URL をユーザーに報告して完了

- 各タスクは専用ブランチ（例: `feat/phase2-research`）で作業する
- worktree を使う場合は `../lab_homepage_tmp/lab-<task-id>/` に作成する
- worktree 内でサブモジュール未初期化の場合は `git submodule update --init --recursive` を実行する

## コンテンツ・データの原則

**サイト内のすべてのコンテンツ・データは架空のものを使用すること。**

- 論文（`data/publications.yaml`）：架空の著者名・タイトル・雑誌・DOI を使用する。DOI は `10.9999/` など実在しないプレフィックスを使う
- メンバー（`data/members.yaml`）：実在しない人名・メールアドレスを使用する
- ニュース（`content/news/`）：実在しないイベント・受賞・発表内容を記述する
- 研究テーマ（`content/research/`）：素粒子実験の文脈に即した架空の内容にする
- 施設・設備（Facilities）、リンク（Links）、アクセス（Access）なども同様
- 画像のプレースホルダーURL（placehold.co 等）は使用可
- **実在する論文・人物・組織・URLを誤ってコンテンツに埋め込まないこと**

## コーディング規約

- Hugo ディレクトリ構成：config/ content/ content.en/ data/ layouts/ static/ i18n/ themes/
- テーマファイルは直接編集しない。カスタムCSSは `assets/css/custom.css` に記述（`static/css/` ではない）
- 論文・リンクデータは `data/*.yaml` で管理しテンプレートで描画
- OGP・robots.txt・sitemap は Hugo 標準機能で自動生成
- GA4 は本番環境（`hugo.Environment == "production"`）でのみ有効化

## 現在のステータス

- **Phase 0**: 完了
- **Phase 1**: 完了（技術スタック・コーディング規約確定・要件定義詳細化）
- **Phase 2**: 未着手（実装待ち）
