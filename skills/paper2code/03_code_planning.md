# Phase 3: Creating the Implementation Plan (Code Planning)

## Goal
Integrate the results of Phase 1 (algorithm extraction) and Phase 2 (concept analysis) to generate a detailed plan that lets a developer implement the whole thing **without reading the paper**.

---

## ⚠️ Content Length Guidelines (STRICTLY FOLLOW)

```
📏 CONTENT BALANCE GUIDELINES:

Section 1 (file_structure):           ~800-1000 chars
Section 2 (implementation_components): ~3000-4000 chars  ← core section
Section 3 (validation_approach):       ~2000-2500 chars
Section 4 (environment_setup):         ~800-1000 chars
Section 5 (implementation_strategy):   ~1500-2000 chars

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📊 Total Target: 8000-10000 chars
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

⚠️ Section 2 is the most important! Include all algorithms, equations, and parameters
⚠️ If the length falls short, details are missing - check again
```

---

## Input
1. **Phase 1 results**: complete algorithm extraction (algorithm_extraction.yaml)
2. **Phase 2 results**: comprehensive paper analysis (concept_analysis.yaml)

---

## Planning Process

### 1. Information Integration
Combine **everything** from both analyses:
- All algorithms and pseudocode
- All components and architecture
- All hyperparameters and values
- All experiments and expected results

### 2. Implementation Mapping
Map each component to a concrete implementation:

```
[For each algorithm/component/method in the paper]:
  - What it does and where it is described in the paper
  - How to organize the code (files, classes, functions)
  - The specific equations, algorithms, and procedures required for implementation
  - Dependencies on and relationships with other components
  - The implementation approach appropriate for this paper
```

### 3. Extracting Technical Details
Collect all technical details relevant to the implementation:

```
[Collect all implementation-related details from the paper]:
  - All algorithms with complete pseudocode and mathematical formulation
  - All parameters, hyperparameters, and configuration values
  - All architecture details (where applicable)
  - All experimental procedures and evaluation methods
  - Any implementation hints, tricks, and special considerations mentioned
```

---

## Output Format: 5 Required Sections

```yaml
complete_reproduction_plan:
  paper_info:
    title: "[Full paper title]"
    core_contribution: "[Main innovation to reproduce]"

  # ============================================
  # Section 1: File Structure (~800-1000 chars)
  # ============================================
  # Design the file organization best suited to this paper
  # - Analyze the paper content (algorithms, models, experiments, systems, etc.)
  # - Organize files and directories in the most logical way for the implementation
  # - Meaningful names and groupings based on the paper content
  # - Clean, intuitive, and focused on the actual implementation
  # - Include documentation files (README.md, requirements.txt) but implement them last

  file_structure: |
    project_name/
    ├── main.py                    # Main entry point
    ├── config.py                  # Configuration and hyperparameters
    ├── models/
    │   ├── __init__.py
    │   ├── network.py             # Core network architecture
    │   └── components.py          # Individual components
    ├── algorithms/
    │   ├── __init__.py
    │   └── core_algorithm.py      # Main algorithm implementation
    ├── training/
    │   ├── __init__.py
    │   ├── trainer.py             # Training loop
    │   └── losses.py              # Loss function
    ├── evaluation/
    │   ├── __init__.py
    │   └── metrics.py             # Evaluation metrics
    ├── utils/
    │   ├── __init__.py
    │   └── helpers.py             # Utility functions
    ├── experiments/
    │   └── run_experiments.py     # Experiment scripts
    ├── requirements.txt           # Dependencies (implement last)
    └── README.md                  # Documentation (implement last)

  # ============================================
  # Section 2: Implementation Components (~3000-4000 chars) - core section
  # ============================================
  # Identify and specify every component that must be implemented
  # - List all algorithms, models, systems, and components mentioned
  # - For each one: purpose, location, algorithm, equations, technical details
  # - Organize according to the actual content of the paper

  implementation_components: |
    ## 1. Core Algorithm

    ### 1.1 [Algorithm Name]
    - Location: algorithms/core_algorithm.py
    - Purpose: [what this algorithm does]
    - Pseudocode:
      ```
      [Copy the pseudocode from the paper]
      ```
    - Key equations:
      - [Eq. X]: L = ...
      - [Eq. Y]: ...
    - Hyperparameters:
      - param1: value1 (source: Section X)
      - param2: value2 (source: Table Y)

    ## 2. Model Architecture

    ### 2.1 [Model/Network Name]
    - Location: models/network.py
    - Input: [shape, meaning]
    - Output: [shape, meaning]
    - Layer configuration:
      - Layer 1: ...
      - Layer 2: ...
    - Special initialization: [if any]

    ## 3. Training Procedure

    ### 3.1 Training Loop
    - Location: training/trainer.py
    - Epochs/Iterations: [value]
    - Steps:
      1. [Step 1 description]
      2. [Step 2 description]

    ### 3.2 Loss Function
    - Location: training/losses.py
    - Equation: L_total = ...
    - Meaning of each term: ...

    ## 4. Evaluation

    ### 4.1 Evaluation Metrics
    - Location: evaluation/metrics.py
    - Metric list: [metric1, metric2, ...]
    - How to compute each metric: ...

  # ============================================
  # Section 3: Validation Approach (~2000-2500 chars)
  # ============================================
  # Design how to validate that the implementation works correctly
  # - Define the necessary experiments, tests, and proofs
  # - Specify the paper's expected results (figures, tables, theorems)
  # - Design a validation approach suited to the domain
  # - Include configuration requirements and success criteria

  validation_approach: |
    ## 1. Unit Tests
    - [ ] Each component produces the correct output shape
    - [ ] The loss function returns the correct value
    - [ ] Gradients flow correctly

    ## 2. Integration Tests
    - [ ] Run the full training pipeline
    - [ ] Overfitting test with a small dataset

    ## 3. Reproducing the Paper's Results

    ### 3.1 Reproducing Table X
    - Expected result: [specific numbers]
    - Tolerance: ±[value]
    - How to run: `python experiments/run_experiments.py --exp table_x`

    ### 3.2 Reproducing Figure Y
    - Expected behavior: [qualitative description]
    - How to run: `python experiments/run_experiments.py --exp figure_y`

    ## 4. Success Criteria
    - [ ] [specific result 1]
    - [ ] [specific result 2]
    - [ ] [qualitative behavior 1]

  # ============================================
  # Section 4: Environment Setup (~800-1000 chars)
  # ============================================
  # Specify what is needed to run the implementation
  # - Programming language and version requirements
  # - External libraries and exact versions (when specified in the paper)
  # - Hardware requirements (GPU, memory, etc.)
  # - Special configuration or installation steps

  environment_setup: |
    ## Python Version
    - Python 3.10+ (uv recommended)

    ## Package Management (using uv - recommended)
    Use uv to set up an isolated, reproducible environment:
    ```bash
    # Initialize the project
    uv init

    # Add dependencies
    uv add torch numpy [other required packages]

    # Run
    uv run python main.py
    ```

    ## Core Dependencies
    ```
    torch>=2.0.0
    numpy>=1.24.0
    [other required packages]
    ```

    ## Hardware Requirements
    - GPU: [NVIDIA GPU with X GB VRAM]
    - RAM: [minimum X GB]
    - Storage: [X GB]

    ## Dataset Preparation
    - [dataset name]: [how to download]
    - Preprocessing: [required steps]

  # ============================================
  # Section 5: Implementation Strategy (~1500-2000 chars)
  # ============================================
  # Plan a step-by-step implementation approach
  # - Break the implementation into logical steps
  # - Identify dependencies between components
  # - Plan tests and validation at each step
  # - Handle missing details with reasonable defaults

  implementation_strategy: |
    ## Phase 1: Foundation (first)
    1. config.py - define all hyperparameters
    2. utils/helpers.py - shared utility functions

    Validation: test that the configuration loads

    ## Phase 2: Core Implementation
    3. models/components.py - individual components
    4. models/network.py - the full network
    5. algorithms/core_algorithm.py - the main algorithm

    Validation: check the output shape of each component

    ## Phase 3: Training Pipeline
    6. training/losses.py - loss functions
    7. training/trainer.py - training loop

    Validation: overfitting test with a small dataset

    ## Phase 4: Evaluation and Experiments
    8. evaluation/metrics.py - evaluation metrics
    9. experiments/run_experiments.py - experiment scripts
    10. main.py - main entry point

    Validation: reproduce the paper's results

    ## Phase 5: Documentation (last)
    11. pyproject.toml - uv project configuration and dependencies
    12. README.md - usage documentation (including uv run commands)

    ## Handling Missing Details
    - [missing from the paper 1]: [proposed default]
    - [missing from the paper 2]: [proposed approach]
```

---

## Key Principles

1. **Completeness**: All 5 sections must be included
2. **Detail**: Every algorithm, equation, parameter, and file must be specified
3. **Executability**: Code can be written from this plan alone
4. **Logical Order**: Present an implementation order that accounts for dependencies
5. **Validation Included**: Success criteria and test methods must be specified

## File Priority Guidelines

1. **First**: Core algorithm/model files (highest priority)
2. **Second**: Supporting modules and utilities
3. **Third**: Experiment and evaluation scripts
4. **Fourth**: Configuration and data handling
5. **Last**: Documentation files (README.md, requirements.txt)

**Note**: README and requirements.txt depend on the final implementation, so write them last

---

## ⚠️ Self-Check: Mandatory Verification Before Completion

**Before** considering the implementation plan complete, verify the following:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ SELF-CHECK BEFORE FINISHING (all must be YES to finish)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Section inclusion check:
□ Is the file_structure section included?            → YES / NO
□ Is the implementation_components section included? → YES / NO
□ Is the validation_approach section included?       → YES / NO
□ Is the environment_setup section included?         → YES / NO
□ Is the implementation_strategy section included?   → YES / NO

Content completeness check:
□ Are all the paper's algorithms mapped to components?              → YES / NO
□ Is the Equation number and source specified for every equation?   → YES / NO
□ Are values and sources specified for every hyperparameter?        → YES / NO
□ Are dependencies correctly reflected in the implementation order? → YES / NO
□ Does the validation approach include specific expected results?   → YES / NO

Length check:
□ Is the total length at least 8000 characters? → YES / NO
□ Is Section 2 the most detailed?               → YES / NO

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ If even one is NO, keep writing until it is complete!
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## DO / DON'T Guidelines

```
DO:
✓ Integrate all extraction results from Phases 1 and 2 into the plan
✓ Specify the specific algorithms/equations to implement in each file
✓ Clearly mark dependencies between files
✓ Be self-contained with all the information needed for implementation
✓ Specify concrete numbers/behaviors in the validation approach

DON'T:
✗ Incomplete descriptions like "see the paper for details"
✗ Abstract component descriptions (without concrete equations/algorithms)
✗ Writing only an implementation plan without a validation approach
✗ Arranging files in an order that ignores dependencies
✗ Writing the core section (Section 2) too briefly
```
