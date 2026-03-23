# コンテンツ作成ガイド

研究室ホームページにコンテンツを追加・更新する際の手引きです。

---

## 論文情報を追加する

`data/publications.yaml` に追記します。**新しいものを先頭に**追加してください。

```yaml
- year: 2026
  authors: "T. Yamada, K. Suzuki et al. (SAMPLE-EXP Collaboration)"
  title: "論文タイトル [架空データ]"
  journal: "Physical Review Letters"
  volume: "136"
  pages: "012345"
  doi: "10.0000/PhysRevLett.136.012345"
```

**記入ルール:**
- `doi` は `10.0000/` から始まる架空の DOI を使用（実在するDOIは記載しない）
- `title` の末尾には `[架空データ]` を付ける
- 実験名は `SAMPLE-EXP`、検出器名は `SAMPLE-DET` を使用

---

## ギャラリー画像を追加する

`data/gallery.yaml` に追記します。

```yaml
- src: "https://placehold.co/600x400/0055A4/ffffff?text=説明+[架空]"
  caption: "写真の説明 [架空データ]"
  category: "lab"   # lab / conf / exp のいずれか
```

| category | 用途 |
|----------|------|
| `lab` | 研究室・ゼミの様子 |
| `conf` | 学会・イベント |
| `exp` | 実験装置・施設 |

実際の画像を使う場合は `static/images/gallery/` に配置し、`src` を `/images/gallery/ファイル名.jpg` と記述します。

---

## 研究テーマを更新する

`content/research/theme-XX/_index.md` を編集します。

英語版は `content.en/research/theme-XX/_index.md` を個別に編集してください。

---

## コンテンツのルール

- **架空データ必須**: 実在する人物・論文・組織の情報は掲載しない
- **[架空データ] マーカー**: 論文タイトル・ニュース記事タイトルの末尾に付ける
- **実験名**: `SAMPLE-EXP`（検出器: `SAMPLE-DET`）を使用
- **人名**: 山田・鈴木・田中などの一般的な架空氏名を使用
- **DOI**: `10.0000/` プレフィックスを使用（未割り当て）
