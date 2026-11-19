# fa-robotics-docs

ソフトウェアエンジニア中心のチームに向けた、**ロボット・FA（工場自動化）の基礎教育**と**実際の自動化案件の要件・設計ドキュメント**をまとめるリポジトリです。

---

## 現在の案件サマリー（Task 1：優先度高）
- **対象作業**：2階からまとめて落下してくる**空ボトル**（基本不透明＋一部色付き透明、若干の形状差あり）を山積み状態から拾い、コンベアレーンへ載せる工程
- **想定構成**：
  - **ロボット**：6軸協働ロボット（本体100万円前後帯）
  - **エンドエフェクタ**：真空吸引（蛇腹パッド＋バネバッファ＋真空スイッチ）
  - **ビジョン・AI**：固定 RGB-D カメラ（PoE推奨／PoCはUSB可）＋ YOLO-pose / seg
  - **制御PC・OS**：Ubuntu LTS（x86_64 + NVIDIA GPU、本番は産業用IPC）

---

## ドキュメント一覧（サイトマップ）

### 1. 現場分析・要件定義 (`docs/01_field_analysis/`)
- [`project_requirements.md`](./docs/01_field_analysis/project_requirements.md) — 案件全体の前提条件・要確認リスト
- [`task1_bottle_picking.md`](./docs/01_field_analysis/task1_bottle_picking.md) — **Task 1：落下ボトルのピック＆プレース分析**
- [`hearing_template.md`](./docs/01_field_analysis/hearing_template.md) — 現場ヒアリング・抜け漏れチェック用テンプレート

### 2. 進め方・PoC計画 (`docs/02_execution_plan/`)
- [`fa_roadmap.md`](./docs/02_execution_plan/fa_roadmap.md) — 手戻りを防ぐFA導入ロードマップ（Step 1〜5）
- [`poc_checklist.md`](./docs/02_execution_plan/poc_checklist.md) — **Task 1 PoC（要素検証）チェックリスト**

### 3. ソフト屋向け ロボット・FA基礎教材 (`docs/03_robotics_handbook/`)
- [`README.md`](./docs/03_robotics_handbook/README.md) — ソフト開発とFAのギャップ一覧
- [`00_essential_curriculum.md`](./docs/03_robotics_handbook/00_essential_curriculum.md) — **ロボット素人が身につけるべき必須知識・完全チェックリスト**
- [`01_coordinates_and_tf.md`](./docs/03_robotics_handbook/01_coordinates_and_tf.md) — 座標系（TF）と Hand-Eye キャリブレーション
- [`02_kinematics_and_motion.md`](./docs/03_robotics_handbook/02_kinematics_and_motion.md) — 運動学（FK/IK）・MoveJ/MoveL・特異点回避
- [`03_safety_and_recovery.md`](./docs/03_robotics_handbook/03_safety_and_recovery.md) — 安全設計（ハード安全回路）・異常系・ステートマシン
- [`04_hardware_and_pneumatics.md`](./docs/03_robotics_handbook/04_hardware_and_pneumatics.md) — ハードウェア仕様・真空吸引（エジェクタ・破壊ブロー）
- [`05_fa_io_and_plc.md`](./docs/03_robotics_handbook/05_fa_io_and_plc.md) — 電気 I/O（DC24V・NPN/PNP・サージ対策）

### 4. システムアーキテクチャ・選定 (`docs/04_architecture/`)
- [`system_overview.md`](./docs/04_architecture/system_overview.md) — **全体アーキテクチャ統合図**
- [`robot_selection.md`](./docs/04_architecture/robot_selection.md) — 協働ロボット選定（100万円前後帯・6軸方針）
- [`end_effector_selection.md`](./docs/04_architecture/end_effector_selection.md) — エンドエフェクタ選定（真空吸引 vs グリッパ）
- [`vision_and_ai.md`](./docs/04_architecture/vision_and_ai.md) — ビジョン・AI認識（RGB-D・YOLO・PoE vs USB）
- [`controller_and_pc.md`](./docs/04_architecture/controller_and_pc.md) — コントローラ構成・PC接続・OS選定（Ubuntu）
- [`ros2_vs_python_sdk.md`](./docs/04_architecture/ros2_vs_python_sdk.md) — ROS 2 を使うべきか（ROS 2 vs 公式 Python SDK）
- [`pc_selection.md`](./docs/04_architecture/pc_selection.md) — 制御PC選定（GPU / 産業用IPC vs Jetson）
- [`power_and_wiring.md`](./docs/04_architecture/power_and_wiring.md) — 電源設計・降圧（DC24V）・ノイズ対策

### 5. 外部連携・保守運用 (`docs/05_operations/`)
- [`connectivity_and_maintenance.md`](./docs/05_operations/connectivity_and_maintenance.md) — 周辺設備連携（コンベア/センサ/LTE保守）と導入後メンテナンス設計
- [`os_and_network_setup.md`](./docs/05_operations/os_and_network_setup.md) — **OS本番設定（Ubuntu）と工場ネットワーク構成（2系統分離）**

---

## チームでの運用ルール（案）
- **確認事項・タスク管理**：GitHub Issues に起票して担当者を割り当てる
- **技術相談・Q&A**：GitHub Discussions または PR 上で議論する
- **図解**：Markdown 内の Mermaid 記法を基本とし、現場の動画・重い3Dデータは別ストレージに置いてリンクを貼る
