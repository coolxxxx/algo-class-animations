---
feature: vox-quality-pass
status: delivered
updated: 2026-09-14
branch: main
commits: 215d188..0d2f97e
---

# VOX 质量短板修复

## Report

**What was built** — stack 线稿去豆腐字并小手重渲；新增 vox-queue（FIFO+STL push/front/pop）并挂 cpp6-6；第一批 bubble/binary/pointer/hanoi 统一 --hand-scale 0.34 重渲。首页加队列入口。

**Verification** — 6× render EXIT=0；6× mux duration 完整（stack/queue/binary/pointer/hanoi=16s，bubble=18s）；QC 抽帧无豆腐、手不糊屏；VOX_MAP cpp6-6 指向 vox-queue。

**Journey log**
1. ✓ 在 msyh 缺字 → 改用中文「匹配成功」类文案
2. cpp6-6 原 stretch 映射栈片 → 独立队列片更贴课

## [S1] Problem
1. `vox-stack` 线稿「✓」为豆腐块（字体缺字）
2. `cpp6-6` STL stack/queue 被 stretch 映射到括号匹配片，无队列本体内容
3. 第一批 4 条（bubble/binary/pointer/hanoi）仍用默认大手（493px），挡住内容；第二三批已用 `--hand-scale 0.34`

## [S2] Design
- 修 stack 线稿缺字 → 重渲 stack（小手）
- 新增 `vox-queue.mp4`：队列 FIFO + STL push/front/pop，映射 `cpp6-6`
- 第一批源图/标注仍在 `vox补充包`，用 `--hand-scale 0.34` + apad 重渲合轨
- 风格与现有一致：暖纸底、空白笔杆、烧字幕、16–18s

## [S3] Out of Scope
- 不扩 assemble.html / 题单
- 不改授权逻辑
- 不重做第二三批

## Tasks
- [x] T1: 修 stack 豆腐字并重渲 — acceptance: 无豆腐块，16s 成片 (covers: S2)
- [x] T2: 新增队列 VOX 并挂 cpp6-6 — acceptance: vox-queue 可播，映射正确 (covers: S2)
- [x] T3: 第一批 4 条小手重渲 — acceptance: 四条 duration 完整、手不糊半屏 (covers: S2)
- [x] T4: 推送并验证 Pages — acceptance: origin/main 同步 (covers: S2)
