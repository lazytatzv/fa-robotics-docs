# システム全体アーキテクチャ（Task 1 想定構成）

ここまでの検討（6軸協働ロボット・真空吸引・RGB-D＋YOLO・Ubuntu IPC・DC24V電源）を統合した全体構成図です。

```mermaid
flowchart TB
    subgraph FIELD["工場現場・ハードウェア"]
        PWR["工場電源<br/>AC100V / 200V"] --> PSU["制御盤<br/>ブレーカー / DC24V電源<br/>安全リレー"]
        AIR["工場圧縮エア"] --> EJ["真空エジェクタ・電磁弁<br/>真空圧力スイッチ (DC24V)"]
        ESTOP["非常停止ボタン<br/>安全機器"] -->|"Safety I/O (ハード直結)"| CTRL["ロボットコントローラ"]
        PSU --> CTRL
        PSU --> PC
        PSU -->|"DC24V"| EJ
        CTRL -->|"動力・エンコーダ"| ARM["6軸協働ロボット<br/>(本体100万円帯)"]
        ARM --> PAD["真空吸着パッド<br/>(蛇腹型＋バネバッファ)"]
        EJ -->|"負圧チューブ"| PAD
        CTRL <-->|"24V DI/DO"| EJ
    end

    subgraph COMPUTE["制御PC (Ubuntu 22.04/24.04 LTS / x86_64 + GPU)"]
        CAM["固定カメラ<br/>PoE / USB3 RGB-D"] -->|"RGB + Depth"| YOLO["AI推論 (YOLO-pose / seg)<br/>＋ 座標変換 (Hand-Eye)"]
        YOLO --> SM["全体制御ステートマシン<br/>(ROS 2 / Python)"]
    end

    SM <-->|"Ethernet (TCP/IP)<br/>SDK / ROS 2"| CTRL
```

## 構成サマリーと関連ドキュメント

| レイヤ | 採用方針 | 詳細ドキュメント |
| --- | --- | --- |
| **ロボット本体** | 6軸協働ロボット（本体100万円前後帯） | [`robot_selection.md`](./robot_selection.md) |
| **エンドエフェクタ** | 真空吸引（蛇腹パッド＋バネバッファ＋真空スイッチ） | [`end_effector_selection.md`](./end_effector_selection.md) |
| **ビジョン・AI** | 固定 RGB-D カメラ ＋ YOLO-pose / seg（PoE推奨、PoCはUSB可） | [`vision_and_ai.md`](./vision_and_ai.md) |
| **コントローラ連携** | Ethernet (TCP/IP) 経由で座標・I/O指令、安全回路はハード直結 | [`controller_and_pc.md`](./controller_and_pc.md) |
| **制御PC・OS** | Ubuntu LTS（x86_64 + NVIDIA GPU）、本番は産業用IPC | [`pc_selection.md`](./pc_selection.md) |
| **電源・配線** | AC100/200V分岐 ＋ FA用DC24Vスイッチング電源＋サージ対策 | [`power_and_wiring.md`](./power_and_wiring.md) |
