---
title: Skill
concept: Skill (技能 / 技能包)
date: 2026-09-05
tags: [AI, skill, capability-extension, prompt-engineering]
---

# Skill (技能 / 技能包)

## 一句话定义

**Skill**（在 Anthropic / WorkBuddy 等 Agent 体系下）= 一组**预先写好的指令 + 可选的资源**（脚本、参考文档、素材），用于把通用 Agent 武装成"某个特定领域里能稳定做事"的专家。

## 为什么学它

- 同一个底层模型，挂不同 Skill 就能变成"PPT 生成器"、"PDF 编辑员"、"数据分析师"、"概念学习助手"……**Skill 是 Agent 时代"能力分发"的最小单元**。
- 自己写好一份 Skill，未来任何对话/项目都能复用——一份投入，长期回报。

## 关键特征（5 条）

- **声明式 + 触发式**：YAML 前置元数据里的 `description` 描述"何时用"，Agent 按需自动加载。
- **SKILL.md 是主文档**：包含"何时用"和"工作流"；过长内容拆到 `references/`，按需加载节省上下文。
- **可携带资源**：`scripts/`（可执行代码）、`references/`（按需查阅的文档）、`assets/`（模板/字体等素材）。
- **两层作用域**：
  - **项目级**：放在仓库的 `.workbuddy/skills/<name>/`——仓库共享、跟随代码。
  - **用户级**：放在 `~/.workbuddy/skills/<name>/`——跨项目跟随用户本人。
- **可被 SkillManage 修改**：`agent_created: true` 标记的 Skill 可被 SkillManage 工具更新/删除（marketplace 安装的 Skill 默认只读）。

## 与相近概念的对比

| 概念 | 谁拥有 | 谁加载 | 典型场景 |
|---|---|---|---|
| **Skill** | 仓库 / 用户 | Agent 自动按需加载 | 领域知识 + 工作流 |
| System Prompt | 模型启动时人工写 | 模型硬加载 | 控制模型人格/语气 |
| Tool / Function Call | Agent runtime | Agent 决策时调用 | 查 DB、发邮件 |
| RAG 知识库 | 独立服务 | 运行时检索 | 长尾、可变的事实 |
| Plugin / MCP | 外部服务 + 协议 | Agent 通过协议接入 | 调用 GitHub / Slack 等 |

> 一句话区分：**Skill = 告诉 Agent "怎么想 / 怎么写"**；Tool = 告诉 Agent "能做什么"。

## 一个具体的例子

> 场景：让 WorkBuddy 在仓库里生成"概念学习资料"。
> 你写一个 Skill：`concept-study`
> ├── `SKILL.md`（何时用 + 怎么生成结构化笔记）
> └── `references/concept_template.md`（每篇笔记的 Markdown 模板）
>
> 下次你说"用 Skill 学习 Agent"——Agent 读到 `concept-study/SKILL.md`，按模板去 `notes/concepts/agent.md` 写笔记。同一份 Skill 可给"上下文"、"Skill"等任意概念复用。

## 常见误解（4 条）

- **误解：Skill = 提示词 (prompt)。** 正解：Skill 是有触发逻辑、能附带资源的"领域包"，不只是几句话。
- **误解：Skill 越多 Agent 越强。** 正解：每个 Skill 都占上下文；超量会稀释注意力。建议按需启用 + 项目级隔离。
- **误解：Skill 必须配代码。** 正解：纯文档型 Skill（就像本课程的 `concept-study`）也完全有效；`scripts/` 可选。
- **误解：Skill 是模型厂商黑话。** 正解：是通用范式——Anthropic、OpenAI、各类 Agent 框架都有类似机制，叫法略有差异。

## 自检问题

1. 【复述】用自己的话讲清楚 Skill 是什么、它和 System Prompt 差在哪？
2. 【对比】Skill、Tool、RAG 三者在"扩展 Agent 能力"上各自解决什么问题？
3. 【应用】你现在学的"统计与数据分析"课，能写出什么样的 Skill？请用一句话写它的 `description`。
4. 【判断】什么场景**不该**用 Skill（直接 system prompt 就行）？什么场景**必须**用 Skill？
5. 【延伸】Skill 的"项目级 / 用户级"两层结构是为了解决什么问题？

## 下一步行动

- [ ] **读**：`workbuddy-builtin` 中 `skill-creator/SKILL.md`，理解 Skill 的设计哲学（"渐进式披露"、三层加载）。
- [ ] **做**：把今天的 `concept-study` Skill 在另一个项目里复用一次，观察"项目级 vs 用户级"差异。
- [ ] **输出**：另写一个 Skill（选题自拟）发到仓库的 `.workbuddy/skills/` 下，并写一段"为什么这个 Skill 值得存在"的 README。
