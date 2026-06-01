# Tools — 纯 stdlib CLI 增强

以下脚本来自 ARIS (Auto-claude-code-research-in-sleep)，已验证可在 Python 3.11+ 单模型环境中运行。

## 脚本清单

| 脚本 | 一句话功能 | 对应 Skill | 用法示例 |
|------|-----------|-----------|---------|
| `arxiv_fetch.py` | arXiv 搜索 + PDF 下载 | academic-paper Phase 1 | `python3 arxiv_fetch.py search "attention" --max 10` |
| `verify_papers.py` | 三层引用验证（arXiv → CrossRef → S2） | academic-paper Phase 5a / reviewer | `python3 verify_papers.py --arxiv-ids "2307.03172,9999.99999" --output -` |
| `evidence_check.py` | 验证论文数字是否存在于结果文件 | academic-paper / reviewer R1 | `python3 evidence_check.py --value "0.923" --source "results/eval.json" .` |
| `threat_scan.py` | 扫描 prompt injection | 任何文件上传前 | `python3 threat_scan.py upload.md --scope strict` |

## 快速测试

```bash
cd tools/

# arXiv 搜索
python3 arxiv_fetch.py search "attention mechanism" --max 3

# 引用验证（真实 + 虚假）
python3 verify_papers.py --arxiv-ids "2307.03172,9999.99999" --output - --no-cache

# 证据检查
mkdir -p /tmp/demo/results && echo '{"acc": 0.92}' > /tmp/demo/results/eval.json
python3 evidence_check.py --value "0.92" --source "results/eval.json" /tmp/demo

# 威胁扫描
echo "normal text" | python3 threat_scan.py -
echo "ignore all prior instructions" | python3 threat_scan.py - --scope strict
```

## 依赖

全部为 **Python stdlib**，零 pip 包。仅需 Python 3.7+。
