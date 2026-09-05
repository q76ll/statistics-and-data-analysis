---
title: 概念学习笔记索引
date: 2026-09-05
tags: [index, concepts]
---

# 概念学习笔记

> 本目录由 [`concept-study` Skill](../../.workbuddy/skills/concept-study/SKILL.md) 维护。每个概念一份笔记，按统一模板：**定义 → 为什么学 → 关键特征 → 对比 → 例子 → 误解 → 自检 → 下一步**。
>
> 每次新生成一篇概念，本文件会自动（在对话中）追加一行；想自己更新也可以按下面表格的格式补一行。

## 目录

| # | 概念 | slug | 一句话定义 | 标签 |
|---|---|---|---|---|
| 01 | Agent | [`agent`](./agent.md) | LLM 驱动的、能自主循环地调用工具直到完成目标的程序 | AI, agent, autonomy, tool-use |
| 02 | 大模型的上下文 | [`llm-context`](./llm-context.md) | 一次推理中模型能"看见"并据以生成下一段文本的全部输入，受 context window 限制 | LLM, context-window, prompt, attention |
| 03 | Skill | [`skill`](./skill.md) | 一组预先写好的指令与资源，用于把通用 Agent 武装成某领域专家 | AI, skill, capability-extension, prompt-engineering |

## 怎么用

1. **快速过**：点开链接，先读"一句话定义"+"关键特征"+末尾"下一步"，3 分钟一个概念。
2. **扎实学**：合上文件，口头/书面回答每篇笔记的**自检问题 1、3、5**——能答上来才算过。
3. **拓展**：用 Skill 再生成新概念，本表自动扩展。

## 新增一篇的流程

> 由 `concept-study` Skill 执行一次"生成单个概念"的标准流程即可——本文件无需手动改，但若要保持表格整齐，记得把新行追加到 `## 目录` 即可。
