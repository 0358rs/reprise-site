# reprise-site

Reprise（リプライズ）の紹介ページ・プライバシーポリシー・サポート。GitHub Pages（Jekyll）で公開する。

| パス | ファイル | 内容 |
|---|---|---|
| `/` | `index.html` | 紹介ページ（日本語） |
| `/en/` | `en/index.html` | 紹介ページ（英語） |
| `/privacy` | `privacy.md` | プライバシーポリシー（日本語・英語を 1 ページに併記） |
| `/support` | `support.md` | サポート（日本語・英語を 1 ページに併記） |

- 共通部品は `_includes/`（head・ヘッダー・フッター・図解）、見た目は `assets/site.css`
- ナビゲーションの文言は `_data/i18n.yml`
- 紹介ページの図解の波形は `_includes/wave-*.html`（生成した SVG）

## 設定（`_config.yml`）

| キー | 内容 |
|---|---|
| `app_store_url` | App Store の商品ページ。空のあいだはダウンロードボタンを出さない |
| `twitter_username` | X のアカウント（@ を除く）。空のあいだはリンクを出さない |
| `url` / `baseurl` | 公開先。独自ドメインにするときは下を参照 |

## 手元で確かめる

```
gem install github-pages
jekyll serve
```

## 独自ドメインへの切り替え

1. ドメインを取得し、DNS に GitHub Pages を向ける
   - 頂点ドメイン（例 `reprise.app`）: A レコード `185.199.108.153` `185.199.109.153` `185.199.110.153` `185.199.111.153`
   - `www` などのサブドメイン: CNAME レコード → `0358rs.github.io`
2. リポジトリの Settings → Pages → Custom domain にドメインを入れ、「Enforce HTTPS」をオンにする
   （ルートに `CNAME` ファイルが作られる）
3. `_config.yml` の `url` をそのドメインに、`baseurl` を `""` にする
4. App Store Connect の URL を書き換える
   - App のプライバシー → プライバシーポリシー URL: `https://<ドメイン>/privacy`
   - バージョン情報 → サポート URL: `https://<ドメイン>/support`、マーケティング URL: `https://<ドメイン>/`
5. アプリのリポジトリ（`0358rs/shadowplayer`）の `docs/app-store-connect-instructions.md` の URL も同じに直す

切り替え後も `https://0358rs.github.io/reprise-site/…` へのアクセスは、GitHub Pages が同じパスの新しいドメインへ転送する。

⚠️ 以前はトップ（`/`）がプライバシーポリシーだった。App Store Connect のプライバシーポリシー URL が
トップのままだと紹介ページが開くので、手順 4 で必ず `/privacy` に直す。
