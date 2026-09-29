# AI 协作日志 — C2 AI for Math 论文

> 挑战 ID：ch-20260717031343-8ot0ji
> 任务：围绕 AI4Math 可靠性框架撰写可投稿 LaTeX 学术论文
> 周期：5 天（2026-09-25 ~ 2026-09-29）
> AI 工具：豆包（Doubao）大语言模型
> 核验原则：所有 AI 生成的文献引用、事实陈述、技术细节均经人工联网核验

---

## Day 1 — 2026-09-25（周五）：任务解析与选题确定

### 上午：任务材料阅读

**AI 协作动作：**
- Prompt：「请帮我解读 CHALLENGE.md，列出这个任务的所有硬性要求、交付物清单、评分标准和红线。」
- AI 输出：整理出 4 项必需交付物（paper.tex、references.bib、AI日志、AAR）、5 个评分维度（研究严谨性25/技术实现20/产物完整性15/AI使用20/复盘质量20）、2 条红线（引用造假→严谨性0分；不可编译→技术实现≤5分）。
- **人工核验**：逐条对照 challenge.json 和 rubric.json 原文，确认 AI 解读准确无误。评分维度分值与 rubric.json 完全一致。

### 下午：选题与框架确定

**AI 协作动作：**
- Prompt：「基于中文论文大纲（AI4Math）.pdf，帮我确定论文的核心论点和原创性贡献。大纲提出了三层结构（生成/语义规约/验证），请帮我提炼出可以作为论文原创贡献的点。」
- AI 输出：建议了 4 个原创贡献点：(C1) 三层分解模型的形式化定义；(C2) 语义规约层作为核心瓶颈的论证；(C3) Typed IR 的设计规范；(C4) 双向一致性管道。
- **人工核验**：对照大纲 PDF 原文，确认这 4 点确实来自大纲但经过了形式化提炼。大纲中"当前系统失败主要源于第二层"这一观察被提升为核心论点，合理。

**AI 生成结论的人工核验记录：**
| AI 生成内容 | 核验方式 | 核验结果 |
|---|---|---|
| 评分维度分值 | 对照 rubric.json | ✅ 一致 |
| 交付物清单 | 对照 challenge.json deliverables 字段 | ✅ 一致 |
| 大纲三层结构 | 对照 PDF 第2节 | ✅ 一致 |

---

## Day 2 — 2026-09-26（周六）：文献检索与批判性阅读

### 全天：联网文献检索

**AI 协作动作（多轮迭代）：**

**第 1 轮：**
- Prompt：「请搜索 AI4Math 可靠性领域的关键文献，包括 LLM 数学推理、形式化证明、神经定理证明、Chain-of-Thought 验证等方向。每篇文献需要给出标题、作者、发表年份、发表 venue 和 arXiv 编号。」
- AI 输出：列出了 12 篇文献，包括 Wei et al. 2022 (CoT)、Wang et al. 2022 (Self-Consistency)、Polu & Sutskever 2020 (GPT-f)、Trinh et al. 2024 (AlphaGeometry) 等。
- **人工核验**：逐篇在 arXiv 和 Google Scholar 搜索验证。发现 AI 输出中 AlphaProof 的发表信息不准确（AI 说是 2024 年 arXiv，实际是 2025 年 11 月发表在 Nature）。已修正。

**第 2 轮（补充检索）：**
- Prompt：「请补充搜索以下方向的文献：(1) Program-of-Thought 和 Toolformer；(2) LeanDojo 和 DeepSeek-Prover；(3) LLM 数学推理可靠性评估（如 MathCheck）；(4) auto-formalization。」
- AI 输出：补充了 Chen et al. 2022 (PoT)、Schick et al. 2023 (Toolformer)、Yang et al. 2023 (LeanDojo)、Liang et al. 2024 (MathCheck)、Wu et al. 2022 (Autoformalization) 等。
- **人工核验**：全部在 arXiv 验证通过。Toolformer 的发表 venue 确认为 NeurIPS 2023。LeanDojo 确认为 NeurIPS 2023。

**第 3 轮（批判性阅读）：**
- Prompt：「请对比分析以下几类方法的可靠性差异：(1) 纯 CoT；(2) Self-Consistency；(3) Program-of-Thought；(4) Tool-augmented；(5) 形式化定理证明（GPT-f/AlphaProof）。从生成能力、可验证性、适用范围三个维度对比。」
- AI 输出：生成了一个 5×3 的对比分析，指出纯 CoT 可验证性为零，形式化证明可验证性最高但适用范围受限，Program-of-Thought 只能验证计算不能验证逻辑。
- **人工核验**：这个分析是推理性结论，无法直接"查证"，但与各论文的方法描述一致。Program-of-Thought 论文确实只将计算委托给解释器，逻辑推理仍在 NL 中。AlphaProof 确实完全在 Lean 环境中运行。判断为合理。

**AI 误导案例记录：**
> **案例**：AI 在第 1 轮检索中将 AlphaProof 描述为"2024 年 arXiv 预印本"。
> **实际情况**：AlphaProof 于 2024 年 7 月由 DeepMind 博客发布，正式论文于 2025 年 11 月发表在 Nature。
> **发现方式**：人工在 DeepMind 官网和 Nature 网站交叉验证。
> **修正**：将 AlphaProof 的引用改为 Hubert et al., Nature, 2025。
> **教训**：AI 对"近期发表"的文献信息容易过时或混淆预印本与正式发表版本，必须逐篇核验发表时间和 venue。

**文献核验汇总表：**
| 文献 | AI 给出的信息 | 人工核验结果 | 修正 |
|---|---|---|---|
| Wei et al. 2022 CoT | NeurIPS 2022, arXiv:2201.11903 | ✅ 正确 | 无 |
| Wang et al. 2022 Self-Consistency | ICLR 2023, arXiv:2203.11171 | ✅ 正确 | 无 |
| Chen et al. 2022 PoT | arXiv:2211.12588 | ✅ 正确 | 无 |
| Schick et al. 2023 Toolformer | NeurIPS 2023, arXiv:2302.04761 | ✅ 正确 | 无 |
| Polu & Sutskever 2020 GPT-f | arXiv:2009.03393 | ✅ 正确 | 无 |
| Trinh et al. 2024 AlphaGeometry | Nature 625, 476-481 | ✅ 正确 | 无 |
| Hubert et al. AlphaProof | 2024 arXiv | ❌ 错误 | 改为 Nature 2025 |
| Yang et al. 2023 LeanDojo | NeurIPS 2023, arXiv:2306.15626 | ✅ 正确 | 无 |
| Liang et al. 2024 MathCheck | arXiv:2407.08733 | ✅ 正确 | 无 |
| Wu et al. 2022 Autoformalization | NeurIPS 2022, arXiv:2205.12615 | ✅ 正确 | 无 |

---

## Day 3 — 2026-09-27（周日）：论文主体写作

### 上午：引言与三层模型

**AI 协作动作：**
- Prompt：「请帮我撰写论文的 Introduction 部分。要求：(1) 背景介绍 AI4Math 的进展和可靠性问题；(2) 指出现有两类范式（纯生成+事后验证、形式化证明）的不足；(3) 提出我们的三层框架作为解决方案；(4) 明确列出 4 个原创贡献点。用学术英语写作。」
- AI 输出：生成了约 800 词的 Introduction，包含背景、问题、方法、贡献、论文结构。
- **人工核验与修改**：
  - AI 提到"GPT-4 在 MATH 上达到 80% 准确率"——这个数字无法确认来源，已删除具体数字，改为定性描述。
  - AI 将 AlphaProof 描述为"金牌水平"——实际是银牌水平，已修正。
  - 贡献点的表述经过人工润色，确保每个贡献都有明确的技术内容而非空泛声明。

- Prompt：「请撰写 Three-Layer Decomposition Model 部分，包括 Generation Layer、Semantic Reduction Layer、Verification Layer 的详细描述。需要包含一个 formal definition 和 tikz 图的代码。」
- AI 输出：生成了三层模型的形式化定义、各层的特征描述、Curry-Howard 对应作为理论基础、以及一个 tikz 三层架构图。
- **人工核验**：
  - Curry-Howard 对应的引用正确（Howard 1980）。
  - tikz 图代码经人工检查语法正确，箭头和节点定义无误。
  - Semantic Reduction Layer 的"核心挑战"（语义歧义、类型缺失、不可逆性）与大纲一致。

### 下午：瓶颈分析与框架设计

**AI 协作动作：**
- Prompt：「请撰写 The Bottleneck: Semantic Reduction 部分。需要包含：(1) 两个 proposition 及其证明（Verification Dependency 和 Hallucination Persistence）；(2) 三类实证证据；(3) 一个 failure mode 对比表格。」
- AI 输出：生成了两个 proposition 的形式化陈述和证明，三类实证证据（形式化系统成功时已形式化、NL 系统可验证性失败、工具增强部分解决），以及一个 7 行的对比表格。
- **人工核验**：
  - Proposition 的证明逻辑自洽，使用了函数式的形式化表述，合理。
  - 实证证据中引用的 AlphaProof、MathCheck、Program-of-Thought 均与原文一致。
  - 对比表格中"TIR-based (ours)"一行标记为全 check，这是我们的主张而非已验证事实，已在表格说明中注明为"目标"。

- Prompt：「请撰写 Proposed Framework 部分，包括 TIR 的形式化定义、pipeline 架构（含 algorithm 伪代码）、双向一致性定义。」
- AI 输出：生成了 TIR 的五元组定义（signature, type system, operational semantics, constraints, compositional graph）、pipeline 的 8 步 algorithm 环境、双向一致性的两个方程。
- **人工核验**：
  - TIR 定义中的组件（类型系统、操作语义、约束系统、组合图结构）与大纲 4.1 节一致。
  - Algorithm 伪代码的 8 个步骤逻辑连贯，从生成到渲染形成闭环。
  - 双向一致性的 round-trip 方程表述正确。

**AI 生成内容的人工修改记录：**
| 章节 | AI 原始内容 | 问题 | 修改 |
|---|---|---|---|
| Introduction | "GPT-4 在 MATH 上 80% 准确率" | 来源不明 | 删除具体数字 |
| Introduction | AlphaProof "金牌水平" | 事实错误 | 改为"银牌水平" |
| Bottleneck 表格 | TIR 全 check | 未验证的主张 | 注明为"目标架构" |
| TIR 定义 | 缺少设计原则 | 不完整 | 补充 4 条设计原则 |

---

## Day 4 — 2026-09-28（周一）：相关工作、应用、实验设计

### 上午：相关工作与应用

**AI 协作动作：**
- Prompt：「请撰写 Related Work 部分，分为 6 个子节：(1) Chain-of-Thought and Reasoning Enhancement；(2) Program-augmented Reasoning；(3) Neural Theorem Proving；(4) Neuro-symbolic Systems；(5) Reliability Evaluation；(6) Auto-formalization。每个子节需要引用至少 2 篇文献，并说明我们的工作与它们的区别。」
- AI 输出：生成了 6 个子节的相关工作，每个子节引用 2-4 篇文献，并在每节末尾说明了与我们工作的区别。
- **人工核验**：
  - 所有引用的文献均在 references.bib 中存在且信息准确。
  - "我们的工作与它们的区别"部分表述合理：CoT 缺少验证层、PoT 只做部分规约、神经定理证明需要预形式化输入等。
  - Neuro-symbolic Systems 子节中 AlphaGeometry 和 AlphaProof 的描述与原文一致。

- Prompt：「请撰写 Applications 部分，包括 4 个应用场景：(1) Automated Theorem Proving；(2) Mathematical Problem Solving；(3) AI-assisted Mathematics Education；(4) Mathematical Research Assistance。每个场景需要说明 pipeline 如何运作。」
- AI 输出：生成了 4 个应用场景，每个场景用编号列表说明了 pipeline 的具体运作步骤。
- **人工核验**：应用场景的描述与框架的 pipeline 一致，逻辑合理。教育场景中"精确定位错误步骤"是 TIR 框架的合理推论。

### 下午：实验设计与讨论

**AI 协作动作：**
- Prompt：「请撰写 Experimental Design 部分，包括：(1) 3 个数据集（GSM8K, MATH, MiniF2F）；(2) 5 个 baseline；(3) 3 个 metrics 的形式化定义（Accuracy, Verifiability, Consistency）；(4) 4 个 hypotheses；(5) 预期结果表格。」
- AI 输出：生成了完整的实验设计部分，包含数据集描述、baseline 列表、三个 metric 的数学定义、四个假设、预期结果表格。
- **人工核验**：
  - GSM8K 的数据量（8,500）和 MATH 的数据量（12,500）与原始论文一致。
  - MiniF2F 的问题数（488）与原始论文一致。
  - Verifiability metric 的定义是我们原创的，表述清晰。
  - 预期结果表格中的数值是定性描述（high/medium/low）而非编造具体数字，合理。

- Prompt：「请撰写 Discussion 部分，包括 Limitations（5 条）、Extensions（4 条）、Broader Implications。」
- AI 输出：生成了讨论部分，包含 5 条局限性、4 条扩展方向、以及更广泛影响的论述。
- **人工核验**：局限性中"概念论文，未实现"这一点诚实且重要，保留。扩展方向中的 multi-agent 引用了 MA-LoT，文献存在。

**AI 生成结论的人工核验记录：**
| AI 生成内容 | 核验方式 | 结果 |
|---|---|---|
| GSM8K 8,500 题 | 对照 Cobbe et al. 2021 | ✅ |
| MATH 12,500 题 | 对照 Hendrycks et al. 2021 | ✅ |
| MiniF2F 488 题 | 对照 Zheng et al. 2022 | ✅ |
| AlphaGeometry 25/30 IMO-AG-30 | 对照 Trinh et al. 2024 Nature | ✅ |
| AlphaProof IMO 银牌 | 对照 DeepMind 博客 + Nature 2025 | ✅ |

---

## Day 5 — 2026-09-29（周二）：结论、参考文献、编译验证

### 上午：结论与参考文献整理

**AI 协作动作：**
- Prompt：「请撰写 Conclusion 部分，总结核心论点和 4 个贡献，展望未来方向。」
- AI 输出：生成了约 300 词的结论，总结了三层框架、语义规约瓶颈、TIR 设计、双向管道，并展望了"自然语言作为接口、可验证核心"的未来。
- **人工核验**：结论与引言中的贡献点一一对应，没有引入新的未论证主张。

- Prompt：「请帮我整理 BibTeX 参考文献，确保每篇文献都有正确的 author、title、year、venue/arxiv 编号。需要包含论文中引用的所有文献。」
- AI 输出：生成了 24 条 BibTeX 条目。
- **人工核验**：
  - 逐条检查 BibTeX 语法（大括号匹配、逗号分隔、字段名正确）。
  - 逐条核对 arXiv 编号是否正确（在 arXiv.org 搜索验证）。
  - AlphaProof 的条目已修正为 Nature 2025。
  - 发现 AI 生成的一条文献作者列表不完整，已补充。

### 下午：LaTeX 编译验证

**AI 协作动作：**
- Prompt：「请帮我检查 paper.tex 中可能的 LaTeX 编译错误，包括：(1) 未定义的引用；(2) 缺少的包；(3) tikz 语法错误；(4) algorithm 环境语法；(5) 数学公式语法。」
- AI 输出：列出了 3 个潜在问题：(1) algorithmic 包需要确认已加载；(2) tikz arrows.meta 库需要确认；(3) hyperref 应该在最后加载。
- **人工核验与修复**：
  - algorithmic 包已在 preamble 中加载 ✅
  - tikz arrows.meta 库已加载 ✅
  - hyperref 的加载位置——实际上 hyperref 通常应该在大多数包之后但在某些包之前。当前位置（geometry 之后）是合理的，未修改。
- 实际运行 `pdflatex paper.tex` 进行编译验证（详见编译验证部分）。

**编译验证记录：**
```
命令：pdflatex -interaction=nonstopmode paper.tex
运行次数：2 次（解析引用需要）
结果：编译成功，生成 paper.pdf
警告：存在 overfull hbox（不影响编译），无 error
```

---

## AI 使用总结

### Prompt 迭代统计
| 天数 | Prompt 轮次 | 主要用途 |
|---|---|---|
| Day 1 | 2 | 任务解读、选题确定 |
| Day 2 | 3 | 文献检索（2轮）、批判性阅读（1轮） |
| Day 3 | 4 | 引言、三层模型、瓶颈分析、框架设计 |
| Day 4 | 4 | 相关工作、应用、实验设计、讨论 |
| Day 5 | 3 | 结论、参考文献、编译检查 |
| **合计** | **16** | |

### AI 结论人工核验率
- 文献引用：100% 逐篇核验（24/24）
- 事实陈述：100% 核验（所有具体数字、系统性能、发表信息）
- 推理性结论：抽样核验（与原文方法描述对照）
- 发现并修正 AI 错误：3 处（AlphaProof 发表信息、GPT-4 准确率数字、AlphaProof 奖牌等级）

### AI 工作流设计
1. **检索 → 核验 → 写入**：所有文献先检索，再人工核验，最后写入 bib
2. **生成 → 审查 → 修改**：所有正文先 AI 生成，再人工逐段审查修改
3. **编译 → 修复 → 重编译**：LaTeX 先编译，根据报错修复，再重编译验证
4. **交叉验证**：关键事实至少在两个独立来源验证（如 arXiv + 官方博客）
