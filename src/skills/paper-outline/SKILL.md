---
name: paper-outline
description: Use when creating, revising, validating, or repairing a research-paper outline before writing; turns experiment evidence into a clear paper idea, scoped claims, method abstraction, evaluation plan, analysis plan, and evidence boundaries without copying run logs into the manuscript.
skill_role: companion
---

# Paper Outline

Use this before `write` when the outline feels like a run log, result dump, engineering note, or group-meeting report instead of a paper plan.

## One-Sentence Summary

Keep one selected outline, but split two views:

- `paper_view`: what the paper will say to readers.
- `evidence_view`: where the exact runs, paths, rows, settings, and reproducibility details live.

The paper should be faithful to the actual evidence, but it should not repeat the agent workflow.

## Basic Workflow

1. Read the current paper state.
   Use `artifact.get_paper_contract(detail='full')`, `artifact.list_paper_outlines(...)`, and then `artifact.validate_academic_outline(detail='full')` if an outline exists.
2. Find the one-sentence paper idea.
   Ask: "What should a researcher remember after reading this paper?" This is not a metric row and not an implementation setting.
3. Separate facts from interpretation.
   Facts are measured results. Interpretations are the careful academic lesson supported by those facts. Unsupported claims go into "must not claim."
4. Write or repair `paper_view`.
   Fill the paper idea, problem/gap/method/result/limit, 1-3 scoped claims, method intuition, evaluation plan, and 4-8 useful analysis jobs.
5. Keep engineering details out of the story.
   Put ports, worktrees, batch shorthand, route decisions, user requests, artifact ids, exact file paths, and local commands into `evidence_view` or appendix-only reproducibility fields.
6. Validate and compile.
   Run `artifact.validate_academic_outline(detail='full')`. If it passes, run `artifact.compile_outline_to_writing_plan(detail='full')`.

## What Good Means

A good outline does three things:

- It has a point: one clear claim or lesson, not a list of what the agent did.
- It is honest: every claim is tied to durable evidence, and limits are explicit.
- It is useful to a reader: the method and analyses teach something beyond "this setup got a number."

Strong papers often start from simple code but make a useful idea legible. Residual connections are more than a code shortcut; the paper teaches how to make depth trainable. Attention is more than a module; the paper teaches how to remove a bottleneck. Do the same only when the quest evidence supports that kind of interpretation.

## Mature Outline Reminder

A mature paper outline is not just a section list. For `paper_type: full_empirical` and `outline_maturity: mature`, surface reminders when these are missing:

- a central thesis and a central insight that are reader-facing, not just metric summaries
- an `insight_ladder` showing how observed facts become allowed interpretations
- 1-3 scoped claims, each with `evidence_needed` and `what_would_falsify_it`
- a closest-neighbor / novelty boundary explaining what the paper is and is not claiming against prior or obvious alternatives
- at least three likely reviewer objections, each mapped to planned evidence, manuscript revision, claim downgrade, or accepted limitation
- 4-8 reviewer-facing analysis jobs beyond the headline result unless an explicit analysis-budget waiver downgrades the paper scope

Analysis quantity has two reminder levels:

- `paper_view.analysis_plan`: normally 4-8 planned analysis jobs for a mature empirical paper.
- paper-facing evidence package: normally 5-10 ready experiment/analysis groups total before treating the manuscript as strong. If the user specifies a number such as 4-8 analyses, track that target visibly until completed, waived, or explicitly downgraded.

## Required Shape

Use this inside `artifact.submit_paper_outline(..., detailed_outline={...})`.

```json
{
  "paper_view": {
    "paper_type": "full_empirical",
    "outline_maturity": "mature",
    "working_title": "Paper-native title",
    "narrative_strategy": {
      "central_thesis": "The one idea the paper wants readers to remember",
      "central_insight": "The reusable lesson suggested by the evidence",
      "reader_takeaway": "What another researcher can learn or reuse"
    },
    "insight_ladder": [
      {
        "level": "Observed fact -> interpretation",
        "statement": "What this fact teaches",
        "evidence": ["main-result-id"],
        "claim_links": ["C1"],
        "risk": "What could make the interpretation too strong"
      }
    ],
    "story_spine": {
      "problem": "What scientific problem exists?",
      "gap": "What prior/easy approach fails to address?",
      "method": "What abstract method is introduced?",
      "main_result": "What measured result supports the claim?",
      "scope_limit": "Where the claim stops"
    },
    "positioning": {
      "closest_neighbor": "The closest existing method, baseline, or obvious alternative",
      "novelty_boundary": "Exactly what is new or reusable here",
      "not_claiming": ["Claims this paper does not make"]
    },
    "core_claims": [
      {
        "claim_id": "C1",
        "claim": "A scoped claim, not a section summary",
        "scope": "Dataset/model/setting boundary",
        "evidence_needed": ["main-result-id", "analysis-id"],
        "what_would_falsify_it": "A result pattern that would weaken the claim"
      }
    ],
    "method_abstraction": {
      "paper_name": "Method name if stable",
      "intuition": "Why the method should work",
      "mechanism_steps": ["Step 1", "Step 2", "Step 3"],
      "appendix_only_details": ["local serving topology", "exact batch/query budget"]
    },
    "evaluation_plan": {
      "setting": "The scientific evaluation setting",
      "datasets_or_benchmarks": [],
      "baselines": [],
      "metrics": [],
      "controlled_factors": []
    },
    "analysis_plan": [
      {
        "analysis_id": "A1",
        "title": "Component ablation",
        "analysis_role": "component ablation",
        "reviewer_question": "Does the claimed mechanism actually cause the gain?",
        "claim_links": ["C1"],
        "target_display": "Main-text ablation table",
        "main_or_appendix": "main_text",
        "failure_interpretation": "How the claim should change if this fails"
      }
    ],
    "reviewer_objections": [
      {
        "objection": "Why a skeptical reviewer might reject or downgrade the paper",
        "answer_route": "analysis | writing | claim_downgrade | limitation",
        "linked_claims": ["C1"],
        "needed_evidence": ["analysis-id"]
      }
    ],
    "evidence_grounding": {
      "observed_facts": ["Facts directly visible in durable results"],
      "allowed_interpretations": ["Careful interpretations allowed by the facts"],
      "must_not_claim": ["Claims the paper must avoid"],
      "evidence_gaps": ["Missing checks or unresolved risks"]
    }
  },
  "evidence_view": {
    "claim_to_items": [],
    "sections": [],
    "unmapped_items": [],
    "appendix_reproducibility": []
  }
}
```

The field names are machine-facing. The thinking should stay simple:

- `central_thesis`: one-sentence paper idea.
- `central_insight`: what readers learn.
- `story_spine`: problem -> gap -> method -> result -> limit.
- `evidence_grounding`: facts, allowed interpretations, and things not to claim.
- `analysis_plan`: the checks a reviewer would ask for.

## Math Modeling Paper Type / 数学建模论文类型

When the paper is a mathematical modeling paper (数学建模论文, MCM/ICM, CUMCM), set `paper_type: "math_modeling"` instead of `"full_empirical"`.

### Math Modeling Outline Schema / 数学建模大纲结构

Use this schema inside `artifact.submit_paper_outline(..., detailed_outline={...})` when `paper_type: "math_modeling"`:

```json
{
  "paper_view": {
    "paper_type": "math_modeling",
    "outline_maturity": "mature",
    "working_title": "Paper-native title / 论文标题",
    "problem_source": "Contest year + problem name or URL / 竞赛题目来源",
    "subproblems": [
      {
        "problem_id": "P1",
        "label": "问题一",
        "description": "Original problem text / 原始问题描述",
        "type": "optimization | prediction | evaluation | classification | other",
        "data_available": true,
        "data_description": "Available data description / 可用数据描述"
      }
    ],
    "narrative_strategy": {
      "central_thesis": "The one idea the paper wants readers to remember",
      "central_insight": "The reusable lesson suggested by the model"
    },
    "story_spine": {
      "problem": "The real-world problem to solve",
      "gap": "Why simple approaches fail",
      "method": "The mathematical model approach",
      "main_result": "The key numerical or structural result",
      "scope_limit": "Where the model stops being applicable"
    },
    "models": [
      {
        "model_id": "M1",
        "target_subproblem": "P1",
        "model_name": "Model name / 模型名称",
        "model_type": "linear_programming | nonlinear_programming | differential_equation | statistical | graph | simulation | etc.",
        "decision_variables": ["x1 description", "x2 description"],
        "parameters": ["alpha description", "beta description"],
        "objective_function": "Objective function description / 目标函数描述",
        "constraints": ["Constraint 1 description", "Constraint 2 description"],
        "solution_method": "Algorithm + software / 算法 + 软件",
        "validation_method": "How to validate this model / 验证方法"
      }
    ],
    "sensitivity_analysis_plan": {
      "parameters_to_test": ["alpha", "beta"],
      "range": "Test range for each parameter",
      "expected_behavior": "Expected result pattern"
    },
    "strengths_weaknesses_plan": {
      "expected_strengths": ["Strength 1", "Strength 2"],
      "expected_weaknesses": ["Weakness 1", "Weakness 2"],
      "improvement_directions": ["Direction 1"]
    },
    "notation_plan": {
      "categories": ["indices", "sets", "variables", "parameters", "functions"],
      "completeness_rule": "Every variable in every formula must appear in notation table"
    },
    "data_sources": [
      {
        "source": "Problem statement / 题目提供",
        "description": "Data provided in contest problem",
        "reliability": "assumed_reliable"
      }
    ],
    "expected_figures_tables": [
      {
        "fig_id": "F1",
        "type": "table",
        "content": "Notation table / 符号说明表",
        "placement": "notation_section"
      },
      {
        "fig_id": "F2",
        "type": "figure",
        "content": "Sensitivity curve / 灵敏度曲线",
        "placement": "sensitivity_analysis"
      }
    ],
    "appendix_plan": [
      "Code listings / 代码清单",
      "Supplementary derivations / 补充推导",
      "Full result tables / 完整结果表"
    ],
    "evidence_grounding": {
      "observed_facts": ["Problem conditions", "Provided data", "Assumptions"],
      "allowed_interpretations": ["Model implications", "Sensitivity conclusions"],
      "must_not_claim": ["Fabricated data", "Fake references", "Unverified external facts"],
      "evidence_gaps": ["Uncertain assumptions", "Data limitations"]
    }
  }
}
```

### Math Modeling Outline Validation / 数学建模大纲验证

Before handing to `write`, check:

- [ ] `paper_type` is `math_modeling`, not `full_empirical`
- [ ] All sub-problems from the original question are identified
- [ ] Each sub-problem has a corresponding model planned
- [ ] Notation plan covers all variable categories
- [ ] Sensitivity analysis plan is explicit
- [ ] Data sources are documented
- [ ] Appendix plan includes code and supplementary derivations
- [ ] The outline does NOT force Introduction/Related Work/Method/Experiments structure
- [ ] The outline does NOT require 4-8 analysis jobs or empirical paper rules

### Math Modeling Distinct from Full Empirical / 与经验型论文的区别

| Aspect | math_modeling | full_empirical |
|--------|:-------------:|:---------------:|
| Structure | Problem→Assumptions→Notation→Model→Solution→Sensitivity→Strengths→Conclusion | Intro→Related Work→Method→Experiments→Analysis→Conclusion |
| Evidence | Problem conditions, data, model derivation, sensitivity | Experimental results, ablation studies, benchmarks |
| Related Work | Optional, only if user requests | Usually required |
| Analysis count | Sensitivity analysis, not 4-8 analysis jobs | 4-8 analysis jobs expected |
| Reference count | 5-15 | 30-50 |
| Template | `templates/math_modeling/` | `templates/iclr2026/` or venue-specific |

## Analysis Plan

A mature empirical paper usually needs 4-8 analysis jobs beyond the main result. Choose them because they support the story, not because of a fixed checklist.

Useful analysis roles:

- component ablation
- robustness or sensitivity
- stronger-baseline comparison
- subgroup or case breakdown
- failure taxonomy
- mechanism or attribution check
- cost, budget, or efficiency tradeoff
- limitation or residual headroom analysis

If there are fewer than 4, mark `outline_maturity: "idea_seed"` or provide `analysis_budget_waiver` with a real reason.

## Bad To Good Examples

Bad:

- "The abstract reports dual ports and 64+64."

Good:

- "All methods are compared under the same evidence budget; the exact serving setup is appendix-only."

Bad:

- "The latest route selected outline-008 and reran opposite-port probes."

Good:

- "The method performs an independent evidence pass and updates a decision only when the new support satisfies preset checks."

Bad:

- "Section 3 reports all experiments and Section 4 reports more experiments."

Good:

- "The main result tests whether the method improves the target task. The analyses then ask why: whether the gain comes from the proposed component, whether it survives stronger baselines, where it fails, and what budget it costs."

Bad:

- "We did only two follow-up analyses because those were the latest completed runs."

Good:

- "The outline plans six follow-ups: ablation, stronger baseline, sensitivity, failure taxonomy, subgroup breakdown, and cost. If only two can be run, the paper is marked early/narrow instead of mature."

## Validation

Before handing to `write`, check:

- `artifact.validate_academic_outline(detail='full')` passes.
- The paper has one clear idea and 1-3 scoped claims.
- If the outline is mature/full-empirical, `insight_ladder`, novelty boundary, reviewer objections, claim falsification criteria, and analysis-count reminders are present or explicitly waived.
- The outline says what was observed, what can be interpreted, and what must not be claimed.
- The analysis plan has 4-8 useful jobs, or a waiver.
- Main-text experiment/analysis item ids are checked for stale duplicates that inflate evidence count.
- `paper_view` does not mention quest, worktree, selected outline, route history, user requests, ports, or `64+64`.
- Exact engineering details are in `evidence_view` or appendix-only fields.

Read `references/outline-patterns.md` when you need more examples.
