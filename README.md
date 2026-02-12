# Windows 11 25H2 ETW Game Performance Analysis


# Windows 11 25H2 ETW Game Performance Analysis

## Overview
Windows 11 25H2 (KB5074109) 環境において、主要なゲームタイトルを対象に **ETW (Event Tracing for Windows)**、**WPR (Windows Performance Recorder)**、**WPA (Windows Performance Analyzer)** を用いた統合パフォーマンス解析を実施しました。

本レポートでは、CPUスケジューリング、メモリ管理、ディスクI/O、およびGPUアクティビティ（DxgKrnl）を相関的に分析し、OSビルド更新による挙動の変化やボトルネックの特定を目的としています。

## Environment
検証環境は以下の通りです。

| Component | Detail |
| :--- | :--- |
| **OS** | Windows 11 25H2 (KB5074109) |
| **GPU** | NVIDIA GeForce RTX 3060 |
| **Tooling** | Windows Performance Recorder (WPR)<br>Windows Performance Analyzer (WPA) |
| **Trace Profile** | Custom `gpu_full.wprp` |

## Trace Targets
以下の3タイトルについて、「1タイトル・1セッション」でトレースを取得しました。

1. **Zenless Zone Zero (ゼンレスゾーンゼロ)**
2. **Wuthering Waves (鳴潮)**
3. **Twinkle Star Knights (ティンクルスターナイツ)**

## Captured Metrics
`gpu_full.wprp` を使用し、以下のメトリクスを同一ETLファイル内で同時取得しています。

* **CPU Scheduling:**
    * Context Switch (CSwitch)
    * ReadyThread (スレッド待機要因の分析)
* **Memory:**
    * HardFaults (ページフォールトによる遅延)
* **Disk I/O:**
    * Read/Write Latency
    * File I/O
* **GPU Activity:**
    * **DxgKrnl:** DirectX Kernel イベント
    * **GPU Usage:** DWM / Win32k / Graphics Queue

## Analysis Methodology
WPAを用いて以下の観点から解析を行います。

1.  **CPU/GPU相関:** レンダリングパイプラインにおけるCPUバウンド（Render Thread）とGPUバウンドの切り分け。
2.  **Stuttering要因:** フレームドロップ発生時の Disk I/O (HardFaults) および ReadyThread の挙動確認。
3.  **OS Overhead:** Windows 11 25H2 特有のバックグラウンドプロセスやスケジューラ挙動の影響。

## Disclaimer
* 本レポートは特定のハードウェア環境およびOSビルド (25H2 KB5074109) における検証結果であり、全ての環境での動作を保証するものではありません。
* ETWトレースの解析結果は、取得タイミングやバックグラウンドタスクの影響を受ける可能性があります。
* 各ゲームタイトルのアップデート状況により、パフォーマンス特性は変化する場合があります。

---

## Analysis Results (Template)

### 1. Zenless Zone Zero
* **Engine:** Unity
* **Observations:**
    * [CPU] P-Coreへのスレッド割り当て状況: ...
    * [GPU] シェーダー負荷の高いシーンでのDxgKrnlキュー: ...

### 2. Wuthering Waves
* **Engine:** Unreal Engine
* **Observations:**
    * [I/O] オープンワールド移動時のAsset Streaming遅延: ...
    * [Memory] スタッタリング発生時のHardFaults相関: ...

### 3. Twinkle Star Knights
* **Platform:** Browser / WebGL / Electron
* **Observations:**
    * [GPU] 2D描画時の電力効率とGPU Clock変動: ...
    * [CPU] シングルスレッド性能への依存度: ...
## Environment
- Windows 11 25H2 (KB5074109)
- NVIDIA RTX 3060
- WPR + WPA

## Captured Metrics
- CPU Scheduling
- CSwitch / ReadyThread
- HardFaults
- Disk IO
- DxgKrnl GPU Activity

## Tested Titles
- Zenless Zone Zero
- Wuthering Waves
- Twinkle Star Knights




# Windows 11 25H2 Performance Trace (ETW/WPR)

## Overview
Windows 11 25H2 (KB5074109) 環境において、
複数ゲームタイトルを対象に ETW / WPR / WPA を用いた
CPU / Memory / Disk / GPU の統合パフォーマンス解析を行った。

## Environment
- OS: Windows 11 25H2 (KB5074109)
- Tooling:
  - Windows Performance Recorder
  - Windows Performance Analyzer
- Trace Profile:
  - Custom WPRP (gpu_full.wprp)

## Trace Targets
- Twinkle Star Knights
- Zenless Zone Zero
- Wuthering Waves

## Notes
- 各ETLは「1タイトル・1セッション」で取得
- CPU/GPU/Memory/Disk は同一ETL内で同時取得
- GPU使用率は DxgKrnl / DWM / Win32k イベントベースで解析

## Disclaimer
ETLファイルにはプロセス名・システムイベントが含まれます。
個人情報・アカウント情報は含まれていませんが、
取り扱いには注意してください。

## 関連記事
https://note.com/kyona_blog/n/n77de33b2b02b
