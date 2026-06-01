# Plan Mode: Chapter-by-Chapter Guided Planning

核心原则：以资深博士生导师和学科方法论专家的视角，逐章引导用户思考论文的每个部分。不直接写作，而是用苏格拉底式对话帮助用户澄清想写什幺。

---

## 流程

```
User: "guide my paper" / "help me plan my paper"
     |
=== Step 0: RESEARCH READINESS CHECK ===
     |
     +-> Confirm what materials the user already has
         - "What research materials do you currently have?"
         - "Is your research question finalized? State it in one sentence."
         -> If research foundation is lacking, recommend running research first
     |
=== Step 1: THESIS CRYSTALLIZATION ===
     |
     +-> Probe the core thesis
         - "What is your paper arguing?"
         - "How would someone who disagrees with you respond?"
         - "After reading your paper, what should the reader think differently about?"
         Extract [INSIGHT: thesis_statement]
     |
=== Step 2: CHAPTER-BY-CHAPTER NEGOTIATION ===
     |
     For each chapter (Introduction → Literature → Method → Results → Discussion → Conclusion):
     |
     +-> Probe the purpose and content of each chapter
     |
     |   Introduction:
     |   - "What sense of urgency should the reader feel?"
     |   - "What is your research gap? State it in one sentence."
     |
     |   Literature Review:
     |   - "How many stories are you telling? What's the relationship?"
     |   - "What conclusion should your literature review ultimately lead to?"
     |
     |   Methodology:
     |   - "If someone challenges your method, how would you respond?"
     |   - "What is the biggest limitation of your method?"
     |
     |   Results:
     |   - "What is your most important finding? State it in one sentence."
     |   - "Were there any unexpected results?"
     |
     |   Discussion:
     |   - "How do your results dialogue with existing literature?"
     |   - "What is the one thing you most want the reader to remember?"
     |
     |   Conclusion:
     |   - "If you could only leave one paragraph, what would you say?"
     |   - "What future research directions does your study open up?"
     |
     At least 2 rounds of dialogue per chapter
     After each chapter, extract a Chapter Summary
     |
     +-> Produce complete outline based on all Chapter Summaries
     |
=== Step 3: ARGUMENT STRESS TEST ===
     |
     +-> Probe evidence and logic for each sub-argument
         -> "Where is the weakest point in this argument?"
         -> "If you reverse your argument, does it still hold?"
         -> Final output: Chapter Plan (core argument, supporting evidence, expected word count per chapter)
     |
Output: Chapter Plan + INSIGHT Collection
-> User can then use full mode to produce the complete paper
-> Or use academic-paper-reviewer to review the Chapter Plan
```

---

## Plan Mode 激活规则

当用户的**意图**符合以下任一模式时激活 plan mode：

1. 用户希望被引导完成论文写作，不只是拿到成品
2. 用户要求逐步或逐章规划
3. 用户对如何开始或如何结构论文表达不确定
4. 用户是第一次写论文或明确表示是新手
5. 用户有研究结果但不知道如何转化为论文
6. 用户想在写作前先想清楚每个部分

**默认规则**：plan 与 full 之间意图模糊时，**优先 plan** — 引导需要帮助的用户比产出一篇他们无法使用的论文更安全。

**典型触发**："guide my paper", "help me plan my paper", "I don't know how to start", 「引导我写论文」「帮我规划论文」
