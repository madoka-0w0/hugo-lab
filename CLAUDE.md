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

## コーディング規約

- Hugo ディレクトリ構成：config/ content/ content.en/ data/ layouts/ static/ i18n/ themes/
- テーマファイルは直接編集しない。カスタムCSSは `static/css/custom.css` に記述
- 論文・リンクデータは `data/*.yaml` で管理しテンプレートで描画
- OGP・robots.txt・sitemap は Hugo 標準機能で自動生成
- GA4 は本番環境（`hugo.Environment == "production"`）でのみ有効化

## 現在のステータス

- **Phase 0**: 完了
- **Phase 1**: 完了（技術スタック・コーディング規約確定・要件定義詳細化）
- **Phase 2**: 未着手（実装待ち）
