# Memory and Context Management Guide

## Purpose
When processing long papers, this **prevents context overflow** and ensures **efficient task progress**.

---

## Core Strategies

### 1. Save Output Step by Step

Save results to files when each Phase completes to reduce the context burden:

```
paper_workspace/
├── paper.txt                      # Original paper text
├── 01_algorithm_extraction.yaml   # Phase 1 result
├── 02_concept_analysis.yaml       # Phase 2 result
├── 03_implementation_plan.yaml    # Phase 3 result
└── src/                           # Phase 4 generated code
    ├── config.py
    ├── models/
    ├── algorithms/
    └── ...
```

**Example save commands:**
```bash
# Save the Phase 1 result
cat > paper_workspace/01_algorithm_extraction.yaml << 'EOF'
[Phase 1 YAML output]
EOF

# Save the Phase 2 result
cat > paper_workspace/02_concept_analysis.yaml << 'EOF'
[Phase 2 YAML output]
EOF
```

### 2. Passing Context Between Phases

When moving to the next Phase, **pass only the key summary instead of the full output**:

```yaml
# Summary passed from Phase 1 → Phase 2
phase1_summary:
  algorithms_found: 3
  key_algorithms:
    - "Algorithm 1: [name] - [one-line key content]"
    - "Algorithm 2: [name] - [one-line key content]"
  hyperparameters_count: 15
  critical_equations: [3, 5, 7, 12]

# Summary passed from Phase 2 → Phase 3
phase2_summary:
  components_count: 5
  implementation_complexity: "Medium"
  key_dependencies:
    - "Component A → Component B"
    - "Component B → Component C"
  experiments_count: 4
```

### 3. Memory Optimization During Implementation

Managing context during the per-file implementation cycle:

```
File implementation cycle:
┌─────────────────────────────────────────────────────┐
│ 1. Load only the info needed for the current file   │
│    - the file's section in implementation_plan.yaml │
│    - dependency file interfaces (not the full code) │
├─────────────────────────────────────────────────────┤
│ 2. Implement the file                               │
├─────────────────────────────────────────────────────┤
│ 3. Move to the next file when done implementing     │
│    - reference the previous file only when needed   │
│    - do not keep the full code in memory            │
└─────────────────────────────────────────────────────┘
```

---

## Tips for Processing Long Papers

### Reading the Paper in Parts

If the paper is very long, analyze it section by section:

```
Reading order (priority):
1. Abstract + Introduction (identify the key contributions)
2. Entire Method section (extract algorithms)
3. Experiments section (environment, baselines, metrics)
4. Appendix (detailed hyperparameters)
5. Related Work (only when needed)

Can skip:
- Related Work details (not needed for implementation)
- Long Discussion/Conclusion (summary only)
- Acknowledgments
```

### Splitting Large Algorithms

Split complex algorithms into sub-components:

```yaml
# Split it instead of processing everything at once
large_algorithm:
  component_1:
    extracted: true
    summary: "[summary]"
  component_2:
    extracted: true
    summary: "[summary]"
  component_3:
    extracted: false  # not yet processed
```

---

## Self-Monitoring Checkpoints

During implementation, **intermediate saves** are recommended in the following situations:

```
Intermediate save triggers:
□ Every 5 files implemented
□ When a complex algorithm (50+ lines) is implemented
□ Save the current state when an error occurs
□ Before starting a new Phase
□ Before starting a long task (30+ minutes expected)
```

### Save Checklist

```yaml
checkpoint_save:
  current_phase: "[current Phase number]"
  completed_files:
    - "config.py"
    - "models/network.py"
  current_file: "algorithms/core.py"
  current_progress: "50%"  # progress on the current file
  next_steps:
    - "[next task 1]"
    - "[next task 2]"
  blockers:
    - "[blockers, if any]"
```

---

## Context Recovery Protocol

If the conversation was interrupted or context was lost:

```
Recovery steps:
1. Check the paper_workspace/ directory
2. Read the most recently completed Phase result file
3. Check the list of generated code files
4. Determine the last point of work
5. Resume from that point
```

**Example recovery commands:**
```bash
# Check the current state
ls -la paper_workspace/
ls -la paper_workspace/src/

# Check the last Phase result
cat paper_workspace/03_implementation_plan.yaml

# Check generated files
find paper_workspace/src -name "*.py" -type f
```

---

## Efficient Reference Patterns

### Reference Only the Interface

When referencing another file, **only the interface is needed, not the full implementation**:

```python
# Reference only signatures instead of the full code
# Interface of models/network.py:
class NetworkModel:
    def __init__(self, config: Config): ...
    def forward(self, x: Tensor) -> Tensor: ...
    def get_features(self, x: Tensor) -> Tensor: ...
```

### Using the Dependency Graph

Reference the dependency graph when deciding the implementation order:

```
config.py (no dependencies)
    ↓
utils/helpers.py (depends only on config)
    ↓
models/components.py (depends on config, utils)
    ↓
models/network.py (depends on components)
    ↓
algorithms/core.py (depends on network)
    ↓
training/trainer.py (depends on all)
```

---

## ⚠️ Precautions

```
⚠️ MEMORY MANAGEMENT RULES:

1. Do not process the entire paper at once
   → Process it section by section

2. Do not include the full output of the previous Phase in the next Phase
   → Pass only the key summary

3. Do not keep all generated code in memory
   → Save it to files and reference it when needed

4. During long tasks, periodically save progress
   → So recovery is possible if interrupted

5. Avoid unnecessary repeated reads
   → Summarize and store information once it has been read
```

---

## Recommended Workflow

```
[Paper input]
    │
    ▼
[Phase 1: Algorithm extraction]
    │ → Save 01_algorithm_extraction.yaml
    │ → Generate key summary
    ▼
[Phase 2: Concept analysis]
    │ → Save 02_concept_analysis.yaml
    │ → Keep Phase 1 summary + Phase 2 summary
    ▼
[Phase 3: Implementation planning]
    │ → Save 03_implementation_plan.yaml
    │ → Keep only key info needed for implementation
    ▼
[Phase 4: Code implementation]
    │ → Implement and save file by file
    │ → Checkpoint every 5 files
    ▼
[Done]
```
