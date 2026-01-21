# PM向けCursorドキュメント活用例

基本的な使い方やルールは[README.md](./README.md)参照。

## PM向けの主な機能

### Commands（コマンド）
- `/create-spec` - 新規機能の仕様書を作成
- `/update-spec` - 既存仕様書の更新と変更履歴管理
- `/spec-review` - 仕様書のレビューと不明点の抽出
- `/stakeholder-alignment` - ステークホルダー間の認識合わせ

### Skills（スキル）
- `pm-spec-review` - 仕様書レビューの専門知識
- `user-story-writing` - ユーザーストーリー作成のベストプラクティス
- `acceptance-criteria` - 受け入れ基準の定義方法

### Agents（サブエージェント）
- `pm-alignment-subagent` - 仕様・要件の整理と認識合わせ
- `requirements-gathering-subagent` - 要件収集と整理

### Rules（ルール）
- `pm-spec.mdc` - 仕様管理のルール（目的・前提・スコープ・非スコープの明確化）
- `user-story.mdc` - ユーザーストーリー記述のルール

## 推奨ディレクトリ構造

```bash
docs/
├── specs/
│   ├── feature-a.md
│   └── feature-b.md
├── requirements/
│   ├── functional.md
│   └── non-functional.md
├── user-stories/
│   └── epic-1/
│       ├── story-1.md
│       └── story-2.md
├── decisions/
│   └── 2024-xx-feature-a.md
└── templates/
    └── spec-template.md
```

## 使い方の例

### 仕様書の作成
```
/create-spec

機能名: ユーザー認証機能
目的: セキュアなログイン機能を提供する
```

### 仕様書のレビュー
```
/spec-review @docs/specs/feature-a.md
```

### ステークホルダーとの認識合わせ
```
/stakeholder-alignment

会議の議事録から決定事項を抽出してください
```

## テンプレート

仕様書作成時は `docs/templates/spec-template.md` を参考にしてください。
