# Math Modeling LaTeX Template / 数学建模 LaTeX 模板

## 适用范围 / Applicable Scopes

This template is designed for:
- 数学建模论文 / Mathematical modeling papers
- MCM/ICM-style papers / MCM/ICM 风格论文
- 全国大学生数学建模竞赛论文 / CUMCM (China Undergraduate Mathematical Contest in Modeling) papers
- Other modeling competition papers / 其他建模竞赛论文

本模板适用于数学建模论文、MCM/ICM 论文和全国大学生数学建模竞赛论文。

## 结构说明 / Structure

```
math_modeling/
├── main.tex                     # 主文件 / Main entry — compiles independently
├── references.bib               # 参考文献 / References (placeholder entries)
├── README.md                    # 本文件 / This file
├── sections/                    # 章节文件 / Section files
│   ├── abstract.tex             # 摘要 / Abstract
│   ├── problem_restatement.tex  # 问题重述 / Problem Restatement
│   ├── problem_analysis.tex     # 问题分析 / Problem Analysis
│   ├── assumptions.tex          # 模型假设 / Model Assumptions
│   ├── notation.tex             # 符号说明 / Notation
│   ├── model_construction.tex   # 模型建立 / Model Construction
│   ├── model_solution.tex       # 模型求解 / Model Solution
│   ├── validation.tex           # 模型检验 / Model Validation
│   ├── sensitivity_analysis.tex # 灵敏度分析 / Sensitivity Analysis
│   ├── strengths_weaknesses.tex # 模型优缺点 / Strengths & Weaknesses
│   ├── conclusion.tex           # 结论 / Conclusion
│   └── appendix.tex             # 附录 / Appendix
```

## 编译 / Compilation

### pdflatex (if using ctex with UTF-8 support):
```bash
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

### xelatex (recommended for Chinese):
```bash
xelatex main.tex
bibtex main
xelatex main.tex
xelatex main.tex
```

### latexmk:
```bash
latexmk -pdf main.tex    # pdflatex
latexmk -xelatex main.tex # xelatex
```

## 注意事项 / Notes

1. **references.bib** 中的条目均为占位符（placeholder），不要当作真实引用。提交前请替换为真实文献。
   References in `references.bib` are placeholders. Replace them with real citations before submission.

2. 本模板使用 `ctexart` 文档类，支持中文排版。如需英文论文，可改用 `article` 文档类。
   This template uses `ctexart` for Chinese typesetting. For English-only papers, switch to `article` class.

3. 每个 `.tex` section 文件中的内容为占位示例，DeepScientist 可根据用户题目替换各章节内容。
   Each `.tex` section file contains placeholder content. DeepScientist will replace section content based on the user's problem.

4. 公式中的每个变量都必须在 `sections/notation.tex` 中的符号表里出现。
   Every variable in formulas must appear in the notation table in `sections/notation.tex`.

5. 每个模型假设都必须在后续章节中被使用或解释其必要性。
   Every model assumption must be used or justified in later chapters.

6. 不要伪造数据、结果或参考文献。
   Do not fabricate data, results, or references.
