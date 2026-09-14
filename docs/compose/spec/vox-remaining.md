---
feature: vox-remaining-knowledge-points
status: delivered
updated: 2026-09-14
branch: main
commits: 49ce658..36fda72
---

# 按知识点补完剩余 VOX

## Report

**What was built** — 第三批 11 条算法向 VOX：栈括号匹配、BFS、DFS 全排列、位运算、约瑟夫环、活动选择、最大子段和、二叉树前序、GCD 辗转相除、高精度加法、贪心找零。每条 16s，小手（--hand-scale 0.34）、apad 补静音、烧字幕。VOX_MAP 覆盖主要算法课；找零钱不再误挂分治片。工作区说明：沙箱禁止 git worktree add，沿用站点仓 main 直推。

**Verification** — 11× render_stream_whiteboard EXIT=0；11× ffmpeg mux EXIT=0，ffprobe duration=16.000；edge-tts 全部生成（gcd 首次 NoAudioReceived 重试成功）。首页/映射由 HTML  grep 校验。

**Journey log**
1. multiline text 触发 PIL textlength 报错 → 拆成两行 box
2. edge-tts 偶发 NoAudioReceived → 改写文案+重试即可
3. Read 工具对 临时日志缓存 路径偶发 File not found，但文件在盘上有效
4. 找零钱原先误挂 divide-greedy → 本批独立成片并改映射

## [S1] Problem
展示台约 30 课，已有 12 条 VOX（递归/排序/二分/指针/汉诺塔/链表/埃氏筛等）。
剩余算法向知识点（栈、BFS、DFS、位运算、约瑟夫、活动选择、最大子段和、二叉树、GCD、高精度、找零钱）无本课 VOX；
且 `py6-2`/`cpp6-3` 找零钱误挂到分治贪心片。

## [S2] Design
- 管线复用：PIL 线稿（暖纸底 #F5EBD7）→ annotation.json → `render_stream_whiteboard.py --hand-scale 0.34` → edge-tts → `apad` 合轨 → 烧字幕 → 拷入 `videos/vox-*.mp4`
- 风格：极简手绘、空白笔杆、无 AI 水印、已烧字幕
- 每条 16–18s，两段式 reveal（region1 概念 / region2 核心）
- 更新 `VOX_MAP` 与首页 VOX 卡入口
- 工作区说明：沙箱禁止 `git worktree add`，沿用站点仓 main 直推（与前两批一致）

## [S3] Out of Scope
- 语法课（input/print/类封装细节）不做单独 VOX
- 不重渲已有 12 条成片（除非 QC 不合格）
- 不改展示台授权/测验逻辑

## Tasks
- [x] T1: 绘制 11 张线稿 + annotation — acceptance: 无水印、教学信息清晰、文件落盘 (covers: S2)
- [x] T2: 渲染 11 条 VOX 并配音烧字幕 — acceptance: 时长完整、字幕可见、手尺度正常 (covers: S2; depends: T1)
- [x] T3: 拷入站点并更新 VOX_MAP/首页 — acceptance: 映射正确、找零钱不再误挂 (covers: S2; depends: T2)
- [x] T4: 推送 GitHub 并抽查 Pages — acceptance: origin/main 同步、首页含新入口 (covers: S2; depends: T3)

