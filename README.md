# Windows 11 25H2 ETW Game Performance Analysis

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
