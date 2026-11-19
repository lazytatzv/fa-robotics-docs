# システム構成・意思決定記録（ADR）

このディレクトリには、システム構成図、安全設計、機器選定の比較表、意思決定記録（ADR）を格納します。

- [`system_overview.md`](./system_overview.md) — **全体アーキテクチャ統合図（Task 1 想定構成）**
- [`software_stack.md`](./software_stack.md) — **推奨ソフトウェアスタック一覧（OS / Docker / ROS 2 / AI / Python）**
- [`pro_selection_playbook.md`](./pro_selection_playbook.md) — **プロの機器・センサ選定プレイブック（裏チェック基準・調達ルール）**
- [`robot_selection.md`](./robot_selection.md) — 協働ロボット選定メモ（100万円前後帯・6軸方針）
- [`end_effector_selection.md`](./end_effector_selection.md) — エンドエフェクタ選定メモ（Task 1：真空吸引 vs グリッパ）
- [`vision_and_ai.md`](./vision_and_ai.md) — ビジョン・AI認識方針（RGB-D / YOLO / PoE vs USB）
- [`sensors_guide.md`](./sensors_guide.md) — 使うセンサ・知っておくべき FA センサ一覧（真空スイッチ / 光電 / 安全センサ等）
- [`controller_and_pc.md`](./controller_and_pc.md) — コントローラ構成とPC接続・OS選定（Ubuntu Linux）
- [`ros2_vs_python_sdk.md`](./ros2_vs_python_sdk.md) — ROS 2 を使うべきか（ROS 2 vs 公式 Python SDK 比較）
- [`pc_selection.md`](./pc_selection.md) — 制御PC選定ガイド（GPU / 産業用IPC vs Jetson / 工場要件）
- [`power_and_wiring.md`](./power_and_wiring.md) — 電源設計・降圧・配線方針（AC100/200V・DC24V・ノイズ対策）
