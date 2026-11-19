# システム構成・意思決定記録（ADR）

このディレクトリには、システム構成図、安全設計、機器選定の比較表、意思決定記録（ADR）を格納します。

- [`robot_selection.md`](./robot_selection.md) — 協働ロボット選定メモ（100万円前後帯・軸数方針）
- [`end_effector_selection.md`](./end_effector_selection.md) — エンドエフェクタ選定メモ（Task 1：真空吸引 vs グリッパ）
- [`vision_and_ai.md`](./vision_and_ai.md) — ビジョン・AI認識方針（Task 1：カメラ・YOLO活用）
- [`controller_and_pc.md`](./controller_and_pc.md) — コントローラ構成とPC接続（Ethernet / SDK / 24V I/O）
- [`pc_selection.md`](./pc_selection.md) — 制御PC選定ガイド（GPU / 産業用IPC vs Jetson / 工場要件）
- [`power_and_wiring.md`](./power_and_wiring.md) — 電源設計・降圧・配線方針（AC100/200V・DC24V・ノイズ対策）
