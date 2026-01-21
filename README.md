# Cursorをちゃんと使うための知識

## 公式ドキュメント

[Cursor ドキュメント](https://cursor.com/ja/docs)

## **ドキュメントの種類と特徴（一覧）**

| **種類** | **主目的** | **発動方法** | **利点** | **位置** |
| --- | --- | --- | --- | --- |
| **AGENTS.md** | プロジェクト全体の基本方針 | 自動適用 | 設定不要・簡易 | プロジェクトルート |
| **Rules** | 背景ルールの定義 | 自動/条件的/手動 | 特定ファイルで条件適用可能 | .cursor/rules/ |
| **Commands** | 定型操作の呼び出し | 手動（/入力） | 定型作業を簡略化 | .cursor/commands/ |
| **Agent Skills** | 専門知識パック | 自動判断（必要時） | 再利用・複雑ワークフロー対応 | .cursor/skills/<name>/ |
| **Subagents** | タスク委譲・並列作業 | 手動/自動 | コンテキスト分離・長タスク対応 | .cursor/agents/ |
| **Semantic Search** | コード意図ベース検索 | 自動 | 自然言語で関連箇所検索 | 仕組みとして動作 |
| **@ Mentions** | 参照ドキュメントの明示 | 手動 | ドキュメント参照を簡易化 | エディタ内から利用 |
| **Ignore Files** | 対象外ファイル制御 | 自動 | ファイル読み取り制限 | .cursorignore |

### **AGENTS.md**

- プロジェクト全体に常時適用される基本指示書（Markdown）
- 簡単な方針やプロジェクトルールを記述する際に便利
- 設定ファイル不要で最初に使うべきファイル形式（README 的）

### **Rules**

- .cursor/rules/ 内に .mdc ファイルとして配置
- 特定ファイルや対象を条件指定してルールを適用可能
- 常時背景ルールとして AI に働きかける際に使う

### **Commands**

- .cursor/commands/ 内に .md ファイルとして保存
- /<command-name> で実行する定型ワークフロー
- テスト実行、PR 作成、コードレビュー等の作業を shortcut 化できる

### **Agent Skills**

- 専門的な知識・能力を持つスキルパック
- .cursor/skills/<skill-name>/SKILL.md として構成
- 必要に応じて AI が読み込み・適用する（自動判断される）

### **Subagents**

- 専用タスクとしてエージェントを分離して実行
- コンテキストを分けてバックグラウンド処理も可能
- 大規模リサーチ・長時間タスク向け

### **Semantic Search**

- プロジェクト全体を埋め込み検索
- 意味ベースで関連箇所を見つける仕組み
- Cursor エージェント内部で自動的に活用される

### **@ Mentions**

- ドキュメント・ファイル参照を明示するための構文
- エディタ内で @Files & Folders 操作やドラッグで参照可
- コード内ドキュメント参照が簡単になる

使い方の例
```bash
@src/backend/UserService.ts を前提に設計レビューしてください
@.cursor/rules/backend-style.mdc のルールに従って修正してください
```

### **Ignore Files**

- .cursorignore でファイル/ディレクトリ単位で読み取り対象外指定
- セマンティック検索・ルール・インデックス対象を制御する
- セキュリティ・パフォーマンス向上に寄与

---

## **具体例：~/projects/sample_project 配置構成**

以下のように整理できます。

```
~/projects/sample_project/
├── AGENTS.md
├── .cursorignore
├── .cursor/
│   ├── rules/
│   │   ├── react-style.mdc
│   │   └── api-guidelines.mdc
│   ├── commands/
│   │   ├── code-review.md
│   │   └── create-pr.md
│   ├── skills/
│   │   ├── graphql-api/
│   │   │   └── SKILL.md
│   │   └── testing-best-practices/
│   │       └── SKILL.md
│   └── agents/
│       ├── research-subagent.md
│       └── audit-subagent.md
├── src/
│   └── ...
├── tests/
│   └── ...
└── README.md
```

### **各配置の目的**

- AGENTS.md
    - プロジェクト全体の基本方針・ルールを記述。
- .cursorignore
    - エージェントが読み取らないファイルを指定（例: ビルド成果物）。
- .cursor/rules/
    - 背景ルールファイルを格納（コードスタイル・ディレクトリ別適用など）。
- .cursor/commands/
    - 手動で実行する定型作業コマンド定義。
- .cursor/skills/
    - プロジェクト共通で使うスキルパック（再利用可能な専門知識）。
- .cursor/agents/
    - サブエージェント定義（複雑・時間のかかるタスクワークフロー）。

---

## **まとめ**

- **簡易な全体指示** → AGENTS.md
  - 思想や前提を記述する。毎回参照されるのでコンテキストを消費しないよう500文字以内。
- **継続的ルール適用** → Rules
- **手動定型ワークフロー** → Commands
  - 作業ショートカットのための手順書を記載する。
- **再利用可能な専門機能** → Agent Skills
- **複雑・独立処理** → Subagents
  - 重い処理・独立タスクをサブエージェントに切り出すことを親タスクのコンテキストを消費しない。
- **ドキュメント制御** → @ Mentions, .cursorignore
  - ＠メンションで特定ファイルだけ読み込む。.cursorignoreで不要なファイルや秘匿情報を参照外にしておく。
- **コード参照精度向上** → Semantic Search

8. 使い分けの指針（まとめ）

思想・前提: AGENTS.md

恒常ルール: Rules

作業ショートカット: Commands

専門知識の再利用: Skills

重い・独立タスク: Subagents

ノイズ除去: .cursorignore
すべて Cursor 内部コンテキスト管理の基本パーツとして使われます
