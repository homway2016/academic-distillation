# Academic Paper — 学术论文写作引擎

通用学术论文写作工具，覆盖全学科，以高等教育领域为默认参考。支持 10 种运行模式、6 种论文类型、5 种引用格式、双语摘要、多格式输出。

---

## 快速开始

**最小命令：**
```
Write a paper on the impact of AI on higher education quality assurance
```

**执行流程：**
1. 配置访谈 — 论文类型、学科、引用格式、输出格式
2. 文献策略 — 系统检索策略、来源筛选
3. 架构设计 — 论文结构、大纲、字数分配
4. 论证构建 — 主张-证据链、逻辑流
5. 全文起草 — 逐节草稿、语域调整
6. 引用合规 + 双语摘要（并行）
7. 同行评审 — 五维评分、修改建议
8. 输出格式化 — LaTeX/DOCX/PDF/Markdown

---

## 触发条件

**英文**：write paper, academic paper, paper outline, write abstract, revise paper, literature review, check citations, convert to LaTeX, format paper, conference paper, journal article, guide my paper, step by step paper, draft manuscript, parse reviews, revision roadmap

**简体中文**：写论文, 学术论文, 论文大纲, 写摘要, 修改论文, 文献综述, 检查引用, 转 LaTeX, 研讨会论文, 期刊文章, 引导我写论文, 帮我规划论文, 逐步写论文, 审查意见, 修订路线图

---

## 10 种运行模式

| 模式 | 用途 | 阶段 |
|------|------|------|
| `full` | 完整论文写作（全部 8 阶段） | 0→7 |
| `plan` | 苏格拉底式逐章引导规划 | Step 0-3 |
| `outline-only` | 仅生成详细大纲 | 0→2 |
| `revision` | 基于评审意见的论文修改 | 6→4 |
| `revision-coach` | 解析非结构化评审意见为结构化路线图 | 独立 |
| `abstract-only` | 仅生成双语摘要 | 5b |
| `lit-review` | 仅文献综述 | 1 |
| `format-convert` | 格式转换 | 7 |
| `citation-check` | 引用检查与格式转换 | 5a |
| `disclosure` | AI 使用披露声明生成 | 独立 |

> 详细模式选择指南见 `references/mode_selection_guide.md`

---

## 8 阶段编排工作流

```
Phase 0: CONFIG        -> 配置访谈              -> Paper Configuration Record
Phase 1: RESEARCH      -> 文献策略              -> Search Strategy + Source Corpus
Phase 2: ARCHITECTURE  -> 架构设计              -> Paper Outline + Evidence Map
Phase 3: ARGUMENTATION -> 论证构建              -> Argument Blueprint
Phase 4: DRAFTING      -> 全文起草              -> Complete Draft
Phase 5a: CITATIONS    -> 引用合规  ──┐         -> Citation Audit Report
Phase 5b: ABSTRACT     -> 双语摘要   ┘         -> Bilingual Abstract + Keywords
Phase 6: PEER REVIEW   -> 同行评审              -> Review Report (max 2 revision loops)
Phase 7: FORMAT        -> 输出格式化            -> Final Output Package
```

### 各阶段详细说明

**Phase 0: CONFIG（交互式）**
- 论文类型（IMRaD / 文献综述 / 理论 / 案例 / 政策简报 / 会议论文）
- 学科与子领域
- 目标期刊（可选）
- 引用格式（APA 7 / Chicago / MLA / IEEE / Vancouver）
- 输出格式（LaTeX / DOCX / PDF / Markdown）
- 语言（EN / zh-CN / 双语段落）
- 字数目标
- 现有材料（RQ、数据、草稿、文献）
- **检查点**：用户确认配置记录后方可进入 Phase 1

**Phase 1: RESEARCH**
- 数据库选择 + 检索式
- 纳入/排除标准
- 来源筛选 + 注释书目
- 文献矩阵（Source × Theme）
- 研究缺口映射
- **检查点**：用户审阅来源（可选增删）

**Phase 2: ARCHITECTURE**
- 结构模式选择（见 `references/paper_structure_patterns.md`）
- 逐节大纲 + 字数分配
- 证据到章节分配
- 章节间过渡逻辑
- **检查点**：用户批准大纲（可要求重组）

**Phase 3: ARGUMENTATION**
- 中心论点 + 子论点
- 每节的 Claim-Evidence-Reasoning 链
- 反论点识别 + 反驳策略
- 逻辑流图

**Phase 4: DRAFTING**
- 按大纲逐节写作
- 学科语域调整
- 文内引用整合
- 每节字数跟踪
- 章节间过渡段落

**Phase 5a & 5b: CITATIONS + ABSTRACT（并行）**

- 引用合规：文内 ↔ 参考文献列表交叉检查（零孤儿引用）、格式合规、DOI/URL 验证、自引比例检查
- 双语摘要：英文（150-300 词）+ 简体中文（300-500 字），独立撰写（非机械翻译），各 5-7 个关键词

**Phase 6: PEER REVIEW**
- 五维评分：Originality (20%) | Methodological Rigor (25%) | Evidence Sufficiency (25%) | Argument Coherence (15%) | Writing Quality (15%)
- 裁决：Accept / Minor Revision / Major Revision / Reject
- 行级反馈 + 修改建议
- 最多 2 轮修改循环 → 回到 Phase 4

**Phase 7: FORMAT**
- 目标格式转换（LaTeX + .bib / DOCX / PDF / Markdown）
- 期刊特定格式（若指定目标期刊）
- 投稿信（若期刊投稿）
- AI 披露声明
- 最终质量检查清单

---

## 6 大铁律

1. **⚠️ IRON RULE**: 用户必须确认 Paper Configuration Record 后方可进入 Phase 1
2. **Phase 2 → 3**: 用户必须批准大纲（可要求重组）
3. **⚠️ IRON RULE**: 最多 2 轮修改循环；未解决项 → "Acknowledged Limitations"
4. **同行评审** Critical 级别问题阻止进入 Phase 7
5. 用户可跳过 Phase 1（文献）若提供自有来源
6. 所有声称必须有引用支撑；矛盾必须披露并比较证据质量

---

## 核心协议索引

| 协议 | 文件 | 用途 |
|------|------|------|
| 模式选择指南 | `references/mode_selection_guide.md` | 10 种模式的选择流程图和决策表 |
| 论文结构模式 | `references/paper_structure_patterns.md` | 6 种论文结构模型（IMRaD / 综述 / 理论 / 案例 / 政策 / 会议）|
| 学术写作风格 | `references/academic_writing_style.md` | 学科语域调整、措辞强度、过渡词、段落构造 |
| 写作质量检查 | `references/writing_quality_check.md` | AI 典型措辞警示、标点控制、 throat-clearing 清除、结构模式警告 |
| 写作判断框架 | `references/writing_judgment_framework.md` | 清晰度测试、读者旅程、修订决策矩阵 |
| 摘要写作指南 | `references/abstract_writing_guide.md` | 英/中摘要结构、关键词选择、质量检查清单 |
| 引用格式切换 | `references/citation_format_switcher.md` | 5 种格式（APA/Chicago/MLA/IEEE/Vancouver）的 in-text 和参考文献规则 |
| 统计可视化标准 | `references/statistical_visualization_standards.md` | APA 7.0 图表规范、色盲友好调色板、图表类型决策树、Python/R 代码模板 |
| 知识隔离协议 | `references/anti_leakage_protocol.md` | 防止 LLM 参数记忆污染用户材料 |
| AI 披露协议 | `references/disclosure_mode_protocol.md` |  venue-specific AI 使用声明生成 |
| Plan 模式协议 | `references/plan_mode_protocol.md` | 苏格拉底式逐章引导规划流程 |

---

## LaTeX 模板索引（`templates/latex/`）

| 模板 | 文件 | 适用场景 |
|------|------|---------|
| **IEEE Conference** | `templates/latex/ieee_conference.tex` | IEEE 双栏会议论文（ICCV/ICASSP/INFOCOM 等） |
| **IEEE Journal** | `templates/latex/ieee_journal.tex` | IEEE Transactions 期刊长文 |
| **NeurIPS** | `templates/latex/neurips2026.tex` | 机器学习顶会，含 `ack` 环境 |
| **ICML** | `templates/latex/icml2026.tex` | 机器学习顶会，双栏 + 影响声明 |
| **ICLR** | `templates/latex/iclr2026.tex` | 表征学习顶会，简洁单栏 |
| **AAAI** | `templates/latex/aaai2026.tex` | AI 综合顶会，含 anonymous/camera-ready 切换 |
| **ACL** | `templates/latex/acl2026.tex` | NLP 顶会，含 Limitations 章节 |
| **ACM MM** | `templates/latex/acm_mm2026.tex` | 多媒体顶会，ACM 版权格式 |
| **CVPR** | `templates/latex/cvpr2026.tex` | 计算机视觉顶会，含 paper ID |
| **数学命令** | `templates/latex/math_commands.tex` | 通用 ML 符号宏（被多数模板 `\input`） |

> 所有模板均为**骨架版本**（已剥离官方说明文字），直接可用。需从对应会议官网下载 `.sty`/`.cls` 样式文件配合使用。

---

## 可选 CLI 工具增强（`tools/`）

以下 Python 脚本为**纯 stdlib**，零外部依赖，可作为 skill 的确定性补充：

| 工具 | 用途 | 对应阶段 |
|------|------|---------|
| `tools/arxiv_fetch.py` | arXiv 搜索 + PDF 下载 | Phase 1（文献检索） |
| `tools/verify_papers.py` | 三层引用验证（arXiv → CrossRef → S2） | Phase 5a（引用合规） |
| `tools/evidence_check.py` | 验证论文中的数字/字符串是否真实存在于结果文件中 | Phase 4-5（数据一致性） |
| `tools/threat_scan.py` | 扫描上传文件是否包含 prompt injection | 任何文件上传前 |

**使用方式**：`python3 tools/<script>.py --help`

---

## 工具策略

| 工具 | 用途 | 保留 |
|------|------|------|
| Read | 读取用户上传的文献、数据、草稿 | ✅ |
| Write / Edit | 写入/编辑论文草稿、配置文件 | ✅ |
| Spawn Agent | 并行调用 specialized agents（如引用检查 + 摘要生成） | ✅ |
| Tavily MCP | 文献检索、DOI 验证、最新政策查询 | ✅（替代 WebSearch）|

---

## 输出格式

- **文本**: LaTeX (.tex + .bib), DOCX (via Pandoc), PDF, Markdown
- **图表**: Python matplotlib / R ggplot2 代码 + LaTeX `\includegraphics` 集成
- **引用**: APA 7.0（默认）、Chicago（Author-Date 或 Notes-Bibliography）、MLA 9、IEEE、Vancouver
