# 推奨ソフトウェアスタック（Task 1〜FA標準構成）

ソフトウェアチームが技術選定で迷わず開発に入れるよう、**OS から AI・ロボット制御・運用保守までの一貫した推奨ソフトウェアスタック**を定義します。

---

## 1. レイヤ別 推奨スタック一覧

| レイヤ | 採用技術（推奨） | 選定理由・補足 |
| --- | --- | --- |
| **ホスト OS** | **Ubuntu 22.04 / 24.04 LTS** (Server / Desktop Minimal) | ROS 2・NVIDIA GPU・カメラ SDK の Tier 1 サポート環境。標準カーネル使用（`PREEMPT_RT` 不要） |
| **コンテナ基盤** | **Docker Engine (`apt`公式) ＋ Docker Compose** | CUDA / TensorRT / ROS 2 の依存隔離、予備機への即時復元、ロールバックが容易（Snap版は使わない） |
| **GPU ランタイム** | **NVIDIA Driver ＋ NVIDIA Container Toolkit** | コンテナ内から GPU を使って YOLO 推論を行うため必須 |
| **ロボティクス基盤** | **ROS 2 LTS（Humble / Jazzy）＋ CycloneDDS** | 上位層の疎結合化、`tf2`（座標変換）、`rviz2`（3D可視化）、`rosbag2`（録画再生）のみ活用。CycloneDDS が設定しやすく安定 |
| **カメラドライバ** | `realsense-ros` または `OrbbecSDK_ROS2` | カメラメーカー公式の ROS 2 パッケージをコンテナで動かす |
| **AI 推論・学習** | **Ultralytics YOLO (`pose` / `seg`) ＋ TensorRT** | 学習は PyTorch、本番推論は TensorRT (`.engine`) 化して 5〜15ms/frame で高速化 |
| **アノテーション** | **CVAT**（社内 Docker 構築） | 工場画像を外部クラウドへ出さず、複数人でキーポイント／ポリゴン作業が可能 |
| **座標計算・画像** | **OpenCV (`cv2`) / NumPy / SciPy** | Hand-Eye 変換、Depth 外れ値除去（中央値・パーセンタイル算出）、ArUco マーカ検出 |
| **ロボット制御** | **Python 3 ＋ メーカー公式 Python SDK** | MoveIt 2 を使わず、薄い ROS 2 ラッパーノード経由で `MoveJ` / `MoveL`・24V DI/DO を叩く |
| **PLC 通信（必要時）** | **`pymodbus`**（Modbus TCP） | 既存 PLC と LAN 連携が必要な場合のみ使用（基本は 24V DI/DO 接点または独立運用） |
| **設定管理** | **YAML**（`hand_eye.yaml`, `robot_params.yaml`） | 現地でのキャリブレーション値・速度・進入禁止範囲をコード変更なしで調整可能にする |
| **現場 Web UI（必要時）** | **FastAPI** ＋ 最小 HTML/JS（or `rosbridge_suite`） | 停止理由の日本語表示・YOLO映像確認・品種切替が必要になった場合のみ 1画面で用意 |
| **開発・品質管理** | **Git / GitHub ＋ VS Code (Remote-SSH) ＋ `uv` / `ruff` / `pytest`** | Python パッケージ管理は `uv`、Linter は `ruff`、座標計算やステートマシンの単体テストを `pytest` で回す |
| **遠隔保守・監視** | **Tailscale / WireGuard ＋ SSH ＋ `logrotate`** | 産業用 LTE ルータ経由で安全にログ回収・エラー画像確認 |

---

## 2. フェーズ別の立ち上げ方（最初から全部盛りにしない）

1. **Phase A（机上 PoC 2〜4週間）**：
   - Ubuntu ＋ `uv`（または `venv`）上で、**Python ＋ YOLO ＋ OpenCV ＋ メーカー公式 Python SDK** だけで最小構成を作り、まず「実機がボトルを掴んで置く」を動かす。
2. **Phase B〜C（テストベンチ〜工場本番）**：
   - 処理の分離・録画デバッグ・自動起動が必要になった段階で **ROS 2（上位層）＋ Docker Compose ＋ TensorRT** に整理して本番化する。
