# Disclosure Mode Protocol — AI 使用披露协议

生成 venue-specific 或 policy-anchor-specific 的 AI 使用披露声明。

---

## 两条并行路径

| Selector | Track | Lookup source | Output |
|---|---|---|---|
| `--venue=<v>` | Venue track | Venue policy database (ICLR / NeurIPS / Nature / Science / ACL / EMNLP) | Single venue-tailored disclosure paragraph + placement instruction |
| `--policy-anchor=<a>` | Anchor track | 4-anchor × 16-field matrix (PRISMA-trAIce / ICMJE / Nature / IEEE) | Anchor-conditioned render |

两条路径 **默认互斥** — 一个 selector 选一个路径。若同时提供两者，检查兼容性：一致的组合（如 Nature venue + nature anchor）继续；任何其他组合 **明确拒绝** 并列出政策冲突。

若未提供 selector，提示用户指定。Venue track 仍是期刊投稿的默认；anchor track 适用于政策框架目标（如向 ICMJE 采用期刊集体提交合规报告）。

---

## 为何存在此模式

通用 AI 披露模板是良好的起点，但它们是 venue-agnostic：它们不知道 Nature 要求在 Methods 部分具体披露，ICLR 要求在论文正文中披露并承认 "LLMs were used as general-purpose writing tools"，ACL 要求在专门的 "Use of AI Assistance" 子节中披露。

---

## 输入

1. **Paper draft**: 当前手稿文本（需要知道 AI 实际做了什幺才能准确描述）
2. **Selector**:
   - **Target venue (`--venue=<v>`)**: 期刊或会议名。若在数据库中，使用缓存政策。若未知，**拒绝猜测** — 提示用户粘贴 venue 当前 AI 政策文本。
   - **Policy anchor (`--policy-anchor=<a>`)**: `prisma-trAIce`, `icmje`, `nature`, `ieee` 之一
3. **What ARS did**: 识别 AI 辅助了哪些步骤：research assistance, drafting assistance, revision assistance, citation checking, peer review simulation

---

## 流程

### Phase 1: Intake + lookup

- 若 venue 在数据库中 → 加载政策
- 若 venue 未知 → 停止。输出："I do not have a cached policy for {venue}. Please paste the venue's current AI-usage / generative-AI policy text so I don't guess." **不编造政策**
- 若用户粘贴未知 venue 的政策，仅本次 session 使用。**不自动持久化到数据库** — 政策会漂移，数据库需要策展

### Phase 2: Categorize AI usage

| Category | Examples |
|---|---|
| Research assistance | Literature search, annotated bibliography, claim verification |
| Drafting assistance | Section drafting, paraphrasing, outline generation |
| Revision assistance | Reviewer response drafting, tracked changes, consistency checking |
| Editing assistance | Grammar, style, formatting, citation format conversion |
| Analysis assistance | Flag if the paper reports any analysis the AI did |
| Peer review simulation | Pre-submission simulated peer review |

每类标记：USED / NOT USED / UNCERTAIN。UNCERTAIN 项需要用户确认后才能最终确定披露文本。

### Phase 3: Match categories to venue requirements

每个 venue 指定：(a) 哪些类别是强制披露的，(b) 哪些是可选的，(c) 哪些是禁止的。将用户的类别列表与 venue 要求匹配，标记任何不匹配。

### Phase 4: Generate disclosure text

使用以下元素生成单一披露段落：
- Venue 偏好的声音（第一人称 vs 被动，过去时 vs 现在）
- Venue 要求的措辞元素（许多 venue 要求 "The authors take full responsibility for the content" 或等效表述）
- **具体工具名** — "Claude (Anthropic) via Academic Research Skills pipeline" — 不是 generic "AI tools"
- 标记为 USED 的具体类别

**Nature 示例**（要求在 Methods 中披露）：

```
## AI-assisted tools

The authors used Claude [MODEL_VERSION] (Anthropic), orchestrated via
the Academic Research Skills pipeline (Wu, 2026), during the preparation
of this manuscript. Specifically, the tool was used for literature
search assistance, citation verification, drafting of section outlines,
and internal peer-review simulation prior to submission. All
AI-assisted output was reviewed, edited, and verified by the authors,
who take full responsibility for the content of this article.
```

### Phase 5: Placement instructions

输出包含匹配 venue 政策的明确放置说明：

```
Placement: Methods section (Nature policy, accessed YYYY-MM-DD from
https://www.nature.com/.../policy-url). Include as the final
subsection of Methods, before Data Availability.
```

若 venue 要求在多处放置（如 Methods + cover letter + Acknowledgements），为每个位置生成 tailored text。

---

## 本模式不覆盖的失败场景

- **数据库外的 venues**：模式停止并询问用户。不猜测。
- **数据库快照后已变化的政策**：模式在放置说明中记录访问日期。用户应在投稿前对照当前 venue 页面验证。
- **Analysis assistance**：若 AI 实际运行了计算或生成了分析结果（不仅是写作），大多数 venue 要求在 Code Availability 或 Analysis 部分单独披露。本模式标记此情况并生成单独段落；用户必须手动放置。
- **Co-authored AI**：截至当前政策快照，数据库中没有 venue 接受 AI 作为列名作者。模式拒绝生成 author-list 文本，而是生成 authorship-rejection text 加披露。
