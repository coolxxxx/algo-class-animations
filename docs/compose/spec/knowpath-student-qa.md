---
feature: knowpath-student-qa
status: delivered
updated: 2026-09-14
branch: main
commits: 1227ed4..HEAD
---

# 以知识点为中心的学生学习路径

## Report

## Report

**What was built** — 展示台每课增加「🧭 学习路径 · 学生八问」：是什么 / 例子(VOX) / 解决什么 / 代码 / 语法 / 上手 / 哪里用 / 为何学。KNOW 覆盖全部 44 个 VOX 课号；无 KNOW 的课不编 3/7/8 空话。VOX 作为第 2 步入口，旁挂按钮保留。

**Verification** — node 解析 KNOW+renderKnowPath PASS（44 keys）；VOX 课号 − KNOW 课号 = 空集。

**Journey log**
1. VOX 旁挂 → 路径第 2 步，学生问题链才闭环
2. 无 KNOW 硬填空话被评审打回 → 有字段才渲染 3/7/8
3. 缺口是 WHY/REFLECT 文案与串联，不是缺外部仓库

## [S1] Problem
展示台已有故事/代码/动画/语法卡/测验/VOX 按钮，但资源是「旁挂」：
- 学生看不到「解决什么问题 / 哪里用得上 / 为什么要学」
- VOX 是独立按钮，不是「先看懂过程」的一环
- 没有按学生提问顺序串起来的路径

## [S2] Design
在每课增加「🧭 学习路径 · 学生八问」面板，按固定顺序回答：

| # | 学生问 | 数据来源 |
|---|---|---|
| 1 | 这是什么意思？ | lesson.story（比喻） |
| 2 | 能不能举例 / 看懂过程？ | VOX（若有）+ 运行动画 |
| 3 | 解决什么问题？ | KNOW.why（新） |
| 4 | 代码怎么实现？ | lesson.code 高亮 |
| 5 | 语法注意什么？ | SYN 语法卡 |
| 6 | 如何上手？ | KNOW.first + tryit |
| 7 | 哪里用得上？ | KNOW.where（新） |
| 8 | 为什么要学？ | KNOW.reflect（新） |

- `KNOW[lessonId] = { why, where, reflect, first[] }`，先为已有 VOX 的算法课写满
- 无 KNOW 的课：面板只显示已有 1/2/4/5/6，不硬编空话
- VOX 从旁挂按钮变为路径第 2 步入口；按钮保留快捷方式
- 学生模式任务卡与路径对齐（有 KNOW 时提示走八问）

## [S3] Out of Scope
- 不重写全部 64 课文案（先覆盖 VOX 算法知识点）
- 不引入外部新仓库（现有资源够用；缺口是「串联与 WHY/REFLECT 文案」，不是缺工具）
- 不改授权逻辑

## Tasks
- [x] T1: 注入 KNOW 数据 + 路径 UI/CSS/JS — acceptance: 有 KNOW 的课显示八问面板 (covers: S2)
- [x] T2: VOX 嵌入路径第2步 — acceptance: 点路径可看 VOX，旁挂按钮仍在 (covers: S2; depends: T1)
- [x] T3: 覆盖主要算法课 KNOW 文案 — acceptance: VOX 映射课均有 why/where/reflect/first (covers: S2; depends: T1)
- [x] T4: 推送并验证 — acceptance: Pages 打开某算法课可见学习路径 (covers: S2)
