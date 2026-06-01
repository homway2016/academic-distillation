# Calibration Mode Protocol — 评审者误差档案校准

## 目的

测量评审者自身的**假阴性率（FNR）**、**假阳性率（FPR）**和**平衡准确率**，使用户在依赖 rubric 分数前了解评审者的误差档案。

> 核心洞察：绝对分数本身难以解释。两篇都得 65 的论文，一个评审者可能系统性地给方法论薄弱论文打高分，另一个可能系统性地给跨学科论文打低分。校准模式让误差**可见**。

---

## 输入

1. **Gold-standard set**：5–20 篇用户已标注已知结局的论文
   - 每篇：论文文件 + ground-truth label（`accept` / `reject` / `borderline`）+ venue context
   - 最少 5 篇；推荐 10–15 篇
   - 必须同时包含至少 1 篇 `accept` 和 1 篇 `reject`，否则 FNR 或 FPR 无定义
2. **Domain specification**：目标领域（误差档案是领域特定的）
3. **Session-only persistence**：误差档案仅缓存于**当前 session**，不跨 session 存储

---

## 流程

### Phase 0: Intake

- 验证集合同时包含 `accept` 和 `reject`
- 若 n < 10，警告："校准样本少，结果应视为方向性而非结论性"
- 若所有标签同侧，拒绝继续并要求反例

### Phase 1: 逐篇运行 `full` 模式 + 集成

对每篇 gold paper：
- 运行标准 `full` 评审流程 **5 次**（5× ensemble），每次使用**新鲜上下文**防止 session 内偏误
- 聚合：
  - 每维度 median rubric score（均值易受单次离群值影响）
  - 5 次运行方差（稳定性指标）
  - Editorial decision（5 次多数投票）

**跨模型验证**：校准模式下默认开启。5 轮中至少 1 轮应使用不同模型家族。若未配置，发出警告并全部使用主模型。

### Phase 2: 构建混淆矩阵

将评审者多数投票决策与用户 ground truth 对比：

- `borderline`  ground truth 不进入二分类矩阵，但单独报告
- 映射：`Accept` / `Minor Revision` → positive；`Major Revision` / `Reject` → negative

| 指标 | 公式 | 报告方式 |
|------|------|---------|
| Balanced accuracy | (TPR + TNR) / 2 | 95% CI（bootstrap 1000 次） |
| FNR（漏报率） | FN / (FN + TP) | 同上 |
| FPR（误报率） | FP / (FP + TN) | 同上 |
| AUC | ROC over rubric-score threshold | 同上 |
| Calibration error | Mean \|rubric_score – ground_truth_severity\| | 按维度 |

### Phase 3: Borderline 处理

Borderline 论文不进入二分类矩阵，但用于 rubric-score 校准：
- 评审者的 rubric score
- 评审者的决策
- 是否正确落入 Major Revision（而非自信地 Accept 或 Reject）

若评审者对 borderline 论文自信地 Accept 或 Reject → "信心校准错误"问题。

### Phase 4: 产出 Calibration Report

```markdown
# Calibration Report
Domain: <domain>
Gold set: n=<N> (accept=<a>, reject=<r>, borderline=<b>)
Runs per paper: 5 (ensembled)
Cross-model: <yes/no>

## Summary Metrics
- Balanced accuracy: 0.XX [95% CI: 0.XX – 0.XX]
- FNR: 0.XX [95% CI ...]
- FPR: 0.XX [95% CI ...]
- AUC: 0.XX
- Ensemble stability: <mean std of rubric scores across runs>

## Per-Dimension Calibration Error
<table of 7 dimensions>

## Systematic Biases Detected
<narrative, e.g.
 "Reviewer tends to over-score originality on cross-disciplinary papers"
 "Reviewer under-scores qualitative methodology by ~8 points"
>

## Recommendations for Session Use
- 将 rubric scores 视为有 ±X 点校准误差
- Accept/Reject 决策中，评审者漏掉 X% 应拒案例（FNR）
- 边界决策建议升级至人类判断
```

### Phase 5: Session 附加

Calibration Report 附加到同 session 的后续评审，作为**置信披露头**：

```markdown
> **Reviewer Confidence Disclosure**
> This reviewer has measured balanced accuracy 0.XX, FNR 0.XX, FPR 0.XX
> on a gold set of <N> papers in <domain>. Rubric scores carry calibration
> error ±X points. Treat borderline decisions with human judgement.
```

此披露**不可隐藏**——校准的目的就是让误差档案可见。

---

## 集成方法说明

- **Median 而非 mean**：均值易受单次离群跑分影响；median 稳健
- **Fresh context per run**：防止单次误读的级联错误
- 用户可减少至 3 轮（token 预算考量），但**不允许 1 或 2 轮**（ensemble 无意义）

---

## 此模式不能修复的问题

- 不预测**领域外**论文的表现
- 不检测单篇论文内的 frame-lock（那是 DA 的职责）
- 不替换 `re-review` 模式的修订验证
- 若 gold set 本身有偏（如全部来自同一实验室），则报告的是有偏档案

---

## 搜索策略

使用 **Tavily MCP** 检索 gold paper 的已知结局背景、venue 标准、领域共识，辅助判断 ground truth 合理性。
