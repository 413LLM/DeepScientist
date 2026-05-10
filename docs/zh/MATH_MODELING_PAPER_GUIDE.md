# 数学建模论文写作指南 / Math Modeling Paper Guide

## 简介 / Introduction

DeepScientist 现已支持数学建模论文的生成和写作。本指南说明如何使用该功能。

当你的任务是写一篇数学建模论文（如 MCM/ICM 论文、全国大学生数学建模竞赛论文等）时，DeepScientist 会自动进入数学建模模式，使用专门的章节结构和写作规则，而不是默认的 AI/ML 经验型论文格式。

## 如何启动数学建模论文任务 / How to Start a Math Modeling Paper

### 推荐用户 Prompt 示例 / Recommended Prompts

**中文：**

```
请帮我写一篇数学建模竞赛论文。题目是 [题目描述]。
要求包含问题重述、模型假设、符号说明、模型建立、模型求解、灵敏度分析和模型优缺点。
```

```
请使用 MCM/ICM 风格写一篇建模论文，题目是 [提供题目数据或链接]。
```

```
帮我写 2024 年全国大学生数学建模竞赛 A 题论文。
```

**English:**

```
Write a mathematical modeling paper in MCM style for the following problem: [problem description].
Include problem restatement, assumptions, notation, model construction, solution, sensitivity analysis, and strengths/weaknesses.
```

```
Help me write a CUMCM-style paper for Contest Problem C of 2025.
```

### 触发关键词 / Trigger Keywords

DeepScientist 通过识别以下关键词自动进入数学建模模式：

| 中文关键词 | English Keywords |
|-----------|-----------------|
| 数学建模论文 | mathematical modeling paper |
| 数学建模竞赛 | MCM / ICM paper |
| 全国大学生数学建模竞赛 | CUMCM paper |
| 建模竞赛论文 | modeling competition paper |
| 优化模型 / 预测模型 / 评价模型 | optimization/prediction/evaluation model |

## 模板位置 / Template Location

数学建模论文的 LaTeX 模板位于：

```
src/skills/write/templates/math_modeling/
```

目录结构：

```
math_modeling/
├── main.tex                     # 主文件，可独立编译
├── references.bib               # 参考文献（占位符）
├── README.md                    # 模板使用说明
└── sections/
    ├── abstract.tex             # 摘要
    ├── problem_restatement.tex  # 问题重述
    ├── problem_analysis.tex     # 问题分析
    ├── assumptions.tex          # 模型假设
    ├── notation.tex             # 符号说明
    ├── model_construction.tex   # 模型建立
    ├── model_solution.tex       # 模型求解
    ├── validation.tex           # 模型检验
    ├── sensitivity_analysis.tex # 灵敏度分析
    ├── strengths_weaknesses.tex # 模型优缺点
    ├── conclusion.tex           # 结论
    └── appendix.tex             # 附录
```

## 支持的章节结构 / Supported Section Structure

数学建模论文的默认章节顺序：

1. **标题 / Title**
2. **摘要 / Abstract** — 必须包含：研究问题、使用模型、求解方法、主要结果、结论建议
3. **关键词 / Keywords**
4. **问题重述 / Problem Restatement** — 用自己的话重述问题
5. **问题分析 / Problem Analysis** — 将问题拆解为子问题
6. **模型假设 / Model Assumptions** — 每个假设必须在后文被使用
7. **符号说明 / Notation** — 每个公式变量必须出现在符号表中
8. **模型建立 / Model Construction** — 目标函数、约束条件、决策变量
9. **模型求解 / Model Solution** — 算法、步骤、软件、收敛性
10. **模型检验 / Model Validation** — 回代检验、误差分析
11. **灵敏度分析 / Sensitivity Analysis** — 关键参数变化时的结果稳定性
12. **模型优缺点 / Strengths & Weaknesses** — 客观评价
13. **结论 / Conclusion** — 逐问题回答
14. **参考文献 / References** — 真实引用或标注为 placeholder
15. **附录 / Appendix** — 代码、数据处理、推导补充

## 与其他科研论文模式的区别 / Difference from Academic Paper Mode

| 特征 | AI/ML Empirical Paper | Math Modeling Paper |
|------|----------------------|---------------------|
| 核心结构 | Intro → Related Work → Method → Experiments → Analysis → Conclusion | 问题重述 → 假设 → 符号 → 建模 → 求解 → 灵敏度 → 优缺点 → 结论 |
| Related Work | 通常必含 | 可选，仅在用户要求时写 |
| 证据类型 | 实验数据、消融实验、benchmark | 模型推导、约束条件、灵敏度分析 |
| 分析数量 | 4-8 个分析任务 | 主要靠灵敏度分析 |
| 参考文献数 | 30-50 | 5-15 |
| 默认模板 | `templates/iclr2026/` | `templates/math_modeling/` |
| 语言 | 英文 (English) | 中文为主 (Primarily Chinese) |

## 重要注意事项 / Important Notes

### 数据诚信 / Data Integrity

- **禁止编造数据** — 如果题目提供了数据，使用题目数据；如果没有，应说明假设
- **禁止伪造实验结果** — 所有数值结果必须来自真实的模型计算
- **禁止编造参考文献** — 如果使用模板中的 placeholder 引用，必须明确标注为 `[PLACEHOLDER]`

### 写作要求 / Writing Requirements

- 每个数学公式中的变量都必须在符号表中解释
- 每个模型假设必须在后续模型中被使用，否则应删除
- 每个子问题必须有对应的模型和求解结果
- 结论必须逐一回顾题目中的每个问题并给出答案
- 灵敏度分析是必含项，不能省略

### 编译 / Compilation

使用 `xelatex`（推荐用于中文）：
```bash
xelatex main.tex
bibtex main
xelatex main.tex
xelatex main.tex
```

或使用 `latexmk`：
```bash
latexmk -xelatex main.tex
```

## 从普通科研论文切换到数学建模模式 / Switching Modes

如果当前 quest 是普通科研论文模式，可以通过以下方式切换到数学建模论文模式：

1. 在用户 prompt 中明确说明要写数学建模论文
2. 包含触发关键词（如"数学建模论文"、"MCM"等）
3. DeepScientist 会自动：
   - 使用 `math-modeling` skill
   - 选择 `templates/math_modeling/` 模板
   - 应用数学建模的章节结构和写作规则

如果自动检测未生效，可以手动指定：
```
请使用 math-modeling skill 写一篇数学建模论文。
```

## Skill 位置 / Skill Location

数学建模 skill 位于：

```
src/skills/math-modeling/SKILL.md
```

该 skill 定义了完整的数学建模论文写作规则、章节要求和工作流程。

## 后续改进 / Future Improvements

1. 支持更多数学建模竞赛风格（如美赛 MCM B 题、C 题等不同类型的模板变体）
2. 自动从题目描述中提取子问题结构
3. 自动生成符号表（扫描全文中使用的变量）
4. 与 MATLAB/Lingo 等求解器的集成
5. 更多英文 MCM/ICM 风格的模板变体
