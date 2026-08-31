# shikakuLog 公式サイト

資格管理アプリ **shikakuLog** のランディングページ。ブラウザ検索からApp Storeへの導線を担う。

公開URL: https://ogilab-apps.github.io/shikakulog/

> サポート・プライバシーポリシー・利用規約は別リポジトリ
> ([shikakulog-support](https://github.com/ogilab-apps/shikakulog-support))。
> このサイトはフッターからそちらへリンクしている。

## 構成

```
index.html      1ファイル完結(CSS・JSともにインライン)
robots.txt      sitemap.xml の場所を宣言
sitemap.xml     更新時は lastmod を直す
.nojekyll       GitHub Pages の Jekyll 処理を止める
assets/
  02-list.jpg 〜 06-widget.jpg   機能ツアーの実機スクショ(表示幅の2倍で書き出し)
  og.jpg                        SNS共有用 1200×630
  icon-32.png / icon-180.png    ファビコン / iOSホーム画面
```

ビルド工程は無い。`index.html` を直接編集して push すれば数分で反映される。

## 設計上の決めごと

- **ヒーローに画像を使わない。** アプリのカードUIとヒートマップをHTML/CSSで描き起こしている。
  拡大しても劣化せず、最大要素がテキストになるため表示も速い。
- **日本語Webフォントを読み込まない。** 数MBあり表示速度を落とすため、本文は端末のフォントに任せる。
  見出しのラテン文字だけ Quicksand(ブランドフォント)を Google Fonts から読む。
- **配色はアプリのデザイントークンに揃える。** primary `#2f6f63`、カード地 `#f2f5f4` ほか。
  差し色はロゴのチェックリスト3色(緑・琥珀・青)。
- ライト/ダークはトークンで3状態(OS設定・明示的な light・明示的な dark)を定義している。

## 更新するとき

### スクリーンショットを差し替える

アプリ側リポジトリの `docs/screenshots/images/<バージョン>/` にある実機スクショを、
**表示幅の2倍(横600px)**の JPEG へ縮小して `assets/` に置く。ファイル名は据え置き。

現在のスクショは **v1.1.0 世代**。以下は未反映なので、撮り直したら差し替える。

- 資格カードのレイアウト変更(v1.1.1)
- 学習ヒートマップ(v1.2.0)
- 資格ごとの通知設定(v1.3.0)

### 文言を変える

`index.html` を直接編集する。FAQ を増減したときは、**末尾の `FAQPage` 構造化データも同じ内容に揃える**こと。
食い違うとGoogleに無視されるか、最悪スパム判定される。

### 料金や機能を変える

アプリ側の [store-listing.md](https://github.com/r-ogiwara-dev/shikakuLog/blob/main/docs/store-listing.md)
が説明文の正本。こちらと矛盾しないようにする。

## SEO

- `title` / `description` / `canonical` / OGP / Twitter Card を設定済み
- 構造化データは `SoftwareApplication` と `FAQPage` の2つ
- **評価(星)の構造化データは入れていない。** 実在しないレビュー評価を書くとスパムポリシー違反になる
- 公開後は **Google Search Console にサイトを登録し `sitemap.xml` を送信**する

「資格管理」のような競合の多い語は、このページ単体では上位に入らない。
記事コンテンツやSNSからの流入と組み合わせる前提。
