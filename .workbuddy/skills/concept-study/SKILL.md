---
name: concept-study
description: 此 Skill 在用户希望"学习/复习/讲清/梳理 一个或一组概念"时触发。典型触发语句包括："用 Skill 学习 X"、"帮我搞懂 X"、"把 X 讲明白"、"帮我整理 X 的学习笔记"、"复习 X" 等。Skill 会按统一的结构化模板（定义 / 为何重要 / 关键特征 / 与相近概念对比 / 实例 / 常见误解 / 自检问题 / 下一步）生成中文 Markdown 学习笔记，落到 notes/concepts/<slug>.md，并维护索引文件。适用于计算机、AI、数学、工程等领域概念的入门到进阶复习场景。
agent_created: true
---

# Concept Study

## Overview

This skill enables structured concept learning. Given a concept name (and optionally context such as background or depth level), produce a Chinese Markdown learning note that moves the learner from confusion to "I can explain it in my own words and use it on a small problem".

## When to use this skill

Use this skill when:

- The user asks to "learn / review / understand / explain / organize notes for" a specific concept.
- The user gives a list of concepts (e.g. "study X, Y, Z") — handle each one in turn, then update the index.
- The user asks for a "概念学习资料"、"学习笔记"、"概念卡" style deliverable.

Do NOT use this skill when:

- The user wants ad-hoc Q&A about a concept (just answer in chat).
- The task is to write runnable code, build a feature, or perform an action (use a different skill).
- The user wants to translate or summarize an existing long document (that is summarization, not concept learning).

## Workflow

Follow these steps in order. Skip a step only when there is a clear reason.

### Step 1 — Capture inputs

Collect:

- **Concept name(s):** the Chinese or English term(s) the user wants to learn. If the name is ambiguous (e.g. "Skill" can mean many things), briefly clarify or pick the most likely interpretation and note the assumption.
- **Optional context:** the user's background, current course, depth level (intro / intermediate / advanced).
- **Optional constraints:** output language (default Chinese), output path (default `<repo>/notes/concepts/<slug>.md`), whether to also update `notes/concepts/index.md`.

If concept names are missing, ask. If context is missing, make reasonable defaults and proceed.

### Step 2 — For each concept, generate a structured note

Use the template in `references/concept_template.md`. Sections are mandatory unless the concept genuinely cannot fill them — in that case mark "N/A (原因)". Keep each section short (1–6 lines or 3–6 bullets). Total length ~ 300–700 words per concept.

The skill is content-led, not form-led: prioritize faithful explanation over squeezing every section. If a section would be filler, drop it.

Content quality rules:

1. **Definition:** one sentence. No circular definition ("X is when you X").
2. **Why it matters:** connect to something concrete the learner is doing or likely to face.
3. **Key characteristics:** 3–5 bullet points — properties, typical magnitudes, conditions.
4. **Comparison:** contrast with 1–3 similar concepts in a small table. This is where learners most often mix things up.
5. **Concrete example:** one short scenario, ideally from the learner's domain if known. Avoid trivial `x = 1` toy examples.
6. **Common misconceptions:** 2–4 misconceptions that real learners hold, with one-line corrections.
7. **Self-check questions:** 3–5 questions ranging from recall to application. The learner should answer them out loud or in writing, not in their head.
8. **Next steps:** 1–3 concrete next moves — read, do, or build something.

### Step 3 — Write files

For each concept:

- Slug: convert Chinese to pinyin or English (e.g. "大模型的上下文" → `llm-context`; "Agent" → `agent`; "Skill" → `skill`). If multiple reasonable slugs exist, pick the shortest unambiguous one.
- Path: `<repo>/notes/concepts/<slug>.md`.
- Frontmatter: include `title`, `concept`, `date`, `tags` (top 3–5 keywords).

Then update (or create) `<repo>/notes/concepts/index.md` with a table of all concepts seen in this batch:

```
| 概念 | slug | 一句话定义 | 标签 |
|---|---|---|---|
| Agent | `agent` | …… | AI, 自治 |
```

### Step 4 — Hand off

After writing, tell the user:

- The list of files created / updated (with absolute paths).
- Whether the index was updated.
- A short self-test suggestion (e.g. "回答 01-Agent.md 里的自检问题 1、3、5，30 分钟后合上文件复述").

## Resources

### references/concept_template.md

Full Markdown template for the per-concept note. Load it before generating each note; do not invent a new structure.

## Style

- Language: Simplified Chinese by default; English technical terms stay English (e.g. token, context window, agent loop).
- Tone: 像一个耐心的高级同学在讲题，不要居高临下，但也不要卖萌。
- No emojis unless the user uses them first.
- Citations: do not invent page numbers or paper titles. If the user needs them, ask.
- Code blocks: only when a 5-line snippet genuinely helps; otherwise prefer prose.
