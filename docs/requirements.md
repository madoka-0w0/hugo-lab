# 研究室ホームページ 要件定義

作成日：2026-02-18

## 基本情報

- 大学・学部・学科：サンプル大学 理学部 物理学科
- 研究室名：まど研究室（まど教授）
- 研究分野：素粒子実験
- 種別：新規構築
- 公開目標時期：未定

## コンテンツ要件

### 必須コンテンツ
- [x] 研究内容（Research）：サブテーマ2つ。図・写真は仮置き（後日差し替え）
- [x] メンバー一覧（Members）：現在1名（教員）。教員は写真掲載、学生は写真なし
- [x] 論文・研究成果（Publications）：論文5本。DOIリンク付き
- [x] ニュース・お知らせ（News）：更新担当者＝教員自身。更新頻度：随時（月1回程度）
- [x] アクセス・連絡先（Access/Contact）：建物名・部屋番号・メールアドレス・電話番号すべて掲載

### 推奨コンテンツ
- [x] 英語版：設置する。まずTop・Research・Membersの3ページから開始し、余裕があれば拡充
- [x] リンク集：設置する
- [ ] 学生向け情報：設置しない
- [x] ギャラリー：設置する

### 任意コンテンツ
- [x] 実験設備紹介（Facilities）：設置する

## 技術スタック

- プラットフォーム：Hugo（静的サイトジェネレータ）
- 理由：Git管理での運用を希望。Web技術に詳しいメンバーがいる。ある程度のデザインカスタマイズが可能なテーマを選定する

### 必須技術要件
- [x] HTTPS（SSL）対応
- [x] 文字コード UTF-8
- [x] OGP設定
- [x] レスポンシブデザイン
- [x] 基本的なSEO設定（titleタグ・meta description）

## 運用方針

- 更新担当者：教員自身
- 更新頻度目標：月1回以上（News中心）
- ドメイン方式：独自ドメイン（実装中は localhost / GitHub Pages デフォルトURLで進める）
- 言語対応：日英バイリンガル（最低限 Top・Research・Members。余裕があれば拡充）
- アクセス解析：Google Analytics GA4 導入

---

## A. サイトマップ・ナビゲーション

### メニュー構成（上部固定ヘッダー）

```
Home / Research / Members / Publications / News / Facilities / Gallery / Links / Access [EN]
```

### URL スラッグ設計

| ページ | URL（日本語） | URL（英語） |
|---|---|---|
| トップ | / | /en/ |
| Research 一覧 | /research/ | /en/research/ |
| Research サブテーマ1 | /research/theme-01/ | /en/research/theme-01/ |
| Research サブテーマ2 | /research/theme-02/ | /en/research/theme-02/ |
| Members | /members/ | /en/members/ |
| Publications | /publications/ | — |
| News 一覧 | /news/ | — |
| News 個別 | /news/YYYY-MM-DD-slug/ | — |
| Facilities | /facilities/ | — |
| Gallery | /gallery/ | — |
| Links | /links/ | — |
| Access | /access/ | /en/access/ |

英語版スコープ（フェーズ1）：Top・Research（一覧＋サブテーマ各1）・Members・Access

---

## B. トップページ構成

| 順序 | セクション | 内容 |
|:---:|---|---|
| 1 | Hero | 大型画像1枚 + 研究室名オーバーレイ + キャッチコピー（日英） |
| 2 | About | 研究室紹介文 3〜5文（仮テキスト：素粒子実験の意義を端的に説明） |
| 3 | Latest News | 直近5件 + 「ニュース一覧」リンク |
| 4 | Research Topics | サブテーマ2枚のカード（仮画像 + タイトル + 説明2〜3行） |
| 5 | Footer | 研究室名・住所・メール・Copyright・大学リンク |

---

## C. ページ別コンテンツ仕様

### Research

- 一覧ページ（/research/）：2つのサブテーマをカード型表示
- 詳細ページ（各1ページ）：タイトル / 概要文 / 図（プレースホルダー） / 詳細説明
- サブテーマ名：仮名で進める（「研究テーマ1」「研究テーマ2」、後日差し替え）
- 英語版：/en/research/ と各サブテーマページを作成

### Members

- 教員（1名）：氏名・役職・写真・メール・自己紹介文（任意）
- 学生：氏名・学年のみ（写真なし）
- 英語版あり

### Publications

- 年度別降順、著者名 / タイトル / 雑誌 / DOIリンク の形式
- Hugo の `data/publications.yaml` で管理（テンプレート描画）
- 英語版不要（論文はすでに英語）

### News

- 時系列一覧 + 個別記事ページ
- `content/news/YYYY-MM-DD-slug.md` で管理
- Front Matter：date / title / tags（受賞・論文掲載・学会発表・メンバー・イベント・メディア）
- 英語版不要

### Facilities

- 設備名 / 写真（任意） / スペック概要 / 用途 のカード型
- 初期は仮テキスト（後日実データ差し替え）

### Gallery

- サムネイルグリッド（2〜4列）
- Lightbox（GLightbox または fslightbox.js）
- `static/images/gallery/` に画像配置 → テンプレートで自動列挙

### Links

- `data/links.yaml` で管理（カテゴリ分け：所属機関・参加実験・関連施設・学会・ツール）

### Access/Contact

- 組織名・建物名・部屋番号・住所・メール・電話・Google Maps 埋め込み
- 英語版あり（/en/access/）

---

## D. Hugo 実装仕様

### ディレクトリ構成

```
hugo-lab/
├── config/_default/
│   ├── config.toml          # baseURL・title・theme
│   ├── languages.toml       # 日英設定（ja=デフォルト、en=/en/）
│   └── params.toml          # ga4_id 等の共通パラメータ
├── content/                 # 日本語コンテンツ
├── content.en/              # 英語コンテンツ（contentDir 分離方式）
├── data/
│   ├── publications.yaml
│   └── links.yaml
├── layouts/
│   ├── _default/baseof.html
│   ├── partials/
│   │   ├── header.html / footer.html / nav.html
│   │   ├── hero.html
│   │   └── analytics.html   # GA4（本番環境のみ有効）
│   └── shortcodes/
├── static/
│   ├── images/（hero/ members/ research/ gallery/ facilities/）
│   ├── css/custom.css
│   └── favicon.ico
├── themes/[選定テーマ]/
└── i18n/
    ├── ja.yaml
    └── en.yaml
```

### テーマ

- **採用：Congo**（Tailwind CSS・多言語○・カードUI○・MIT License）
- GitHub Actions でビルド時に `hugo mod get` または themes/ にサブモジュールとして追加

### 多言語設定

- `defaultContentLanguage = "ja"`（/ でアクセス）
- 英語は /en/ prefix
- contentDir 分離方式（content/ が ja、content.en/ が en）
- UIラベルは i18n/ja.yaml・i18n/en.yaml で管理

### Google Analytics GA4

- `layouts/partials/analytics.html` に gtag.js を記述
- `{{ if eq hugo.Environment "production" }}` で本番環境のみ有効化
- Measurement ID は `params.toml` の `ga4_id` で管理

### 必須技術設定

- `enableRobotsTXT = true`（sitemap.xml も自動生成）
- meta description：Front Matter の `description` フィールド、未設定時は `.Summary`
- OGP 画像：`static/images/ogp.png`（1200×630px）

### デザイン方針

- スタイル：ビジュアル重視・モダン（大型ヒーロー画像 + カードUI）
- カラー：白ベース + サイエンスブルー（`#0055A4` 系）アクセント1色
- 日本語フォント：Noto Sans JP（Google Fonts）
- 欧文フォント：Inter（Google Fonts）
- カスタムCSS：Congo の `params.toml` で `colorScheme` を調整 + `static/css/custom.css` でピンポイント上書き（テーマファイル直接編集は不可）
- Congo の `colorScheme = "custom"` で Tailwind の primary color を `#0055A4` に設定

---

## E. 開発ワークフロー

### Git ブランチ戦略

- `main`：本番（push で GitHub Actions が自動ビルド → gh-pages ブランチにデプロイ）
- `develop`：開発統合

### GitHub Actions 設定ポイント

- トリガー：`push to main`
- ビルドコマンド：`hugo --minify`
- デプロイ先：`gh-pages` ブランチ（GitHub Pages の source に設定）
- Hugo バージョン：`.github/workflows/deploy.yml` で extended 版を指定

### コンテンツ更新フロー（教員による運用）

```
hugo new news/YYYY-MM-DD-title.md
# エディタで記入
hugo server --disableFastRender  # ローカル確認
git add / commit / push
→ GitHub Actions が自動ビルド（hugo --minify）・デプロイ（約1〜2分）
```

### ドメイン設定（独自ドメイン取得後）

- GitHub Pages の Custom domain 欄に独自ドメインを設定
- `static/CNAME` ファイルに独自ドメインを記述
- DNS レジストラで CNAME レコードを `<username>.github.io` に向ける

### 仮コンテンツ方針

| コンテンツ | 方針 |
|---|---|
| ヒーロー画像 | CC0画像（物理実験系）を使用。後日差し替え |
| Research 図 | placehold.co または単色PNG。後日差し替え |
| 教員写真 | 提供前は placehold.co |
| 本文テキスト | Lorem ipsum を使わず素粒子実験に即した意味のある日本語ダミー文 |
| 論文データ | 実データを記入 |
| News | サイトオープン告知を1件作成 |

---

## F. 実装フェーズ計画

| フェーズ | 内容 |
|:---:|---|
| 1（骨格） | Hugoプロジェクト初期化・テーマ選定・多言語設定・デプロイ設定 |
| 2（コア） | Research / Members / Publications / Access（実データ） |
| 3（運用系） | News + GitHub Actions 自動デプロイ |
| 4（補助系） | Facilities / Gallery / Links |
| 5（英語版） | Top / Research / Members の英語版 |
| 6（仕上げ） | OGP / SEO / GA4 確認・独自ドメイン設定 |
