# SEO 改修レポート

対象: `index.html`（トップ） / `article.html`（記事）

## 目的
- 検索エンジンでの理解促進（タイトル/説明/構造化データ/OG/Twitter）
- 共有時の見栄え改善（OG/Twitter 画像・文言）
- クリック率改善（明確なタイトル/ディスクリプション）
- 表示パフォーマンスと可読性の微改善（画像属性・ナビ強化）

## 変更点サマリ

### 共通（両ページ）
- メタ: `robots`, `author`, `theme-color` を追加
- カノニカル: `link rel="canonical"` を追加（例: `https://example.com/`）
- RSS: `link rel="alternate" type="application/rss+xml"` を追加
- OG/Twitter: タイトル/説明/URL/画像/ロケールを追加
- JSON-LD: トップに `WebSite` と `Organization`、記事に `BlogPosting` と `BreadcrumbList` を追加
- 画像: `decoding="async"` と（必要箇所に）`fetchpriority="high"` を付与、`alt` テキストを具体化

### `index.html`
- `<title>` を「Modern Blog | シンプルで読みやすいブログデザイン」に最適化
- `<meta name="description">` を内容に即した説明に刷新
- ヒーロー画像: `alt` を意味的に更新、`decoding="async"`, `fetchpriority="high"` を追加
- 記事カード 6件: すべてのサムネイル `alt` を記事内容に合わせて具体化、`decoding="async"` を追加
- フッター: （補足）RSS リンクを HTML の `<head>` にも追加済み。フッターの外部リンクに `rel` 付与は任意（次対応候補）。
- JSON-LD: `WebSite` + `Organization` を `</body>` 直前に挿入

### `article.html`
- `<title>` を「読みやすさを高めるUIルール集 | Modern Blog」に最適化
- `<meta name="description">` を本文要約に刷新
- カノニカル: `https://example.com/article.html`
- OG/Twitter: `og:type=article`, 公開/更新日時、画像、URL を追加
- アイキャッチ: `alt` の具体化 + `decoding="async"` + `fetchpriority="high"`
- シェアボタン: 外部リンクに `rel="noopener noreferrer nofollow"` を付与
- JSON-LD: `BlogPosting`（記事情報一式）+ `BreadcrumbList` を `</body>` 直前に挿入

## 構造化データの詳細
- `WebSite`: サイト名・URL・言語・検索アクション（将来のサイト内検索 URL を想定）
- `Organization`: サイト運営主体（名称・URL・ロゴ）
- `BlogPosting`: 見出し、要約、画像、公開日、更新日、著者、発行元、`mainEntityOfPage`
- `BreadcrumbList`: Home → 記事 の 2 階層

## 画像/リンク最適化
- 画像: `loading="lazy"` に加え `decoding="async"` を付与、ヒーロー/アイキャッチは `fetchpriority="high"`
- 代替テキスト: すべての記事サムネイル/ヒーローを意味のある文言に変更
- 外部リンク: シェア系リンクに `rel="noopener noreferrer nofollow"`

## 反映による効果（期待）
- タイトル/ディスクリプション最適化 → SERP クリック率の向上
- カノニカル/OG/Twitter → 重複回避・SNS での表示最適化
- JSON-LD → 検索エンジン理解の促進（リッチリザルトの可能性）
- 画像属性の強化 → CLS 抑制や初期表示の安定に寄与

## 経過（タイムライン）
1. 仕様整理: spec.md の要件確認（Tailwind/レイアウト/相互作用）
2. 既存実装把握: `index.html` / `article.html` の構成を確認
3. メタ情報追加: タイトル/ディスクリプション/カノニカル/OG/Twitter を両ページへ適用
4. 構造化データ挿入: `WebSite`/`Organization`/`BlogPosting`/`BreadcrumbList` を JSON-LD で追加
5. 画像・リンク調整: `alt`/`decoding`/`fetchpriority`、シェアリンク `rel` の付与
6. 確認: 目視でタグ挿入位置と整合性をチェック

## 今後の推奨（任意）
- ドメイン確定後、`canonical`/OG `url`/画像 `logo.png`/`feed.xml` の実 URL に更新
- `robots.txt` と `sitemap.xml` の設置（ビルド/デプロイ時に生成）
- OGP 画像の共通テンプレート化（記事ごとにタイトル入り画像を生成）
- パンくず UI の表示（JSON-LD は追加済み、HTML 表示は任意）
- Core Web Vitals 計測（Lighthouse/Pagespeed）と継続改善

