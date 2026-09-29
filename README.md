# C2 · AI for Math 论文 — From Natural Language to Verifiable Reasoning

> 挑战：**C2 AI for Math 论文**（challenge_id：`ch-20260717031343-8ot0ji`）
> 类型：可投稿 LaTeX 学术论文 + 参考文献 + AI 协作日志 + 七维 AAR 复盘
> 状态：已交付（论文 PDF 15 页，参考文献 24 篇全部人工核验）

本仓库是挑战 C2 的完整交付包，核心产物是一篇关于 **AI 数学推理可靠性** 的概念性学术论文：在自然语言生成与形式化验证之间，显式引入一层 **语义归约层（Semantic Reduction Layer）**，并用 **类型化中间表示（TIR, Typed Intermediate Representation）** 把它形式化。

---

## 交付物清单

| 文件 | 说明 |
|---|---|
| `paper.tex` | 论文 LaTeX 源码（42 KB，含 tikz 图、algorithm 环境、定理与命题、对比表） |
| `paper.pdf` | 编译产物（15 页） |
| `references.bib` | BibTeX 参考文献，**24 条**，全部逐条人工核验真实性 |
| `AI日志.md` | AI 协作日志：16 轮 prompt 迭代记录、每轮人工核验结论、修正的 3 处 AI 错误 |
| `AAR复盘.md` | 七维 AAR 复盘报告 + 对照 rubric 的自评得分（自评 90/100） |
| `README.md` | 本文件 |

## 论文核心内容

**标题**：From Natural Language to Verifiable Reasoning: A Semantic Reduction Framework for Reliable AI Mathematics

**问题**：LLM 的数学推理输出本质不可靠——自然语言思维链是概率性的、无类型的，且难以直接验证。现有两条路线（纯生成＋事后检查、全形式化定理证明）都没能搭好「流畅自然语言」与「机器可检验的正确性」之间的桥。

**论点**：AI4Math 可靠性的**瓶颈不在生成能力，也不在验证能力，而在于从非形式自然语言到结构化、类型安全形式对象这一层不稳定的翻译**。

**方案**：三层语义归约框架 + 双向流水线
1. 自然语言层 → TIR 层：把非形式推理归约为带类型的中间表示
2. TIR 层 → 形式后端：对 TIR 做类型检查与约束检查，交给 Lean/Coq 等后端验证
3. 已验证结果 → 自然语言层：反向渲染回人类可读的表述

**章节结构**：Introduction → Three-Layer Decomposition Model → The Bottleneck: Semantic Reduction → Proposed Framework (TIR) → Related Work → Applications → Experimental Design → Discussion → Conclusion

**性质说明**：本文是**概念性论文**（conceptual paper），贡献是框架与实验设计，不含实际实验数据；论文中已明确标注这一边界。

## 如何编译

```bash
pdflatex paper
bibtex   paper
pdflatex paper
pdflatex paper
```

依赖：标准 TeX Live / MacTeX 发行版（`article` 文档类 + `amsmath`、`amssymb`、`tikz`、`algorithm`/`algorithmic`、`booktabs`、`hyperref` 等常用宏包，均为发行版自带）。

已在 `pdflatex` 下编译通过，产出 `paper.pdf`（15 页）；残留少量 overfull hbox 警告，不影响成稿。

## AI 协作方式（摘要）

采用「**检索 → 核验 → 写入**」与「**生成 → 审查 → 修改**」两条工作流，全部 16 轮 prompt 记录在 `AI日志.md`：

- 文献引用 24/24 逐篇人工核验（100%）
- 具体数字、系统性能、发表信息 100% 核验
- 共发现并修正 **3 处 AI 错误**：AlphaProof 发表信息、GPT-4 在 MATH 上的准确率数字（AI 编造，无权威来源）、AlphaProof 奖牌等级（金牌 → 官方表述为银牌水平）
- 关键事实至少在两个独立来源交叉验证（如 arXiv + 官方博客）

三条 AI 误导案例的发现方式、误导机制分析与对策，详见 `AAR复盘.md` 第六、七维。
