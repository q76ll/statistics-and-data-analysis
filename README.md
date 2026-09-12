# 📘 概念学习资料仓库（concept-learning-generator）

一个演示 **「个人概念学习 Skill + 结构化学习资料」** 的 GitHub 仓库。

仓库的核心是一个**项目级 Skill**：`concept-learning-generator`。它接收任意一个概念名，先检索权威来源，再按统一的 9 个板块生成一份可离线打开的 HTML 学习资料（也支持 Markdown）。

> 仓库名沿用了早先的 `statistics-and-data-analysis`，当前内容已聚焦于"概念学习 Skill 演示"。早期的课程目录骨架（`notes/` `code/` `data/` `assignments/`）保留作为历史记录。

---

## 🎯 仓库用途

1. **演示项目级 Skill 的完整设计**——从触发判断、输入字段、生成步骤到自检清单，全部写在 `.workbuddy/skills/concept-learning-generator/SKILL.md` 里，可直接阅读、复用。
2. **沉淀结构化学习资料**——已用这个 Skill 生成 3 份概念资料（Agent / 大模型的上下文 / Skill），每份结构一致、可横向对比。
3. **透明披露人工核查过程**——哪些是 AI 协助生成的、哪些经过人工核对与改写、哪些明确没做，都在本文档下方如实记录。

---

## 📂 仓库结构

```
statistics-and-data-analysis/
├── README.md                                        ← 本文件
├── .gitignore                                       ← 已排除敏感文件
├── .workbuddy/
│   └── skills/
│       └── concept-learning-generator/
│           └── SKILL.md                             ← 项目级 Skill 主入口 ★
└── learning-materials/
    ├── index.html                                   ← 资料索引
    ├── agent.html                                   ← 概念资料：Agent
    ├── llm-context.html                             ← 概念资料：大模型的上下文
    ├── skill.html                                   ← 概念资料：Skill
    ├── concept-relationship.html                    ← 三者关系说明（HTML，含 Mermaid）
    └── concept-relationship.md                      ← 三者关系说明（Markdown）
```

---

## 🧠 Skill 的存放路径

```
.workbuddy/skills/concept-learning-generator/SKILL.md
```

这是**项目级 Skill**：它随仓库一起提交、共享，任何人在 WorkBuddy 中打开本仓库都会被自动加载。

SKILL.md 的顶部是 YAML 元数据：

```yaml
---
name: concept-learning-generator
description: 当用户给出一个名词/概念/术语（如 Agent、大模型的上下文、Skill、RAG、CAP 定理），
  且期待一份完整的「学习资料」而非一句话答案时，使用本 Skill。典型触发语：用
  concept-learning-generator 学习 X、帮我生成 X 的学习资料、我想搞懂 X……不适用于：
  工具用法问答、代码调试、文件格式转换、纯事实性一句话查询。
agent_created: true
---
```

正文包含以下章节（与作业要求的五类说明一一对应）：

| 作业要求 | SKILL.md 中的位置 |
|---|---|
| 适用场景 | 第一节「触发判断」——用"应该触发 / 不应触发"对照表划定边界 |
| 输入信息 | 第二节「输入信息 (Input)」——5 个字段的表格，含必填/默认值/说明，缺省项须标注"假设" |
| 生成步骤 | 第三节「生成步骤 (Procedure)」——Step 1–5：检索 → 组织 → 个人解释 → 生成文件 → 自检 |
| 输出结构 | 第四节「输出结构」——9 个必备板块 + 可视化讲解规则 + 自测题出题规范 |
| 资料来源要求 | 第五节「资料来源要求」——禁止伪造、可核查、主来源优先官方、标注引用、区分事实与观点 |
| 自检要求 | 第六节「自检要求」——10 条交付前清单 |

**它不是一次性提示词**：SKILL.md 第八节明确写了"面向任意概念，不要把它写成只服务于 Agent / 上下文 / Skill 的一次性提示词；新增概念时只需提供概念名，重复 Step 1–5 即可"。

---

## 🛠️ 如何在 WorkBuddy 中调用这个 Skill

### 前置条件

1. 已安装 WorkBuddy（v5.x 及以上）。
2. 已克隆本仓库，并**以本仓库目录作为 workspace 打开**——WorkBuddy 会自动加载 `.workbuddy/skills/<name>/SKILL.md`。
3. 或者：把 `.workbuddy/skills/concept-learning-generator/` 整个目录复制到用户级目录 `~/.workbuddy/skills/` 下，这样它跨项目可用。

### 调用方式

直接在对话框输入即可（以下任一句都能触发）：

```
用 concept-learning-generator 学习一下 CAP 定理，做成 HTML 放到 learning-materials/cap-theorem.html
```

```
帮我生成 贝叶斯定理 的学习资料，视角是面试复习，输出中文 HTML
```

```
我想搞懂 RAG 在 AI Agent 里是什么，给我一份带来源的学习卡片
```

```
用 concept-learning-generator 学习 Transformer 注意力机制，输出 md
```

### 触发后会发生什么

1. WorkBuddy 读取 Skill 的 `description`，语义匹配成功后加载 SKILL.md 正文。
2. 按 **Step 1** 先做 `WebSearch` 检索权威来源，必要时用 `WebFetch` 验证链接有效性。
3. 按 9 个板块组织内容（Step 2），"个人解释"用第一人称撰写（Step 3）。
4. 生成独立 HTML（内联 CSS，可双击打开），可视化部分按需选用纯 HTML/CSS 或 Mermaid（Step 4）。
5. 过一遍自检清单（Step 5），不通过则修正后再交付。
6. 产出落到 `learning-materials/<slug>.html`，并在 `index.html` 中追加一行。

---

## 📚 已生成的学习资料

| # | 概念 | 文件 | 一句话定义 |
|---|---|---|---|
| 01 | Agent（智能体） | [agent.html](./learning-materials/agent.html) | 由大模型驱动、能在循环中自主使用工具直到完成目标的程序 |
| 02 | 大模型的上下文 | [llm-context.html](./learning-materials/llm-context.html) | 一次推理中模型能看见并据以生成文本的全部输入，受窗口上限约束 |
| 03 | Skill（技能） | [skill.html](./learning-materials/skill.html) | 一份打包好的领域工作手册，以渐进式披露的方式按需加载 |

**关系说明**：[concept-relationship.html](./learning-materials/concept-relationship.html) / [concept-relationship.md](./learning-materials/concept-relationship.md)
—— 说明三者不在同一层，重点回答两个问题：**上下文如何影响 Agent 的工作**，**Skill 如何沉淀可复用的任务知识**。

每份资料都包含 9 个板块：学习目标 / 核心问题 / 个人解释 / 核心机制 / **可视化讲解** / 应用场景 / 易混淆与边界 / 自测问题 / 参考来源。

### 可视化讲解的两种实现

| 实现方式 | 用在哪 | 是否离线可用 |
|---|---|---|
| 纯 HTML + CSS（堆叠条、卡片、网格） | agent.html、llm-context.html、skill.html 的全部图 | ✅ 是，双击即可看 |
| 内联 SVG（注意力衰减曲线） | llm-context.html 图 2 | ✅ 是 |
| Mermaid（CDN 加载） | concept-relationship.html 图 1 | ⚠️ 需联网；已附纯文字兜底，离线可读 |

所有图都配有 `viz-caption` 图说；依赖 Mermaid 的图额外附了一段纯文字说明，保证离线或 CDN 失效时读者仍能理解图意。图中出现的数值均为**示意**并已显式标注。

---

## 🔍 人工核查与修改记录

> 本节如实记录"AI 协助生成 + 人工核对"的分工，便于复审。

### ✅ 我人工核查 / 修改 / 决定的部分

1. **Skill 的整体设计**——触发判断的边界表、5 个输入字段的取舍、Step 1–5 的流程、"9 个板块"的输出结构、10 条自检清单，均参照给定的设计模板逐项落实并核对，不是让 AI 自由发挥的产物。
2. **每份资料的"个人解释"**——第一人称的类比是我自己定的：Agent 用"会自己拉清单的助手"、上下文用"没有记忆的演员与有限的舞台"、Skill 用"给新同事的岗位手册"。资料中已用 `🔍 待人工复核` 标出建议再改写的段落。
3. **参考资料逐条核验**——所有链接都指向 Anthropic 官方博客/文档、Claude Academy、arXiv、OpenAI GitHub 等真实页面，未使用任何编造的 URL、论文编号或作者名。对不确定的链接用工具实际访问验证过。
4. **可视化选型**——哪一处"值得画图"、用什么图表达（循环图 / 堆叠条 / 曲线 / 关系图），按"结构、流程、对比、定量"的维度逐个判断；文字能讲清的地方没有硬凑图。
5. **自测题的设计**——题型组合（简答 + 选择 + 应用）与四维度覆盖（概念辨析 / 核心机制 / 应用场景 / 风险边界）按规范逐题检查过，答案统一放进 `<details>` 折叠区。

### 🤖 AI 协助生成、经我核对后保留的部分

1. **HTML 的结构与 CSS 写法**——我给出约束（内联样式、浅色主题、卡片式分区、中文排版、移动端可读），具体 CSS 由 AI 起草，我检查渲染效果后保留。
2. **Mermaid 图的节点与连线**——AI 给出初版，我调整了节点分组与配色（上下文/Agent/Skill 三类分色），并补充了文字兜底。
3. **部分示例代码片段**（agent loop 伪代码、层级摘要伪代码）——AI 起草，我读过之后调整了表述并确认逻辑无误。

### ❌ 明确未做的部分

- **未编造任何引用**：所有来源均为真实可点击的官方文档、课程、论文或官方仓库。
- **未整段照搬 AI 对话**：各板块均为重新组织后的表述；正式概念定义处标注了 `[来源 N]` 以便回溯。
- **未上传任何敏感信息**：仓库内不含 API Key、Token、密码或个人隐私；`.gitignore` 已排除相关文件类型。

### ⚠️ 待补充 / 需人工确认

- `agent.html` 的应用场景中使用的是通用工程示例，未引用具体商业产品的官方材料；如需举例特定产品，需补充相应来源链接。
- `llm-context.html` 图 2 的曲线形态来自对 "lost in the middle" 现象的文字描述，属**示意**而非从论文中摘取的原始数据点；若需要精确数据，应从原文图中取样并注明页码。

---

## 🔐 版本与安全

- **全部作业内容已提交并推送到 GitHub**：见下方提交历史。
- **本仓库不含任何 API Key、密码、个人隐私信息**。
- `.gitignore` 已排除以下敏感文件类型：

```
.env  .env.*  *.env
*.pem  *.key  *.pfx  *.keystore
credentials.json  credentials.yaml  credentials.yml
secrets.*
gcp-credentials.json  service-account*.json
```

---

## 📝 提交历史

```
87e83ba  feat(skills): 升级 concept-study Skill 并切换到 HTML 学习资料
96f9b0b  feat(skills): 新增 concept-study Skill 并用它学习 3 个概念
6e4d5c9  docs: 完善课程 README 与添加 .gitignore
8aa9af1  docs: 添加 assignments 目录说明
8f7b9d7  docs: 添加 data 目录说明
cb2f123  docs: 添加 code 目录说明
1f04d15  docs: 添加 notes 目录说明
5a237e7  docs: 添加第一篇学习笔记 - 描述统计
6bb8752  docs: 更新仓库结构与学习记录
24e3756  chore: 添加 .gitignore
26aebe4  docs: 完善课程学习笔记 README
dc54ebd  Initial commit
```

---

> 做这个 Skill 的初衷：把"学一个概念"这件本来很散的事，变得**可复用、可对比、可核查**。它不是银弹，但它让"再学一个新概念"的成本明显下降。
