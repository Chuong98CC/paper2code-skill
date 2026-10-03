---
name: paper2code
description: |
  Analyzes research papers (PDF/arXiv URL) and converts them into executable code.
  Automatically activates on requests to replicate a paper, implement an algorithm, or reproduce research.
  Responds to requests such as "implement this paper", "paper2code", "convert paper to code".
---

# Paper2Code: An AI Agent That Converts Research Papers into Code

## Overview

This Skill systematically analyzes research papers and runs a **4+2-stage pipeline** that converts them into executable code.

**Core principle**: Rather than simply reading the paper and generating code, it first creates a **structured intermediate representation (YAML)** and then writes the code.

---

## ⚠️ Core Behavioral Control Rules (CRITICAL)

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ MANDATORY BEHAVIORAL RULES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. Implement only one file at a time
2. After implementing a file, proceed to the next file without asking for confirmation/permission
3. The original paper specification always takes precedence over reference code
4. The Self-Check for each Phase must be performed before completion
5. Save all intermediate results as YAML files

DO:
✓ Implement exactly what the paper specifies
✓ Write simple and direct code
✓ Working first, elegant later
✓ Test each component immediately
✓ Move to the next file immediately after implementation is complete

DON'T:
✗ Do not ask "Shall I implement the next file?" between files
✗ Extensive documentation not required for core functionality
✗ Optimization not required for reproducibility
✗ Excessive abstraction or design patterns
✗ Providing only instructions without writing actual code
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Input Handling

### Supported Formats
1. **arXiv URL**: `https://arxiv.org/abs/xxxx.xxxxx` or `https://arxiv.org/pdf/xxxx.xxxxx.pdf`
2. **PDF file path**: `/path/to/paper.pdf`
3. **Already converted text/markdown**: When the paper content is provided as text

### How to Handle Input

**For an arXiv URL:**
```bash
# Convert to a PDF URL and download
curl -L "https://arxiv.org/pdf/xxxx.xxxxx.pdf" -o paper.pdf

# Convert the PDF to text (using pdftotext)
pdftotext -layout paper.pdf paper.txt
```

**For a PDF file:**
```bash
pdftotext -layout "/path/to/paper.pdf" paper.txt
```

---

## Pipeline Overview

```
[User input: paper URL/file]
        │
        ▼
┌─────────────────────────────────────────────┐
│ Step 0: Obtain paper text                   │
│ - arXiv URL → PDF download                  │
│ - PDF → text conversion                     │
└─────────────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────────────┐
│ Phase 0: Reference Code Search (Optional)   │
│ @[05_reference_search.md]                   │
│ Output: reference_search.yaml               │
└─────────────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────────────┐
│ Phase 1: Algorithm Extraction               │
│ @[01_algorithm_extraction.md]               │
│ Output: 01_algorithm_extraction.yaml        │
└─────────────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────────────┐
│ Phase 2: Concept Analysis                   │
│ @[02_concept_analysis.md]                   │
│ Output: 02_concept_analysis.yaml            │
└─────────────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────────────┐
│ Phase 3: Implementation Plan                │
│ @[03_code_planning.md]                      │
│ Output: 03_implementation_plan.yaml         │
└─────────────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────────────┐
│ Phase 4: Code Implementation                │
│ @[04_implementation_guide.md]               │
│ Output: complete project directory          │
└─────────────────────────────────────────────┘
```

---

## Data Transfer Format Between Phases

### Phase 1 → Phase 2 Transfer
```yaml
phase1_to_phase2:
  algorithms_found: "[number of algorithms found]"
  key_algorithms:
    - name: "[algorithm name]"
      section: "[paper section]"
      complexity: "[Simple/Medium/Complex]"
  hyperparameters_count: "[number of hyperparameters collected]"
  critical_equations: "[list of key equation numbers]"
  missing_info: "[list of missing information]"
```

### Phase 2 → Phase 3 Transfer
```yaml
phase2_to_phase3:
  components_count: "[number of components identified]"
  implementation_complexity: "[Low/Medium/High]"
  key_dependencies:
    - "[component A] → [component B]"
  experiments_to_reproduce:
    - "[experiment name]: [expected result]"
  success_criteria:
    - "[specific success criteria]"
```

### Phase 3 → Phase 4 Transfer
```yaml
phase3_to_phase4:
  file_order: "[list of files in implementation order]"
  current_file: "[file currently being implemented]"
  completed_files: "[list of completed files]"
  blocking_dependencies: "[dependencies that must be resolved]"
```

---

## Phase Details

### Phase 0: Reference Code Search (Optional)
Using the @[05_reference_search.md](05_reference_search.md) prompt:
- Search for and evaluate 5 similar implementations
- Obtain references to improve implementation quality
- **Output**: Reference list in YAML format

### Phase 1: Algorithm Extraction
Using the @[01_algorithm_extraction.md](01_algorithm_extraction.md) prompt:
- Extract all algorithms, equations, and pseudocode
- Collect hyperparameters and configuration values
- Document the training procedure and optimization methods
- **Output**: Complete algorithm specification in YAML format

### Phase 2: Concept Analysis
Using the @[02_concept_analysis.md](02_concept_analysis.md) prompt:
- Map the paper structure and sections
- Analyze the system architecture
- Identify relationships and data flow between components
- Document experiment and validation requirements
- **Output**: Implementation requirements specification in YAML format

### Phase 3: Creating the Implementation Plan
Using the @[03_code_planning.md](03_code_planning.md) prompt:
- Integrate the results of Phases 1 and 2
- Create a detailed implementation plan with 5 required sections:
  1. `file_structure`: Project file structure
  2. `implementation_components`: Details of components to implement
  3. `validation_approach`: Validation and testing methods
  4. `environment_setup`: Environment and dependencies
  5. `implementation_strategy`: Step-by-step implementation strategy
- **Output**: Complete YAML implementation plan (8000-10000 characters)

### Phase 4: Code Implementation
Following the @[04_implementation_guide.md](04_implementation_guide.md) guide:
- Generate code file by file according to the plan
- Implement in dependency order
- Each file must be complete and executable
- **Output**: Executable codebase

---

## Memory Management
Refer to the @[06_memory_management.md](06_memory_management.md) guide:
- Manage context when processing long papers
- Save output at each step
- Recovery protocol for interruptions

---

## Quality Standards

### Principles That Must Be Followed
- **Completeness**: Complete implementation with no placeholders or TODOs
- **Accuracy**: Exactly reflect the equations and parameters specified in the paper
- **Executability**: Code that can be run immediately
- **Reproducibility**: Must be able to reproduce the paper's results

### File Implementation Order
1. Configuration and environment files (initialize config, requirements.txt)
2. Core utilities and base classes
3. Main algorithm/model implementation
4. Training and evaluation scripts
5. Documentation (finalize README.md and requirements.txt)

---

## ✅ Final Completion Checklist (MANDATORY)

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ BEFORE DECLARING COMPLETE - ALL MUST BE YES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

□ Are all algorithms from the paper implemented?                         → YES / NO
□ Are all environments/datasets set to the correct versions?             → YES / NO
□ Are all comparison methods referenced in the experiments implemented?  → YES / NO
□ Is there a working integration to run the paper's experiments?         → YES / NO
□ Can all metrics, figures, and tables be reproduced?                    → YES / NO
□ Is there basic documentation explaining how to reproduce the results?  → YES / NO
□ Does the code run without errors?                                      → YES / NO

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ If even one is NO, it is not complete!
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Usage Examples

### Example 1: arXiv Paper
```
User: implement this paper: https://arxiv.org/abs/2301.12345

Claude: I will analyze the paper and convert it into code.

[Phase 0: Reference code search (optional)...]
[Phase 1: Algorithm extraction...]
[Phase 2: Concept analysis...]
[Phase 3: Creating the implementation plan...]
[Phase 4: Code generation...]
```

### Example 2: PDF File
```
User: implement the algorithms from this paper: /home/user/papers/attention.pdf
```

### Example 3: Requesting Only a Specific Part
```
User: implement only the algorithm in Section 3 of this paper
```

---

## Related Files

- [01_algorithm_extraction.md](01_algorithm_extraction.md) - Phase 1: Algorithm Extraction
- [02_concept_analysis.md](02_concept_analysis.md) - Phase 2: Concept Analysis
- [03_code_planning.md](03_code_planning.md) - Phase 3: Implementation Plan
- [04_implementation_guide.md](04_implementation_guide.md) - Phase 4: Implementation Guide
- [05_reference_search.md](05_reference_search.md) - Phase 0: Reference Search (Optional)
- [06_memory_management.md](06_memory_management.md) - Memory Management Guide

---

## Notes

```
⚠️ REMEMBER:

1. Read the paper thoroughly: understand the full content before starting implementation
2. Save intermediate results: save each Phase's YAML output to a file
3. Incremental implementation: don't generate all the code at once; proceed file by file
4. Include validation: include simple test code when possible
5. References are inspiration: reference code is for understanding and applying, not copying
```
