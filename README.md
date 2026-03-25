# みずやり手帳 — Vercel デプロイ手順

## ファイル構成

```
mizuyari/
├── api/
│   └── claude.js        ← AnthropicへのプロキシAPI（APIキーはここで使う）
├── public/
│   └── index.html       ← アプリ本体
├── vercel.json          ← Vercel設定
└── README.md
```

---

## デプロイ手順（30分程度）

### Step 1: GitHubにアップロード

1. https://github.com にアクセスしてアカウント作成（または既存アカウントでログイン）
2. 右上の「+」→「New repository」をクリック
3. Repository name に `mizuyari` と入力 → 「Create repository」
4. 「uploading an existing file」をクリック
5. このフォルダの中身（api・public・vercel.json）を全部ドラッグ＆ドロップ
6. 「Commit changes」をクリック

---

### Step 2: Vercelにデプロイ

1. https://vercel.com にアクセスしてアカウント作成（GitHubアカウントでログイン推奨）
2. 「Add New Project」をクリック
3. GitHubと連携して `mizuyari` リポジトリを選択
4. 「Deploy」をクリック（設定変更は不要）
5. デプロイ完了！ `mizuyari-xxx.vercel.app` のようなURLが発行される

---

### Step 3: APIキーを設定

1. Vercelのダッシュボードでプロジェクトを開く
2. 上部メニュー「Settings」→ 左メニュー「Environment Variables」
3. 以下を入力して「Save」:
   - **Name**: `ANTHROPIC_API_KEY`
   - **Value**: AnthropicのAPIキー（https://console.anthropic.com/settings/keys で取得）
4. 左メニュー「Deployments」から最新のデプロイを開き、右上「...」→「Redeploy」

---

### Step 4: 動作確認

発行されたURL（例: `https://mizuyari-abc123.vercel.app`）をブラウザで開く。
植物を追加してAI機能が動作すれば完了。

---

## APIキーの取得方法

1. https://console.anthropic.com にアクセス
2. 「API Keys」→「Create Key」
3. 名前を入力（例: mizuyari）してキーをコピー
4. ※キーは一度しか表示されないので必ず保存すること

---

## コスト目安

| 機能 | 1回あたりの費用目安 |
|------|-------------------|
| 写真から植物名認識 | 約0.5〜1円 |
| 植物プロフィール表示 | 約0.3〜0.5円 |
| 水やり評価 | 約0.1〜0.2円 |
| AI状態診断 | 約0.2〜0.3円 |

月100人が毎日使った場合、推定 月2,000〜5,000円程度。

---

## カスタムドメインを設定したい場合

1. Vercelダッシュボード →「Domains」
2. 取得済みドメインを入力して「Add」
3. DNSレコードをVercelの指示通りに設定

---

## 問題が起きたとき

- AI機能が動かない → Vercelの「Environment Variables」でAPIキーが正しく設定されているか確認
- 「502 Bad Gateway」が出る → Vercelの「Functions」タブでエラーログを確認
