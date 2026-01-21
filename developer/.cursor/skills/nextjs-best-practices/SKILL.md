# Next.js Best Practices Skill

## このスキルの役割
- Next.js アプリケーションの設計・実装レビューを支援する
- App Router と Pages Router の適切な使い分けを判断する

## 前提知識
- Next.js 14.x（App Router）
- React Server Components
- Server Actions

## 判断基準
- App Router と Pages Router の適切な使い分け
- Server Components と Client Components の適切な分離
- データフェッチング戦略（Server Components vs API Routes）
- メタデータの適切な設定
- 画像最適化（next/image）の使用

## よくある改善提案
- Server Components をデフォルトで使用し、必要な場合のみ Client Components を使用
- API Routes の代わりに Server Actions を検討
- 動的インポートによるコード分割
- メタデータの適切な設定（SEO 向上）
- 画像の最適化と lazy loading
