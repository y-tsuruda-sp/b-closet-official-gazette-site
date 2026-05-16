# 電子公告サイト（official-gazette.yo-sya.com）

株式会社〇〇の電子公告を公開するサイトです。  
Cloudflare Pages + GitHub によるホスティングで、GitHubにプッシュするだけで自動反映されます。

---

## サイト構成

```
official-gazette-site/
├── index.html         # トップページ（公告一覧）
├── style.css          # スタイルシート
├── README.md          # この説明ファイル
└── pdfs/
    ├── index.json     # 公告ファイル管理用JSON
    ├── .gitkeep       # フォルダ保持用
    └── *.pdf          # 公告PDFファイル（各自追加）
```

---

## 新しい電子公告PDFを公開する手順

### 1. PDFファイルを `pdfs/` フォルダに追加

```
pdfs/2025_kessan.pdf   ← このように配置する
```

### 2. `pdfs/index.json` に1行追記

```json
[
  {
    "title": "決算公告",
    "filename": "2024_kessan.pdf",
    "date": "2024-03-31"
  },
  {
    "title": "決算公告",
    "filename": "2025_kessan.pdf",
    "date": "2025-03-31"
  }
]
```

`title`・`filename`・`date` の3項目を必ず記入してください。

| 項目 | 内容 |
|------|------|
| `title` | 公告の種類（例：決算公告、合併公告） |
| `filename` | PDFのファイル名（拡張子込み） |
| `date` | 公開日（YYYY-MM-DD形式） |

### 3. GitHubにコミット・プッシュ

```bash
git add pdfs/2025_kessan.pdf pdfs/index.json
git commit -m "Add 2025年決算公告"
git push
```

### 4. 数分後に自動反映を確認

https://official-gazette.yo-sya.com にアクセスして一覧に表示されることを確認してください。

---

## 初期セットアップ（初回のみ）

### GitHub → Cloudflare Pages 連携

1. [Cloudflare Dashboard](https://dash.cloudflare.com) にログイン
2. 「Pages」→「プロジェクトを作成」→「Gitに接続」
3. このリポジトリ `official-gazette-site` を選択
4. ビルド設定は**空欄のまま**（静的HTMLのためビルド不要）
5. 「保存してデプロイ」→ `official-gazette-site.pages.dev` で確認

### カスタムドメイン設定

1. Cloudflare Pages プロジェクト →「カスタムドメイン」タブ
2. `official-gazette.yo-sya.com` を入力して設定
3. CloudflareのDNSにCNAMEレコードが自動追加される
4. 数分〜数時間後に https://official-gazette.yo-sya.com でアクセス可能になる

---

## 注意事項

- **電子公告は会社法上の法的効力を持つため、公告の掲載期間中はPDFファイルを削除しないこと**
- HTTPS（SSL）はCloudflare Pagesが自動で対応するため、追加設定は不要
- `yo-sya.com`（コーポレートサイト）は別リポジトリ・別プロジェクトとして構築すること

---

## URL構成

| URL | 用途 |
|-----|------|
| `https://official-gazette.yo-sya.com` | 電子公告サイト（本リポジトリ） |
| `https://yo-sya.com` | コーポレートサイト（別途作成予定） |
