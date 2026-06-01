# Writing Quality Check — 写作质量检查清单

## 目的

一套从 AI 生成文本的常见模式中提炼出的写作质量规则。这些规则**适用于所有文本**，无论是否由 AI 生成。目标是更好的散文，而非检测规避。

> **设计边界**：本清单改善写作质量。它不是 humanizer。我们不旨在欺骗 AI 检测器。我们旨在产出清晰、精确、多样的学术散文。

---

## A. 高频词汇警示

以下词汇在 AI 生成文本中出现比例过高。遇到时问自己：**"这真的是这里最精确的词汇，还是我在默认使用它？"**

| 词汇 | 为何被标记 | 更好的替代（视语境） |
|------|------------|---------------------|
| delve | 过度用作 "explore" 替代 | examine, investigate, analyze |
| tapestry | 复杂性的陈腐隐喻 | network, interplay, system |
| landscape | 非字面时模糊 | field, domain, context |
| pivotal | 重要性夸大 | important, significant, central |
| crucial | 同上 | essential, necessary, critical |
| foster | 模糊动词 | promote, develop, cultivate |
| showcase | 非学术语域 | demonstrate, illustrate, present |
| testament | 陈腐 | evidence, indicator |
| navigate | 非字面时模糊 | manage, address, handle |
| leverage | 商业术语 | use, employ, utilize |
| realm | 古旧/诗意 | domain, field, area |
| embark | "begin" 的过度表达 | begin, initiate, undertake |
| underscore | 过度使用的强调动词 | emphasize, highlight, stress |
| multifaceted | 模糊的复杂性声称 | complex, varied, diverse |
| nuanced | 常为空洞 | subtle, detailed, fine-grained |
| comprehensive | 常无依据 | thorough, extensive, broad |
| robust | 模糊的质量声称 | reliable, strong, rigorous |
| intricate | 同 multifaceted | complex, detailed, elaborate |
| cornerstone | 陈腐隐喻 | foundation, basis, core element |
| paradigm | 科学哲学外过度使用 | framework, model, approach |
| synergy | 商业术语 | interaction, cooperation |
| holistic | 无定义时模糊 | comprehensive, integrated |
| streamline | 非学术 | simplify, optimize |
| cutting-edge | 陈腐 | recent, advanced, state-of-the-art |
| groundbreaking | 夸大 | novel, innovative, pioneering |

### 例外规则
若标记词汇是**目标学科的标准术语**，则豁免：
- "paradigm shift" in philosophy of science → OK
- "landscape" in ecology/geography (literal) → OK
- "robust" in statistics ("robust estimator") → OK

---

## B. 标点模式控制

### Em Dash（—）
- **限制**：每篇论文 ≤ 3 个，推荐 0-1
- **原因**：AI 文本过度使用 em dash 做插入语。学术写作通常用逗号、括号或独立句子
- **修复**：替换为逗号、括号，或重构成独立句子

### Semicolons（;）
- **限制**：每 1000 词 ≤ 2 个
- **原因**：AI 文本用分号连接独立从句，句号会更清晰
- **修复**：用句号开始新句子。分号保留给紧密相关的平行结构

### Colon-List Sequences
- **规则**：避免 2+ 连续段落都以冒号+列表开头
- **原因**：创造单调的枚举模式
- **修复**：将列表项整合到散文中，或使用单一合并列表

---

## C. Throat-Clearing Openers（ throat-clearing 开头）

删除以下句首。直切要点。

| Throat-clearing phrase | 处理方式 |
|-----------------------|---------|
| "In the realm of..." | 删除。以实际主题开头 |
| "It's important to note that..." | 删除。若重要，内容自会说话 |
| "It is worth mentioning that..." | 同上 |
| "In today's rapidly evolving..." | 删除。时间戳陈腐语增加无信息 |
| "This serves as a testament to..." | 替换为直接声称 |
| "It goes without saying that..." | 若不言而喻，别说 |
| "In order to..." | 替换为 "To..." |
| "It should be noted that..." | 删除。直接 note |
| "As a matter of fact..." | 删除。陈述事实 |
| "When it comes to..." | 替换为直接主题 |
| "At the end of the day..." | 删除。口语且模糊 |
| "With that being said..." | 删除或视情况用 "However" |

### 避免元评论
也注意描述论文在做什幺而非直接做的句子：
- "This section will discuss..." → 直接 discuss
- "The following paragraph examines..." → 直接 examine
- "We now turn our attention to..." → 直接 turn

例外：Introduction 中的 roadmap 句子（"Section 2 reviews the literature; Section 3 describes the methodology"）是标准学术实践，保留。

---

## D. 结构模式警告

### Rule of Three Compulsion（三的强迫）
- **模式**：每个论证恰好 3 个子点，每个列表恰好 3 项
- **原因**：真实分析不总是分解为三元组。两个强点胜过三个充水的
- **修复**：用证据支持的任意数量。2 可以。5 可以。不要硬凑到 3

### Uniform Paragraph Length（统一段落长度）
- **模式**：所有段落约相同长度（150-200 词）
- **原因**：自然写作有段落长度变化。短段落强调，长段落展开复杂论证
- **修复**：变化段落长度。10 句段落后的 2 句段落创造节奏

### Synonym Cycling（同义词循环）
- **模式**：一段内对同一概念用 3+ 不同同义词避免重复
- **原因**：学术写作中，一致的术语是美德。"students" → "learners" → "participants" → "subjects" 混淆而非 impress
- **修复**：每节每个概念选一个术语。重复它。技术重复是清晰，不是弱点

### Binary Contrast Overuse（二元对比过度使用）
- **模式**："Not X. Y." 或 "It's not about X — it's about Y." 每篇论文使用超过 2 次
- **原因**：这个修辞装置一次有效。重复成为 tic
- **限制**：每篇论文 ≤ 2 次

### Mirror Structure（镜像结构）
- **模式**：每节内部结构相同（主题句 → 3 个证据点 → 综合句）
- **原因**：创造模板盖章感。不同节服务不同目的，应有不同内部节奏
- **修复**：让节结构跟随内容需要。方法可以是程序性的。讨论可以是探索性的

---

## E. Burstiness（句子长度变化）

好的写作有**句子长度的自然变化**。短句创造冲击。长句展开复杂思想。交替创造节奏。

### 检测规则
若 5+ 连续句子都落在狭窄词数范围内（如都在 20-25 词之间）：**标记审查**。

### 修复方法
- 插入短句（≤ 10 词）打破模式
- 若模式单调短促，将两个短句合并成一个复杂句
- 大声朗读段落 — 若感觉像节拍器，变化它

### 各节 Burstiness 目标
- **Abstract**: 中等变化（事实性、稳定节奏）
- **Introduction**: 高变化（短句 hook，长句 build）
- **Literature Review**: 中等（稳定分析节奏，偶尔短综合）
- **Methods**: 低变化可接受（程序性章节自然长度统一）
- **Results**: 中等（关键发现短句，详细描述长句）
- **Discussion**: 最高变化（强调短句，解释长句，结论极短句）

---

## 使用方式

### 起草时（首选）
在每节的自我审查子步骤中**边写边应用**。在问题传播前抓住它们。

### 最终审查（后备）
若起草时未应用，在交给引用合规检查前做全文扫描。

### 评分（内部，不向用户报告）
每类规则跟踪违规：
- 0 违规：Clean
- 1-3 违规：Minor — 自我审查中修复
- 4+ 违规：Pattern issue — 审查该节的写作方法

不要向用户报告分数。在起草期间静默修复问题。
