# Anti-Leakage Protocol — 知识隔离协议

---

## 目的

当用户提供全面的研究材料（RQ Brief、Synthesis Report、Annotated Bibliography、实验数据）时，写作 agent 应**主要基于这些材料**构建论文，而非 LLM 的参数记忆。防止：

1. **方法论编造（Failure Mode 6）**：LLM 用训练数据写出看似合理的方法部分，而非用户实际程序
2. **隐式知识泄漏**：LLM 用记忆内容填补缺口，可能不准确、过时或来自不同情境
3. **无意抄袭**：LLM 从训练数据中复现近逐字段落

---

## 协议

### 何时激活

当**以下全部**为真时激活：
- 用户通过 pipeline handoff 提供了研究材料（RQ Brief + Synthesis Report + Annotated Bibliography）
- 论文处于 `full` 或 `revision` 模式（非 `plan` 或 `outline-only`）
- 材料是实质性的（非占位 stub）

### 何时不激活

不激活当：
- 用户处于 `plan` 或 `socratic` 模式（探索性 — 预期使用 LLM 知识）
- 材料极少（如仅有 RQ Brief 无 bibliography）
- 用户明确要求 LLM 用自身知识补充

### Prompt Insertion

激活时，在 draft writer 的工作上下文前插入：

```
## Knowledge Isolation Directive

You are writing this paper based on the research materials provided in this session:
- RQ Brief, Synthesis Report, and Annotated Bibliography (from upstream research)
- Any additional materials the user has provided (experimental logs, datasets, prior drafts)

Priority rules:
1. PREFER session materials over your parametric knowledge for all factual claims
2. Every claim in the paper MUST be traceable to a source in the Annotated Bibliography or user-provided data
3. If the materials do not cover a topic the outline requires, flag it as [MATERIAL GAP] rather than filling from memory
4. Do NOT introduce references not present in the Annotated Bibliography unless explicitly asked by the user
5. The Methods section must describe ONLY what is documented in the user's materials — do not infer or interpolate experimental procedures

This is NOT a prohibition on using language skills or academic writing knowledge.
You may use your knowledge of academic conventions, writing style, logical argumentation,
and discipline norms. The restriction applies only to FACTUAL CONTENT — claims, citations,
data, and methodology descriptions must come from session materials.
```

### [MATERIAL GAP] 处理

当标记 `[MATERIAL GAP]` 时：
1. 缺口在下一个检查点 surface
2. 用户可提供额外材料，或授权 LLM 针对该特定缺口进行补充
3. 若补充：缺口部分在草稿元数据中标记 `[LLM-SUPPLEMENTED]` 供完整性审查

---

## 与现有检查的关系

| 检查 | 它捕捉什幺 | 知识隔离补充什幺 |
|-------|----------------|-------------------|
| Integrity gate | 事后编造引用 | 在写作时防止编造 |
| Failure Mode 6 | 方法与实际程序不匹配 | 防止 LLM 发明程序 |
| Writing Quality Check | AI 典型措辞模式 | 知识隔离防止 AI 典型*内容*（而非风格） |
