# Revision Tracking Template

> 用于 revision mode 记录修改轨迹，便于用户和评审者追踪变更。

---

```markdown
# Revision Tracking Log

**Paper Title**: [标题]
**Revision Round**: [R1 / R2]
**Date**: [日期]
**Author**: [作者]

---

## Summary of Changes

[1 段概述本轮修改的主要方向和范围。]

---

## Detailed Change Log

### Change #[N]

| Field | Content |
|-------|---------|
| **Source** | [Reviewer 1 / Reviewer 2 / Reviewer 3 / DA / Self-initiated] |
| **Original Comment** | [评审意见的逐字引用或摘要] |
| **Location** | [章节 / 段落 / 行号] |
| **Change Type** | [Addition / Deletion / Rewrite / Reorganization] |
| **Severity** | [Critical / Major / Minor / Suggested] |
| **Status** | [Completed / Partial / Declined with rationale] |

**Before**:
```
[修改前的原文]
```

**After**:
```
[修改后的文本]
```

**Rationale**: [若为 declined，解释为何不修改；若为 completed，简述修改理由]

---

### Change #[N+1]

[同上格式...]

---

## Statistics

| Category | Count |
|----------|-------|
| Total reviewer comments | [N] |
| Fully addressed | [N] |
| Partially addressed | [N] |
| Declined with rationale | [N] |
| Self-initiated changes | [N] |
| Critical issues resolved | [N] / [N] |
| Major issues resolved | [N] / [N] |
| Minor issues resolved | [N] / [N] |

---

## Acknowledged Limitations (Unresolved)

[本轮修订中无法合理解决的问题，以及为何它们被接受为局限性。]

1. **[Limitation]**: [描述] — **Rationale**: [为何无法在当前修订中解决]
2. ...

---

## Cross-Reference to Reviewer Comments

| Reviewer Comment ID | Change ID | Status |
|--------------------|-----------|--------|
| R1-C1 | Change #1 | Completed |
| R1-C2 | Change #2 | Declined |
| ... | ... | ... |
```

---

## 使用说明

1. **逐条映射**：每个评审意见都映射到一个 Change entry，不遗漏
2. **保留原文**：Before/After 对比让修改透明可追溯
3. **诚实记录**：Declined 的修改也要有充分理由，不可隐瞒
4. **统计汇总**：让编辑快速了解修订覆盖度
5. **Acknowledged Limitations**：诚实承认无法解决的关切，展示学术诚信
