# Re-Review Mode Protocol — 再审验收与 R&R 追溯

## 目的

验证作者修订是否真正回应了首轮评审意见。核心机制是**独立验证**——不轻信作者的"已修改"声称，而是直接对照修订稿核实。

## 输入

1. 原始 Revision Roadmap（Stage 3 输出）
2. 修订后手稿
3. Response to Reviewers（可选但强烈建议）

---

## 验证逻辑

### 按优先级逐项检查

```
For each item in Revision Roadmap:

Priority 1 (Required):
  -> 检查修订稿中是否有对应修改
  -> 评估修订质量：FULLY_ADDRESSED / PARTIALLY_ADDRESSED / NOT_ADDRESSED / MADE_WORSE
  -> 所有 Priority 1 必须 FULLY_ADDRESSED 才能 Accept

Priority 2 (Suggested):
  -> 检查每项
  -> 至少 80% 应有回应
  -> NOT_ADDRESSED 项需要作者解释

Priority 3 (Nice to Fix):
  -> 检查但不影响决策
```

### 追溯规则（Traceability Rule）

对每项 Priority 1，评审者**必须**：

1. 读取 Response to Reviewers 中的作者声称
2. 导航到修订稿中声称的修改位置
3. **独立验证**声称与实际修改是否匹配
4. 若作者声称为空或模糊（如"按建议修改"），标记 Verified? 为 `🔍 Cannot verify`，并在 Quality Assessment 中标记

---

## Commitment 验证（Schema 11 行级）

对每条从 `revision_coach_agent` 提取的 `commitment`，验证其 `fulfillment_status`：

| 状态 | 含义 | 验证方式 |
|------|------|---------|
| `fulfilled` | 所需证据存在且实质回应 commitment | 按 `required_evidence_type` 在指定位置验证 |
| `partial` | 证据存在但未完全回应 | 例：在数据集Y上跑实验，但评审者要求的是数据集X |
| `not-fulfilled` | 所需证据缺失 | 若 `unfulfilled_rationale` 为空，标记 `COMMITMENT_GAP` |
| `explicitly-rejected-with-rationale` | 作者明确拒绝处理，但提供了理由 | 仍需 `unfulfilled_rationale` |

### Evidence Type 验证映射

- `new_section` / `new_figure` / `new_table` / `new_citation` / `methods_paragraph` / `discussion_paragraph` / `prose_edit` → 对照**修订稿**的 `revision_location`
- `acknowledgment_only` → 对照 **Response to Reviewers**（不要求手稿修改）
- `other` → 若 `revision_location` 为空，提示作者补充；若已填，在指定位置验证

**注意**：`residual_action` 非空与部分 `fulfilled` 不矛盾。`residual_action` 是 concern 级别（前瞻性），`fulfillment_status` 是 commitment 级别。

---

## 新问题检测

除检查旧项外，EIC 还需扫描：
- 修订新增内容是否引入新问题
- 新增引用是否正确（深度验证留给 Stage 4.5 诚信检查）
- 修订是否导致不一致

---

## 再审后苏格拉底指导

若 Re-Review Decision = Major Revision：

1. **缺口分析** — "首轮修订解决了多少问题？剩余的为何难处理？"
2. **根因诊断** — "是证据不足、论证不清，还是结构性问题？"
3. **权衡决策** — "哪些可以标记为研究局限性？"
4. **行动计划** — 为每个残余问题规划修订方法

最多 5 轮对话，用户可随时说 "just fix it" 跳过。

---

## 输出格式

```markdown
# Verification Review Report

## Decision
[Accept / Minor Revision / Major Revision]

## Revision Response Checklist

### Priority 1 — Required Revisions
| # | Original Comment | Author's Claim | Status | Location | Verified? | Quality Assessment |
|---|------------------|----------------|--------|----------|-----------|-------------------|
| R1 | [原文] | [作者声称] | FULLY_ADDRESSED | 第X节 | ✅ Yes | 充分回应 |
| R2 | [原文] | [作者声称] | PARTIALLY_ADDRESSED | 第Y节 | ⚠️ Partial | 部分回应，仍缺 [具体缺口] |

### Priority 2 — Suggested Revisions
| # | Original Comment | Status | Notes |
|---|------------------|--------|-------|
| S1 | [原文] | FULLY_ADDRESSED | -- |
| S2 | [原文] | NOT_ADDRESSED | 作者解释: [理由] |

### Priority 3 — Nice to Fix
| # | Original Comment | Status |
|---|------------------|--------|
| N1 | [原文] | FULLY_ADDRESSED |

## New Issues (Discovered During Revision)
| # | Type | Location | Description |
|---|------|----------|-------------|
| NEW-1 | [类型] | 第X节 | [描述] |

## Decision Rationale
[基于检查表的决策理由]

## Residual Issues (If Any)
[列出未解决项，建议标记为 Acknowledged Limitations]
```

---

## 反模式

| 反模式 | 后果 | 正确做法 |
|--------|------|---------|
| **盖章式再审** | 不看手稿就写"已全部回应" | 逐条对照修订稿独立验证 |
| **轻信作者声称** | 作者说"已补充"实际未改 | 必须亲自导航到修订位置核实 |
| **忽略 MADE_WORSE** | 修订反而把问题改得更糟 | 明确标记并升级严重度 |
| **遗漏新问题** | 只查旧项，不管新增缺陷 | 扫描修订内容的一致性 |
