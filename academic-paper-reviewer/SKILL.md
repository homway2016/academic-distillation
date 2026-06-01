# Academic Paper Reviewer — Distilled Core Methodology

> 剥离外部文献检索与 API 依赖，保留多视角同行评审的核心方法论与协议。
> 所有需要外部搜索的位置，统一替换为 Tavily MCP。

---

## 1. 概述

模拟真实国际期刊同行评审流程：自动识别论文领域，动态配置 **5 位独立评审者**（主编 + 3 位同行 + 魔鬼代言人），从四个互不重叠的视角产出评审意见，最终合成**编辑决策信**与**修订路线图**。

### 1.1 工具策略

| 操作 | 策略 |
|------|------|
| `Read` | 读取用户上传的论文文件（PDF / DOCX / Markdown） |
| `Write` | 输出评审报告、编辑决策信、修订路线图 |
| `Spawn Agent` | 保留多 Agent 并行评审架构（5 位评审者独立运行） |
| 外部搜索 | 统一使用 **Tavily MCP** 验证引用、补充领域背景（原 WebSearch 全部替换） |

---

## 2. 评审团队（5 人面板）

| 角色 | 职责 | 视角 |
|------|------|------|
| **EIC** | 期刊适配、原创性、整体质量 | 主编视角 |
| **Methodology Reviewer (R1)** | 研究设计、统计效度、可复现性 | 方法论视角 |
| **Domain Reviewer (R2)** | 文献覆盖、理论框架、领域贡献 | 领域专家视角 |
| **Perspective Reviewer (R3)** | 跨学科连接、实践影响、基础假设挑战 | 跨学科视角 |
| **Devil's Advocate (DA)** | 核心论点挑战、逻辑谬误检测、最强反驳 | 对抗视角 |

> **铁律**：5 位评审者**独立评审**，禁止交叉引用彼此报告。综合者禁止编造评审意见。

---

## 3. 六种运作模式

| 模式 | 触发场景 | 面板规模 | 输出 |
|------|---------|---------|------|
| `full` | 投稿前综合评审（默认） | 5 人 | 5 份评审报告 + 编辑决策 + 修订路线图 |
| `quick` | 15 分钟快速质量评估 | EIC 单独 | 主编快速评估 + 关键问题清单 |
| `methodology-focus` | 仅检查方法/统计 | EIC + R1 | 深度方法论评审报告 |
| `guided` | 引导式改进（苏格拉底对话） | 5 人 + 对话 | 渐进揭示问题，最终输出路线图 |
| `re-review` | 再审验收（验证修订是否到位） | EIC + 综合者 | 修订追溯矩阵 + 残余问题 + 新决策 |
| `calibration` | 校准评审者误差档案 | 5 人 × 5 轮 | FNR / FPR / 平衡准确率报告 |

---

## 4. 三阶段评审流程

```
Phase 0: 领域分析与评审者配置
    └─ 读取论文 → 识别学科/方法/目标期刊层级 → 生成 5 位评审者身份卡
    └─ 用户可调整身份卡后再进入 Phase 1

Phase 1: 并行多视角评审（5 人独立）
    ├─ EIC        → EIC Review Report
    ├─ R1         → Methodology Review Report
    ├─ R2         → Domain Review Report
    ├─ R3         → Perspective Review Report
    └─ DA         → Devil's Advocate Stress-Test Report

Phase 2: 编辑综合与决策
    └─ 综合者读取 5 份报告 → 识别共识 vs 分歧 → 仲裁争议
    └─ 输出：编辑决策信 + 修订路线图（可直接输入 revision 模式）
```

### 4.1 Phase 2.5: 修订教练（仅当 Decision ≠ Accept）

EIC 通过苏格拉底对话引导作者：
1. 整体定位 — "读完评审意见后，最让你惊讶的是哪一点？"
2. 核心问题聚焦 — 引导理解共识性问题
3. 修订策略 — "如果只能改三处，你会选哪三处？"
4. 反驳回应 — 引导思考如何回应 DA 的挑战
5. 执行规划 — 帮助优先级排序

用户可随时说 "just fix it" 跳过对话。

---

## 5. 七维评审量表（0–100）

| 维度 | 权重 | 核心问题 |
|------|------|---------|
| Originality（原创性） | 20% | 增量贡献还是范式突破？ |
| Methodological Rigor（方法严谨性） | 25% | 设计、效度、统计、可复现性 |
| Evidence Sufficiency（证据充分性） | 25% | 来源质量、数量、三角验证 |
| Argument Coherence（论证连贯性） | 15% | 逻辑链是否完整、有无跳跃 |
| Writing Quality（写作质量） | 15% | 术语精度、段落结构、学术规范 |
| Literature Integration（文献整合）* | 报告用 | 覆盖度、定位精度、理论谱系 |
| Significance & Impact（意义与影响）* | 报告用 | 实践/理论意义、受众范围 |

**决策阈值**：
- ≥ 80：Accept
- 65–79：Minor Revision
- 50–64：Major Revision
- < 50：Reject

> 详见 `references/quality_rubrics.md` 完整量表 + `references/review_criteria_framework.md` 分类型标准。

---

## 6. 核心协议索引

| 协议 | 文件 | 用途 |
|------|------|------|
| **七维评审框架** | `references/review_criteria_framework.md` | 通用 + 分类型（实证/理论/综述/案例/政策） |
| **质量量表** | `references/quality_rubrics.md` | 0–100 评分细则 + 权重 |
| **编辑决策标准** | `references/editorial_decision_standards.md` | Accept / Minor / Major / Reject 决策矩阵 |
| **魔鬼代言人协议** | `references/devils_advocate_protocol.md` | 8 维挑战 + 让步门槛 + 攻击强度保持 |
| **再审验收协议** | `references/re_review_mode_protocol.md` | R&R 追溯矩阵 + Commitment 验证 |
| **校准模式协议** | `references/calibration_mode_protocol.md` | FNR/FPR / 5× Ensemble / 置信披露 |
| **引导式评审协议** | `references/guided_mode_protocol.md` | 渐进揭示对话流程 |
| **评审质量思维** | `references/review_quality_thinking.md` | 三镜头框架（内部效度/外部效度/贡献） |
| **统计报告标准** | `references/statistical_reporting_standards.md` | APA 7.0 + 红旗清单 + 方法专用检查表 |

---

## 7. 铁律与反模式

### 7.1 六大铁律

1. **独立评审**：5 位评审者互不引用彼此报告。
2. **禁止编造**：综合者只能基于 Phase 1 报告合成，禁止虚构评审意见。
3. **DA CRITICAL 不可忽略**：若魔鬼代言人发现 CRITICAL 问题，编辑决策不能是 Accept。
4. **再审必须验证**：re-review 不可盖章通过，必须逐条独立核实修订手稿。
5. **只读约束**：评审者禁止修改原稿，只能产出独立报告。
6. **具体可执行**：每条批评必须包含"什幺问题、在哪里、怎幺改"。

### 7.2 常见反模式

| 反模式 | 后果 | 正确做法 |
|--------|------|---------|
| 评分马屁精（Sycophantic Inflation） | 给平庸论文打高分回避冲突 | 分数必须有证据支撑；方法有漏洞则严谨性 ≤ 6 |
| 重复批评 | R1/R2/R3 提出相同观点 = 虚假多样性 | 每位评审者角度必须不同 |
| 笼统反馈 | "方法可以更强" | 必须具体到章节/段落/数据 |
| 忽视 DA | DA 发现 CRITICAL 但决策仍是 Accept | 严格执行铁律 #3 |
| 盖章式再审 | 不看手稿就写"已全部回应" | 逐条对照修订稿独立验证 |

---

## 8. 评审报告模板

- `templates/peer_review_report_template.md` — 单份评审报告结构
- `templates/editorial_decision_template.md` — 编辑决策信结构
- `templates/revision_response_template.md` — 作者修订回应模板（R→A→C 格式）

---

## 9. 跨模型验证（可选）

当启用 `ARS_CROSS_MODEL` 时，DA 在完成后可将论文（不带自身发现，防止锚定）发送至独立模型进行对抗评审。若发现新的 CRITICAL/MAJOR 问题，以 `[CROSS-MODEL-FINDING]` 标注并入报告。

搜索统一使用 **Tavily MCP** 完成：
- 验证引用真实性
- 补充领域背景
- 检索反驳证据（DA 使用）

---

## 可选 CLI 工具增强（`tools/`）

以下 Python 脚本为**纯 stdlib**，可作为评审流程的确定性补充：

| 工具 | 用途 | 对应评审阶段 |
|------|------|-------------|
| `tools/verify_papers.py` | 三层引用验证（arXiv → CrossRef → S2），捕获幻觉引用 | R1/R2 文献检查 |
| `tools/evidence_check.py` | 验证论文声明的数字/字符串是否存在于原始结果文件 | R1 方法论审计 |
| `tools/threat_scan.py` | 扫描上传文件是否包含 prompt injection | 任何文件上传前 |

**使用方式**：`python3 tools/<script>.py --help`

---

## 10. 快速路由

| 用户输入 | 路由 |
|---------|------|
| "Review this paper" / "评审这篇论文" | `full` |
| "Quick look" / "快速看一下" | `quick` |
| "Check methodology" / "检查方法" | `methodology-focus` |
| "Guide me to improve" / "帮我改进" | `guided` |
| "Verify revisions" / "验证修订" | `re-review` |
| "How accurate are your scores?" / "校准评审者" | `calibration` |
 