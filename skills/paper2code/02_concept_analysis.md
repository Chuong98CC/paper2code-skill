# Phase 2: Concept Analysis

## Goal
Understand the **overall structure** of the research paper and identify **all elements that must be implemented** for a successful reproduction.

---

## ⚠️ DO / DON'T Guidelines (CRITICAL)

```
DO:
✓ Systematically map every section of the paper
✓ Understand the data flow and dependencies between all components
✓ Identify all environments/datasets/baselines used in the experiments
✓ Define success criteria with concrete numbers
✓ Assess implementation complexity and priority

DON'T:
✗ Do not confuse Related Work with implementation requirements
✗ Do not use abstract success criteria (e.g. "good performance")
✗ Do not omit relationships between components
✗ Do not skip variants required for the ablation study
```

---

## ⚠️ Output Format Restrictions

```
⚠️ MANDATORY OUTPUT FORMAT:
- Output in YAML format only
- Pure YAML only, with no markdown explanation or preamble
- All required fields must be filled in
- Include concrete numbers and sources

Output start: "```yaml"
Output end: "```"
```

---

## Analysis Protocol

### 1. Paper Structure Analysis
Create a complete map of the paper:

```yaml
paper_structure_map:
  title: "[full paper title]"

  sections:
    1_introduction:
      main_claims: "[what the paper claims to have achieved]"
      problem_definition: "[the exact problem being solved]"

    2_related_work:
      key_comparisons: "[methods this work builds on or competes with]"

    3_method:  # multiple subsections possible
      subsections:
        3.1: "[title and main content]"
        3.2: "[title and main content]"
      algorithms_presented: "[list of all algorithm names]"

    4_experiments:
      environments: "[all test environments/datasets]"
      baselines: "[all comparison methods]"
      metrics: "[all evaluation metrics used]"

    5_results:
      main_findings: "[key results proving the method works]"
      tables_figures: "[important result tables/figures to reproduce]"
```

### 2. Method Decomposition
For the main method/approach:

```yaml
method_decomposition:
  method_name: "[full name and abbreviation]"

  core_components:  # decompose into implementable pieces
    component_1:
      name: "[e.g. State Importance Estimator]"
      purpose: "[why this component exists]"
      paper_section: "[where it is described]"

    component_2:
      name: "[e.g. Policy Refinement Module]"
      purpose: "[its role in the system]"
      paper_section: "[where it is described]"

  component_interactions:
    - "[how component 1 is passed to component 2]"
    - "[data flow between components]"

  theoretical_foundation:
    key_insight: "[key theoretical insight]"
    why_it_works: "[intuitive explanation]"
```

### 3. Implementation Requirements Mapping
Map the paper's content to code requirements:

```yaml
implementation_map:
  algorithms_to_implement:
    - algorithm: "[name in the paper]"
      section: "[where it is defined]"
      complexity: "[Simple/Medium/Complex]"
      dependencies: "[what is needed for it to work]"

  models_to_build:
    - model: "[neural network or other model]"
      architecture_location: "[section describing it]"
      purpose: "[what this model does]"

  data_processing:
    - pipeline: "[required data preprocessing]"
      requirements: "[what the data should look like]"

  evaluation_suite:
    - metric: "[metric name]"
      formula_location: "[where it is defined]"
      purpose: "[what it measures]"
```

### 4. Experiment Reproduction Plan
Identify **all** required experiments:

```yaml
experiments_analysis:
  main_results:
    - experiment: "[name/description]"
      proves: "[the claim this validates]"
      requires: "[components needed to run it]"
      expected_outcome: "[concrete numbers/trends]"

  ablation_studies:
    - study: "[what is removed]"
      purpose: "[what this shows]"

  baseline_comparisons:
    - baseline: "[method name]"
      implementation_required: "[Yes/No/Partial]"
      source: "[where to find an implementation]"
```

### 5. Key Success Factors
Definition of a successful reproduction:

```yaml
success_criteria:
  must_achieve:
    - "[main results that must be reproduced]"
    - "[key behaviors that must be demonstrated]"

  should_achieve:
    - "[additional results validating the method]"

  validation_evidence:
    - "[specific figures/tables to reproduce]"
    - "[qualitative behaviors to demonstrate]"
```

---

## Output Format

```yaml
comprehensive_paper_analysis:
  executive_summary:
    paper_title: "[full title]"
    core_contribution: "[one-sentence summary]"
    implementation_complexity: "[Low/Medium/High]"
    estimated_components: "[number of main components to build]"

  complete_structure_map:
    # full section decomposition from above

  method_architecture:
    # detailed component decomposition

  implementation_requirements:
    # all algorithms, models, data, metrics

  reproduction_roadmap:
    phase_1: "[what to implement first]"
    phase_2: "[what to build next]"
    phase_3: "[final components and validation]"

  validation_checklist:
    - "[ ] [specific results to achieve]"
    - "[ ] [behaviors to demonstrate]"
    - "[ ] [metrics to match]"
```

---

## Important Principles

1. **Be thorough**: Do not miss anything. The output must be a complete blueprint for reproduction
2. **Structure**: Break down every part of the paper into implementable pieces
3. **Identify relationships**: Clarify dependencies and data flow between components
4. **Specify validation criteria**: Define what counts as a "successful reproduction"
5. **Set priorities**: Distinguish core contributions from secondary elements

---

## ⚠️ Self-Check: Mandatory Verification Before Completion

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ SELF-CHECK BEFORE FINISHING (all must be YES to complete)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Paper structure analysis check:
□ Are all Method sections mapped?                            → YES / NO
□ Are all algorithm names listed?                            → YES / NO
□ Are all experiments in the Experiments section identified? → YES / NO

Component analysis check:
□ Are inputs/outputs of all components defined? → YES / NO
□ Is the data flow between components clear?    → YES / NO
□ Is the dependency order identified?           → YES / NO

Experiment requirements check:
□ Are all environments/datasets identified? → YES / NO
□ Are all baseline methods identified?      → YES / NO
□ Are all evaluation metrics defined?       → YES / NO
□ Are ablation study variants identified?   → YES / NO

Success criteria check:
□ Do must_achieve items include concrete numbers?     → YES / NO
□ Are specific tables/figures to reproduce specified? → YES / NO

Output format check:
□ Is the output in pure YAML format? → YES / NO
□ Are all required fields filled in? → YES / NO

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ If even one is NO, keep analyzing until it is complete!
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
