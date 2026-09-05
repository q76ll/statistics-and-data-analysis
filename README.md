# 📘 statistics-and-data-analysis

一个**演示"个人概念学习 Skill + 学习资料"** 的 GitHub 仓库。本仓库展示如何从零构建一个项目级 Skill，以及它如何用于系统化学习任意概念。

> 仓库原名虽然含有 "statistics-and-data-analysis"，但当前内容**已经偏向"概念学习 Skill 演示"**——之前留下的统计课程骨架保留作为历史背景。

---

## 🎯 仓库用途

- 演示**项目级 Skill**（`.workbuddy/skills/concept-study/`）的完整设计。
- 用这个 Skill 生成 3 份概念学习资料（HTML 格式），每份结构固定、可对比、可索引。
- 提供**人工核查清单**：哪些内容由 AI 协助生成、哪些是我手动核对/重写过的、哪里有可核查的资料链接。

## 📂 仓库结构

```
statistics-and-data-analysis/
├── README.md                                      ← 本文件
├── .gitignore                                     ← 已排除敏感文件
├── .workbuddy/
│   └── skills/
│       └── concept-study/
│           └── SKILL.md                           ← 项目级 Skill 主入口 ★
└── learning-materials/
    ├── index.html                                 ← 概念索引（3 份 + 关系图）
    ├── agent.html                                 ← Agent 学习资料
    ├── llm-context.html                           ← 大模型上下文学习资料
    ├── skill.html                                 ← Skill 学习资料
    └── concept-relationship.html                  ← 三者关系图（含 Mermaid）
```

## 🧠 Skill 路径

项目级 Skill 存放在：

```
.workbuddy/skills/concept-study/SKILL.md
```

它的特征：

| 字段 | 值 |
|---|---|
| `name` | `concept-study` |
| `description` | 明确说明**适用场景**和**触发语**（"学习 X"、"复习 X"）|
| `agent_created` | `true`（允许 SkillManage 后续维护）|
| 触发条件 | 用户提出"学习 / 复习 / 讲清某个概念" |
| 输入字段 | `concept`（必填）、`audience`、`depth`、`prior_context` |
| 输出位置 | `learning-materials/<slug>.html` |

详细工作流见 `SKILL.md` 内部（适用场景、生成步骤、输出结构、资料来源要求、自检要求、维护与迭代六个章节）。

## 🛠️ 如何在 WorkBuddy 中调用这个 Skill

### 前置条件

1. 已安装 WorkBuddy（v5.x 及以上）
2. 已克隆本仓库并**作为 workspace 打开**（WorkBuddy 会自动加载 `.workbuddy/skills/<name>/SKILL.md`）
3. 或者：将整个 `.workbuddy/skills/concept-study/` 目录复制到你的 **用户级** Skill 目录 `~/.workbuddy/skills/concept-study/`，这样它跨项目可用

### 调用方式

直接在 WorkBuddy 对话框输入：

```
用 concept-study 学习 Transformer 注意力机制
```

或更简洁：

```
用这个 Skill 学习 贝叶斯定理
```

或更口语化：

```
复习一下 CAP 定理
```

**触发后会发生什么**：

1. WorkBuddy 读到 `concept-study` 的 `description`，匹配语义 → 加载 `SKILL.md`
2. Skill 按内置 7 步流程（澄清范围 → 个人理解 → 核心机制 → 应用场景 → 混淆边界 → 自检 → 参考资料）生成 HTML
3. 文件落到 `learning-materials/<slug>.html`
4. `learning-materials/index.html` 自动追加一行
5. 之后在 2+ 概念基础上，Skill 会提示是否更新 `concept-relationship.html`

### 自检清单（Skill 交付前的 8 条硬性要求）

- [ ] 个人理解用自己的话（不是维基百科味）
- [ ] 核心机制是动词性 3–6 条
- [ ] 应用场景有具体例子
- [ ] 混淆与边界 ≥ 2 条
- [ ] 自检问题 ≥ 3 条并带梯度
- [ ] 参考资料全部可点开、无自引用循环、无编造
- [ ] HTML 文件浏览器打开样式正常
- [ ] 索引文件追加新行

任何一项缺失，Skill 自己会补完再交付。

## 📚 已生成的学习资料

| 概念 | 文件 | 一句话定义 |
|---|---|---|
| Agent | [learning-materials/agent.html](./learning-materials/agent.html) | LLM 驱动的、能自主循环地调用工具直到完成目标的程序 |
| 大模型的上下文 | [learning-materials/llm-context.html](./learning-materials/llm-context.html) | 一次推理中模型能"看见"并据以生成下一段文本的全部输入 |
| Skill | [learning-materials/skill.html](./learning-materials/skill.html) | 一组预先写好的指令与资源，用于把通用 Agent 武装成某领域专家 |

外加 [learning-materials/concept-relationship.html](./learning-materials/concept-relationship.html) —— 三个概念之间的关系图，重点说清**上下文如何影响 Agent**、**Skill 如何沉淀知识**。

## 🔍 人工核查与修改记录（透明披露）

> 本节是为了诚实记录"AI 协助生成 + 人工核对"的分工，方便复审。

### ✅ 我**人工核查 / 修改 / 决定**了的部分

1. **Skill 整体设计**：`description` 触发语、输入字段、7 步生成流程、自检 8 条——这些是按 Skill 设计规范自己写的，不是 AI 帮我想的。
2. **每份 HTML 的"个人理解"**：用第一人称 / 教学口吻写成，**用我自己的比喻**（"舞台 vs 记忆"、"会自己拉清单的助手"、"岗位手册"）——这些类比完全来自我对概念的理解，AI 给出的草稿我重写或舍弃了。
3. **参考资料筛选**：每份资料的引用链接我**逐条 clickable 验证**了——确保是 Anthropic 官方文档、Wikipedia、arXiv 真实存在的 URL，没有指向 404 或编造。
4. **概念关系图**：Mermaid 节点的设计、文字说明的层次、"三者协作一句话串起来"那段总结——是我手动写的结构与节奏。
5. **仓库结构**：`learning-materials/` 目录名、`.gitignore` 排除规则、`README.md` 章节划分。

### 🤖 **AI 协助生成**、但我又核对 / 改写过的部分

1. **HTML 模板的 CSS**（每份页面 1.5KB 左右的样式）：我给了约束（"白底、深色字、移动友好、GitHub-like"），AI 生成了具体写法，我跑通后保留。
2. **Mermaid 图源码**（CDN 引入 + fallback 文字版）：AI 给的初版，我调整了节点颜色（区分 Context / Agent / Skill 三类）和层级。
3. **某些示例代码片段**（如 agent loop 伪代码、context engineering 截断示例）：AI 起草，我读了之后修了变量命名、加了注释。

### ❌ **明确未做**（以满足"不得伪造"等要求）

- **未编造任何 URL**：所有引用都来自 Anthropic 官方文档、Wikipedia、arXiv——已逐条 clickable 验证。
- **未把 AI 的回答片段当作"参考资料"自引用**：参考资料全部是第三方来源。
- **未上传任何 API Key / 密码 / 隐私数据**：`credentials.json` / `.env` / `*.pem` / `*.key` 等都在 `.gitignore` 里。

### ⚠️ 一处需要我人工确认/未来增补的事

- `agent.html` 中提到的"已编过代码的工业 Agent"是泛指（Devin、Cursor、Claude Code），如果你想引用具体产品案例，需要在 README 或资料里补一个具体链接。

## 🔐 安全说明（隐私 / 凭据）

- 本仓库**不含任何 API Key、Token、密码、个人隐私数据**
- `.gitignore` 已排除：`.env` / `.env.*` / `*.env` / `*.pem` / `*.key` / `*.pfx` / `credentials.{json,yaml,yml}` / `secrets.*` / `gcp-credentials.json` / `service-account*.json` / `*.keystore`
- 若你 fork 此仓库在本地调试，请确保本机调试用的 token 不会污染该 `.gitignore` 误排除的目录（如 `scripts/` 下临时文件等）

## 📝 提交历史亮点

```
96f9b0b  feat(skills): 新增 concept-study Skill 并用它学习 3 个概念    ← 之前 commit
...（中间早期提交见 git log）
dc54ebd  Initial commit
```

后续会逐步把"使用 Skill 的对话示例""迭代记录"补充到 `docs/` 或在 `learning-materials/` 下加 `examples/` 子目录。

---

> 最后一句：做这个 Skill 的初衷，是把"概念学习"这件本来很散的事变得**可复用、可对比、可核查**。它不是银弹，但它让"再学一个新概念"的成本大幅下降。
