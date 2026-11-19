# fa-robotics-docs

ソフトウェアエンジニア中心のチームに向けた、**ロボット・FA（工場自動化）の基礎教育**と**実際の自動化案件の要件・設計ドキュメント**をまとめるリポジトリです。

## ディレクトリ構成

- [`docs/01_field_analysis/`](./docs/01_field_analysis/) — 工場の現状分析・ヒアリング内容・ワークや環境の仕様
  - [`hearing_template.md`](./docs/01_field_analysis/hearing_template.md) — 状況整理・抜け漏れ確認用テンプレート
- [`docs/02_execution_plan/`](./docs/02_execution_plan/) — FA導入の進め方・PoC計画・ロードマップ
  - [`fa_roadmap.md`](./docs/02_execution_plan/fa_roadmap.md) — 手戻りを防ぐFA開発プロセス（Step 1〜5）
- [`docs/03_robotics_handbook/`](./docs/03_robotics_handbook/) — ソフト屋チーム向けロボット・FA基礎教材
  - [`README.md`](./docs/03_robotics_handbook/README.md) — ソフトウェア開発とのギャップ・教えるべき基礎項目一覧
- [`docs/04_architecture/`](./docs/04_architecture/) — システム構成・安全設計・機器選定・意思決定記録（ADR）

## 運用ルール（案）

- **疑問点・確認事項**は GitHub Issues に起票して担当者を割り当てる
- **設計方針や技術的なQ&A**は Discussions または PR 上で議論する
- **図解**は Markdown 内の Mermaid 記法を基本とし、重い動画や3Dデータは別ストレージに置いてリンクを貼る
