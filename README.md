# content-organizer

**MX（Media Mix）の型を実装する、コンテンツ横断の統合・調整エージェント。**

content-organizer 自身は、本・動画・イベントの制作ドメインではない。

複数の専門ドメインをひとつの企画として統べ、開発・制作・マーケティングがドメインごとにばらつかないように、共通の目的・企画・成果物・依存関係・コスト・スケジュールを管理する。

## Position

```
                         MX
                  Media Mix の型
                         │
                         ▼
               content-organizer
                統合・調整エージェント
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
         本              動画            イベント
          │              │              │
 editor-agent      video-editor    event-organizer
```

## Domain boundary

| Layer | Repository | Responsibility |
|---|---|---|
| Archetype | MX | Media Mix の型 |
| Instance / Orchestrator | content-organizer | 複数ドメインの統合・調整 |
| Book domain | editor-agent | 本の企画・編集・制作管理 |
| Video domain | video-editor | 動画編集・制作 |
| Event domain | event-organizer | イベント企画・制作管理 |

## Core responsibility

content-organizer は各ドメインの専門作業を奪わない。

- 共通企画
- audience / target
- message / proposition
- world / brand consistency
- deliverables
- domain dependencies
- milestones
- schedule
- budget / cost
- marketing
- distribution
- cross-media promotion
- feedback
- priority
- acceptance criteria

## One project, three domains

```
企画
  ↓
content-organizer
  │
  ├── 共通企画
  ├── ターゲット
  ├── メッセージ
  ├── 世界観
  ├── KPI
  ├── 予算
  ├── スケジュール
  └── dependencies
          │
    ┌─────┼─────┐
    ▼     ▼     ▼
   本    動画   イベント
    │     │      │
editor- video- event-
agent   editor organizer
```

各ドメインは専門性を持つ。しかし、**企画の目的と全体整合性は content-organizer が持つ。**

## Anti-drift

最大の目的は **domain drift の防止**。

本・動画・イベントを別々のプロジェクトとして開発すると、メッセージ、ターゲット、スケジュール、予算、マーケティングが分断される。

content-organizer は共通の企画状態を canonical な情報として保持し、各 domain agent に必要な契約だけを渡す。

```
Shared Intent
     │
     ▼
content-organizer
     │
     ├── book contract ──→ editor-agent
     ├── video contract → video-editor
     └── event contract → event-organizer
```

## Marketing

content-organizer は制作進行だけでなく、メディアミックス全体のマーケティングも管理する。

```
Market
  ↓
Audience
  ↓
Intent
  ↓
Content strategy
  ↓
Book + Video + Event
  ↓
Distribution
  ↓
Promotion
  ↓
Feedback
  ↺
```

## PM hierarchy

- **content-organizer** = media-mix PM
- **editor-agent** = book/editorial PM
- **video-editor** = video production PM
- **event-organizer** = event PM

上位PMが下位ドメインの専門実装を置き換えるのではなく、目的・契約・依存関係を調整する。

## Principle

> **専門化することで深くなり、統合することでバラバラにならない。**

> **content-organizer は作る人ではなく、複数の作る人・エージェントを一つの企画として成立させる。**

## Relationship

```
MX
└── content-organizer
      ├── editor-agent
      ├── video-editor
      └── event-organizer
```

**MX は型。**

**content-organizer はその型のインスタンス。**

**editor-agent / video-editor / event-organizer は専門ドメイン。**
