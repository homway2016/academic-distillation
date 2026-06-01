# academic-distillation

> 从 [ARIS (Academic Research Skills)](https://github.com/Imbad0202/academic-research-skills) 蒸馏而来的单模型版本。
> 剥离了跨模型编排（Codex MCP 依赖），保留核心方法论、协议与模板，适配 Claude Code + Kimi 2.6 环境。

单模型环境下的学术论文写作与评审套件。

## 结构

```
skill_distillation/
├── academic-paper/              # 8 阶段论文写作引擎
│   ├── SKILL.md
│   ├── references/
│   └── templates/
├── academic-paper-reviewer/     # 5 人独立评审面板
│   ├── SKILL.md
│   ├── references/
│   └── templates/
└── tools/                       # 纯 stdlib CLI 增强工具（可选）
    ├── arxiv_fetch.py           # arXiv 搜索 + PDF 下载
    ├── verify_papers.py         # 三层引用验证
    ├── evidence_check.py        # 数字-证据一致性检查
    └── threat_scan.py           # 上传文件安全扫描
```

## 安装

```bash
cp -r academic-paper ~/.claude/skills/
cp -r academic-paper-reviewer ~/.claude/skills/
# tools/ 为可选，复制到项目目录后使用
```

## 触发词

- **写论文**: "write a paper on ..." / "写论文"
- **审稿**: "review my paper" / "审稿"

每个 SKILL.md 底部有完整的触发词列表。

---

## Credits

- **上游项目**: [Imbad0202/academic-research-skills](https://github.com/Imbad0202/academic-research-skills) — ARIS 完整版（含跨模型编排、13-agent 研究流水线）
- **上游项目**: [Auto-claude-code-research-in-sleep-main] - 参考tool
- **LaTeX 模板来源**: 各会议官方 Author Kit（NeurIPS / ICML / ICLR / AAAI / ACL / ACM / CVPR / IEEE）
- **CLI 工具来源**: ARIS `tools/` 目录（已剥离内容，保留骨架 + 纯 stdlib 脚本）
