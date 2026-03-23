# ○○研究室 ホームページ

サンプル大学 理学部物理学科 素粒子実験研究室の公式サイトです。
Hugo（静的サイトジェネレーター）と Congo テーマで構築されています。

---

## 目次

1. [はじめに（初回セットアップ）](#はじめにセットアップ)
2. [ローカルでプレビューする](#ローカルでプレビューする)
3. [ニュースを投稿する](#ニュースを投稿する)
4. [メンバー情報を更新する](#メンバー情報を更新する)
5. [論文情報を追加する](#論文情報を追加する)
6. [ギャラリーを更新する](#ギャラリーを更新する)
7. [変更を反映する（Git 操作）](#変更を反映するgit-操作)
8. [ページ構成](#ページ構成)

---

## はじめに（セットアップ）

### 必要なソフトウェア

- **Git** — バージョン管理ツール
  → [git-scm.com](https://git-scm.com/) からインストール
- **Hugo Extended** — サイト生成ツール（`extended` 版が必要）
  → [gohugo.io/installation](https://gohugo.io/installation/) を参照
  → Mac の場合: `brew install hugo`（Homebrew が必要）

> **Go（プログラミング言語）は不要です。**
> Hugo は Go で書かれていますが、コンパイル済みのバイナリとして配布されているため、
> Go を別途インストールする必要はありません。

### リポジトリのクローン

```bash
git clone --recurse-submodules https://github.com/madoka-0w0/hugo-lab.git
cd hugo-lab
```

> **注意**: `--recurse-submodules` が必要です（テーマが submodule として管理されているため）。
>
> オプションなしでクローンしてしまった場合は、クローン後に以下を実行してください:
> ```bash
> git submodule update --init --recursive
> ```

---

## ローカルでプレビューする

```bash
hugo server
```

ブラウザで `http://localhost:1313/` を開くと確認できます。
ファイルを保存するたびに自動でリロードされます。

終了するには `Ctrl + C` を押してください。

---

## ニュースを投稿する

### 1. 記事ファイルを作成する

```bash
hugo new news/YYYY-MM-DD-タイトル.md
```

例:
```bash
hugo new news/2026-04-01-award.md
```

`content/news/` に新しいファイルが作成されます。

### 2. ファイルを編集する

作成されたファイルをテキストエディタで開き、内容を記入します:

```markdown
---
title: "○○賞を受賞しました [架空データ]"
date: 2026-04-01
tags: ["受賞"]
description: "記事の概要（検索結果などに使われます）"
---

本文をここに書きます。

**[架空データ — 実在しない内容の場合はこの注記を末尾に]**
```

### 使えるタグ

| タグ | 用途 |
|------|------|
| `お知らせ` | 一般的なお知らせ・サイト更新 |
| `論文掲載` | 論文の掲載・採録通知 |
| `受賞` | 受賞・表彰 |
| `学会発表` | 学会・シンポジウムでの発表 |
| `メンバー` | メンバーの加入・卒業 |

> **⚠️ 新しいタグを追加する場合**: `assets/css/custom.css` の「News タグ」セクションと `archetypes/news.md` のコメントも合わせて更新してください（エンジニアに依頼してください）。

### 3. プレビューして確認する

`hugo server` を起動した状態で `http://localhost:1313/news/` を確認します。
Draft（下書き）のファイルを確認したい場合は:

```bash
hugo server -D
```

---

## メンバー情報を更新する

メンバー情報は `data/members.yaml` で管理しています。

```bash
# ファイルをテキストエディタで開く
open data/members.yaml   # Mac
```

### 教員の項目

```yaml
faculty:
  - name: "山田 太郎"          # 日本語氏名
    name_en: "Taro Yamada"      # 英語氏名
    role: "准教授"
    role_en: "Associate Professor"
    email: "yamada@example.ac.jp"
    bio: "日本語の自己紹介文"
    bio_en: "English biography"
```

### 学生の項目

```yaml
students:
  doctoral:
    - name: "鈴木 一郎"
      grade: "博士課程3年"
  master:
    - name: "田中 二郎"
      grade: "修士課程2年"
  undergraduate:
    - name: "佐藤 三郎"
      grade: "学部4年"
```

---

## 論文情報を追加する

論文データは `data/publications.yaml` で管理しています。**新しいものをファイルの先頭に追加**してください。

```bash
# ファイルをテキストエディタで開く
open data/publications.yaml   # Mac
```

### 追記の形式

```yaml
- year: 2026
  authors: "T. Yamada, K. Suzuki, H. Tanaka et al. (SAMPLE-EXP Collaboration)"
  title: "論文タイトル [架空データ]"
  journal: "Physical Review Letters"
  volume: "136"
  pages: "012345"
  doi: "10.0000/PhysRevLett.136.012345"
```

| 項目 | 内容 |
|------|------|
| `year` | 出版年（数値） |
| `authors` | 著者リスト（"名前, 名前 et al." 形式） |
| `title` | 論文タイトル（末尾に `[架空データ]` を付ける） |
| `journal` | 雑誌名（省略なし） |
| `volume` | 巻号 |
| `pages` | ページ番号 |
| `doi` | DOI（`10.0000/` から始まる形式） |

> **注意**: `doi` を記載すると論文タイトルがリンクになります。省略も可能です（その場合は行ごと削除してください）。

### プレビューで確認する

`http://localhost:1313/publications/` で表示を確認してください。

---

## ギャラリーを更新する

ギャラリーの画像データは `data/gallery.yaml` で管理しています。

```bash
# ファイルをテキストエディタで開く
open data/gallery.yaml   # Mac
```

### 実際の画像を使う場合

1. 画像ファイルを `static/images/gallery/` に配置する
2. `gallery.yaml` に追記する:

```yaml
- src: "/images/gallery/2026-04-lab.jpg"
  caption: "研究室の様子 [架空データ]"
  category: "lab"
```

### プレースホルダー画像を使う場合（仮）

画像が未定の場合は `placehold.co` の URL を使用できます:

```yaml
- src: "https://placehold.co/600x400/0055A4/ffffff?text=説明+[架空]"
  caption: "写真の説明 [架空データ]"
  category: "exp"
```

### カテゴリー

| category | フィルター表示名 | 用途 |
|----------|-----------------|------|
| `lab` | 研究室 | 研究室・ゼミの様子 |
| `conf` | 学会・イベント | 学会・シンポジウム |
| `exp` | 実験装置 | 実験装置・施設の写真 |

### 画像ファイルの推奨サイズ

- 横長（3:2）: 1200×800px 以上
- ファイル形式: JPEG（`.jpg`）または WebP（`.webp`）
- ファイルサイズ: 1枚あたり 500KB 以下を目安に

### プレビューで確認する

`http://localhost:1313/gallery/` でフィルターも含めて動作確認してください。

---

## 変更を反映する（Git 操作）

### 基本的な流れ

```bash
# 1. 最新の状態を取得
git pull origin main

# 2. 変更したファイルをステージング
git add content/news/2026-04-01-award.md
# または変更したファイルを個別に指定

# 3. コミット（変更内容のメモ）
git commit -m "受賞ニュースを追加"

# 4. GitHub にプッシュ
git push origin main
```

### 注意事項

- 複数人で作業する場合は `git pull` を先に行ってください。
- `data/` 以下のファイル（members.yaml・publications.yaml・gallery.yaml）は複数人が同時に編集すると競合が起きやすいため、変更前後に必ず `git pull` してください。

---

## ページ構成

```
content/               ← 日本語コンテンツ
  _index.md            ← トップページ
  news/                ← ニュース記事
  research/            ← 研究テーマ
  members/             ← メンバー（レイアウトは data/ を参照）
  access/              ← アクセス・連絡先
  publications/        ← 論文一覧（レイアウトは data/ を参照）
  gallery/             ← ギャラリー（data/gallery.yaml を参照）

content.en/            ← 英語コンテンツ
  （日本語と同じ構成）

data/
  members.yaml         ← メンバーデータ
  publications.yaml    ← 論文データ
  gallery.yaml         ← ギャラリー画像データ

assets/css/custom.css  ← カスタムスタイル
config/_default/       ← サイト設定
```

---

## よくある質問

**Q. ローカルで確認したら崩れているが本番では正常**
A. Hugo のキャッシュが原因の場合があります。`hugo server --disableFastRender` を試してください。

**Q. 日本語が文字化けする**
A. ファイルの文字コードが `UTF-8` になっているか確認してください。

**Q. 画像を追加したい**
A. `static/images/` フォルダに画像を置き、Markdown 内で `![説明](/images/ファイル名.jpg)` と記述します。

---

## 問い合わせ

技術的な問題はリポジトリの [Issues](https://github.com/madoka-0w0/hugo-lab/issues) にてご連絡ください。
