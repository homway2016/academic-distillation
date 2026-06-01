# Mode Selection Guide — 模式选择指南

帮助用户选择最合适的运行模式。

---

## 模式选择流程图

```
User Input →
│
├── Already have complete research?
│   ├── Yes → Want a full paper?
│   │   ├── Yes ─────────────────────────→ full mode
│   │   └── No → Just need an outline?
│   │       ├── Yes ─────────────────────→ outline-only mode
│   │       └── No → Just need an abstract?
│   │           ├── Yes ──────────────────→ abstract-only mode
│   │           └── No → Just need a literature review?
│   │               ├── Yes ─────────────→ lit-review mode
│   │               └── No ──────────────→ full mode
│   │
│   └── No → Want guided thinking?
│       ├── Yes ─────────────────────────→ plan mode
│       └── No ──────────────────────────→ full mode
│
├── Have an existing paper to revise? ──────────────────────→ revision mode
├── Just need format conversion? ────────────────────────→ format-convert mode
└── Just need a citation check? ────────────────────────→ citation-check mode
```

---

## 各模式详细说明

### full mode — 完整论文写作

- **适用**：有明确研究问题和（部分）材料；需要从头到尾产出一篇完整论文
- **不适用**：没有研究方向（→ 先用 deep-research）；仅需某个特定部分
- **输出**：完整论文草稿 + 参考文献 + 双语摘要 + 评审报告
- **阶段**：全部 8 阶段

### plan mode — 苏格拉底式逐章引导规划 ★

- **适用**：有想法但不够清晰；想要逐章指导；第一次写论文；想先想清楚再动笔
- **不适用**：已经知道要写什幺（→ full 更快）；仅需大纲无深度思考
- **输出**：Chapter Plan + INSIGHT Collection
- **后续**：可转为 full mode 产出完整论文

### outline-only mode — 大纲生成

- **适用**：仅需论文结构和详细大纲；提交给导师审阅的提案
- **输出**：详细大纲 + 证据分配 + 字数分布
- **阶段**：Phase 0-2

### revision mode — 论文修改

- **适用**：已有完整草稿；收到评审意见需要修改；感觉某些部分需要改进
- **先决条件**：用户提供现有论文内容
- **输出**：修改后的论文 + 修改说明（跟踪更改）

### revision-coach mode — 修订教练

- **适用**：收到非结构化评审意见，需要解析为结构化修订路线图
- **输出**：分类、映射、优先排序的评审意见 + 修改建议
- **特点**：可独立运行，无需先前 pipeline 执行

### abstract-only mode — 摘要写作

- **适用**：论文已完成，仅需摘要；需要会议摘要；需要双语摘要
- **输出**：双语摘要（zh-CN + EN）+ 关键词

### lit-review mode — 文献综述

- **适用**：需要某个主题的文献综述；准备论文的文献综述章节
- **输出**：注释书目 + 文献矩阵 + 综合分析

### format-convert mode — 格式转换

- **适用**：已有论文内容，需要格式转换；Markdown → LaTeX / DOCX / PDF
- **输出**：目标格式的文档

### citation-check mode — 引用检查

- **适用**：已有论文，仅需检查引用格式；投稿前最终检查；切换引用格式
- **输出**：引用错误报告 + 自动修正建议

### disclosure mode — AI 使用披露

- **适用**：需要生成 venue-specific AI 使用披露声明
- **输出**：符合目标期刊/会议政策的披露段落 + 放置说明

---

## 常见误选场景

| 用户说 | 容易误选 | 正确选择 | 原因 |
|---------|---------|---------|------|
| "Help me write an outline" | outline-only | 先确认：要简单大纲还是深度规划？ | 可能需要 plan mode |
| "I want to write a paper but don't know how to start" | full | plan mode | 需要引导式思考 |
| "Help me revise my paper" | revision | 先确认：有评审意见吗？ | 可能需要 full mode 重写 |
| "Help me search for literature" | lit-review | 确认：是为论文还是为研究调查？ | 可能需要 deep-research |
| "I want to plan my paper step by step" | outline-only | plan mode | 需要交互式引导 |
| 「带我写论文」/「引导我写论文」 | full | plan mode | 需要苏格拉底式引导 |
| 「第一次写论文」/「论文新手」 | full | plan mode | 新手需要逐章引导 |

---

## 快速决策表

| 你有什幺？ | 你想要什幺？ | 选择模式 |
|-----------|-----------|------------|
| 什幺都没有 | 完整论文 | plan → full |
| 研究问题 + 文献 | 完整论文 | full |
| 研究问题 + 文献 | 大纲 | outline-only |
| 模糊想法 | 论文计划 | plan |
| 已完成论文 | 修改 | revision |
| 已完成论文 | 摘要 | abstract-only |
| 已完成论文 | 格式转换 | format-convert |
| 已完成论文 | 引用检查 | citation-check |

---

## Plan → Full 转换协议

Plan mode 完成后转为 full mode 的质量门槛：

- [ ] Chapter Plan 中每章至少有 1 个 argument sketch 评级为 `adequate` 或以上
- [ ] 整体结构映射到 `paper_structure_patterns.md` 中的已识别模式
- [ ] 至少识别 5 个潜在参考文献（作为 literature_strategist 的种子）
- [ ] 研究问题已最终确定（不再处于苏格拉底对话的演化中）

**转换时丢弃**：苏格拉底对话中的会话填充物、明确标记为 "maybe" 的暂定想法、plan mode 的迭代草稿（仅最终版本带入）
