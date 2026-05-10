---
name: math-modeling
description: Use when the user wants to write a mathematical modeling paper, MCM/ICM-style paper, or CUMCM (全国大学生数学建模竞赛) style paper. Triggers on keywords: 数学建模论文, mathematical modeling paper, MCM/ICM, 建模竞赛论文, optimization/prediction/evaluation modeling report.
skill_role: companion
---

# Math Modeling Paper / 数学建模论文

## Match Signals / 触发条件

Use this skill when the user task matches one or more of:
- 数学建模论文 / mathematical modeling paper
- MCM / ICM paper / MCM-ICM style paper
- 全国大学生数学建模竞赛论文 / CUMCM paper
- 建模竞赛论文 / modeling competition paper
- 优化模型 / optimization model
- 预测模型 / prediction model
- 评价模型 / evaluation model
- 综合评价类建模报告 / comprehensive evaluation modeling report
- A paper whose core structure is: 问题重述、模型假设、符号说明、模型建立、模型求解、灵敏度分析、模型优缺点
- A paper whose central evidence comes from model construction, solution derivation, and sensitivity analysis rather than empirical benchmarking

Do NOT use this skill for:
- Standard AI/ML empirical papers (ICLR/NeurIPS/ICML style)
- Systems papers (OSDI/NSDI style)
- Papers whose primary contribution is a new neural architecture, training method, or benchmark result

## Core Distinction from AI/ML Empirical Papers / 与AI/ML经验型论文的核心区别

| Aspect | AI/ML Empirical Paper | Math Modeling Paper |
|--------|----------------------|---------------------|
| Core contribution | New method, architecture, or empirical finding | Model construction and solution for applied problem |
| Structure | Introduction / Related Work / Method / Experiments / Analysis / Conclusion | 问题重述 / 模型假设 / 符号说明 / 模型建立 / 模型求解 / 灵敏度分析 / 结论 |
| Evidence type | Experimental results, ablation studies, benchmarks | Model derivation, constraints, solution steps, sensitivity checks |
| "Related Work" | Usually required | Only include if user requests literature review |
| Claims | Supported by experimental data | Supported by model logic, data sources, and sensitivity analysis |
| Figures/Tables | Experimental result plots, comparison tables | Model diagrams, flowcharts, result tables, sensitivity curves |
| Appendices | Hyperparameters, extra experiments | Code listings, data processing, supplementary derivations |

## Required Paper Structure / 必含论文结构

A mathematical modeling paper should typically contain the following sections in order:

1. **标题 / Title** — Concise description of problem and method
2. **摘要 / Abstract** — Must include: 研究问题 + 使用模型 + 求解方法 + 主要结果 + 结论建议
3. **关键词 / Keywords** — 3-8 keywords
4. **问题重述 / Problem Restatement** — Restate the original problem in your own words
5. **问题分析 / Problem Analysis** — Break down the problem into sub-problems; analyze each
6. **模型假设 / Model Assumptions** — List all assumptions explicitly; each must be used or justified later
7. **符号说明 / Notation** — Every variable appearing in formulas must be explained here
8. **模型建立 / Model Construction** — Build the mathematical model: objective function, constraints, variables
9. **模型求解 / Model Solution** — Solve the model: algorithm, steps, software, convergence proof if applicable
10. **模型检验或验证 / Model Validation** — Validate the model: back-testing, error analysis, comparison to known values
11. **灵敏度分析 / Sensitivity Analysis** — Test how results change when key parameters vary
12. **模型优缺点 / Strengths & Weaknesses** — Objective assessment; do not oversell
13. **结论 / Conclusion** — Summarize findings; answer every sub-problem from the original question
14. **参考文献 / References** — Only real or explicitly marked placeholder citations
15. **附录 / Appendix** — Code, data processing details, supplementary derivations

## Writing Rules / 写作规则

### 1. Abstract Checklist / 摘要检查清单
The abstract must answer:
- What is the research problem? / 研究什么问题？
- What model was used? / 用了什么模型？
- How was it solved? / 如何求解？
- What are the main results? / 主要结果是什么？
- What are the conclusions/recommendations? / 结论和建议是什么？

### 2. Variable Documentation / 变量说明
- Every variable in every formula must appear in the notation table / 符号表
- Notation table format: 符号 | 含义 | 单位 (if applicable)
- Example: $x_{ij}$ | 第 $i$ 个样本的第 $j$ 个指标值 | —

### 3. Assumption Discipline / 假设纪律
- Each assumption must be:
  - Reasonable / 合理
  - Used in the model / 在后续模型中被使用
  - Declared before model construction / 在建模前声明
- If an assumption is never used, remove it
- If an assumption is used but not declared, add it

### 4. Problem-Solution Mapping / 问题与解答对应
- Each sub-problem from the original question must have a corresponding model and result
- 如果题目有问题一、问题二、问题三，必须分别建模和求解
- The conclusion must revisit each sub-problem

### 5. Data Integrity / 数据诚信
- NEVER fabricate data / 禁止编造数据
- NEVER fabricate experimental results / 禁止伪造实验结果
- NEVER fabricate references / 禁止编造不存在的参考文献
- If data is assumed or estimated, state this explicitly
- If data comes from public sources, cite them

### 6. Model Completeness / 模型完整性
Each model should specify:
- Decision variables / 决策变量
- Objective function / 目标函数
- Constraint conditions / 约束条件
- Parameters / 参数
- Solution method / 求解方法
- Validation method / 验证方法

### 7. Language / 语言
- Default: Chinese mathematical modeling paper style / 中文数学建模论文风格
- If user requests English: English MCM/ICM style
- Use formal academic language in the target language

### 8. LaTeX Template / LaTeX 模板
- Default template: `templates/math_modeling/`
- Uses `ctexart` for Chinese support (pdflatex + ctex or xelatex)
- Main entry: `main.tex`
- Section files go in `sections/`

## Workflow / 工作流

1. **Identify the task** — Confirm this is a math modeling paper, not an AI/ML empirical paper
2. **Analyze the problem** — Break the original problem into sub-problems
3. **Create outline** — Use `paper-outline` with `paper_type: math_modeling`
4. **Draft sections** — Write each section following the structure above
5. **Check completeness** — Verify all chapters present, all variables documented, all assumptions used
6. **Verify data integrity** — Confirm no fabricated data, results, or references
7. **Compile LaTeX** — Ensure `main.tex` compiles cleanly
8. **Finalize** — Run the math modeling finalization checks

## Interaction with Other Skills

- **paper-outline**: Use `paper_type: math_modeling` (not `full_empirical`)
- **write**: Follow the math modeling section structure; use `templates/math_modeling/`
- **review**: Apply the math modeling review checklist
- **finalize**: Apply the math modeling final check

## AVOID / Pitfalls / 避免事项

- Do NOT force the paper into Introduction / Related Work / Method / Experiments structure
- Do NOT require "experimental results" like an AI paper — model derivation and sensitivity analysis are the evidence
- Do NOT require Related Work unless the user explicitly requests it
- Do NOT fabricate data — if the problem provides data, use it; if not, state assumptions
- Do NOT fabricate references — mark placeholder references explicitly
- Do NOT skip sensitivity analysis — it is a core requirement
- Do NOT leave variables undefined in the notation table
- Do NOT write abstract before the paper body is stable
- Do NOT apply "5-10 experiment groups" or "4-8 analysis jobs" rules from empirical papers
