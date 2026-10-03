# Phase 4: Code Implementation Guide

## Goal
Generate a **complete and executable codebase** based on the implementation plan produced in Phase 3.

---

## Core Behavioral Control Rules

### ⚠️ CRITICAL BEHAVIORAL RULES

```
⚠️ SINGLE FILE PER RESPONSE:
- Implement exactly one file per response
- Do not ask for permission between files
- Keep implementing until done

DO:
- Implement exactly what the paper specifies
- Write simple, direct code
- Working first, elegant later
- Test each component immediately
- Move to the next file right after finishing an implementation

DON'T:
- Don't ask "Should I implement the next file?" between files
- Waste time on advanced tooling instead of paper requirements
- Extensive documentation not needed for core functionality
- Optimization utilities not needed for reproducibility
- Excessive abstraction or design patterns
- Only giving instructions without writing actual code
```

### Tool Calling Strategy

```
TOOL CALLING STRATEGY:
1. ⚠️ Implement one file per message
2. Plan the next step after checking results
3. File implementation cycle: analyze → implement → next file

EXECUTION PATTERN:
- Plan First: Explain reasoning before each task
- One Step at a Time: Execute → check results → plan next → execute
- Iterative Progress: Build the solution incrementally
- Strategic Sequencing: Choose the logical next step based on previous results

⚠️ CRITICAL: Use bash and python tools to directly reproduce the paper
            - Don't just give instructions, actually implement it
```

---

## Top Priority

Implement **all** algorithms, experiments, and methods mentioned in the paper.
Success is measured by **completeness and accuracy**, not by code elegance.

### Core Strategy
- Read the paper and the implementation plan thoroughly and identify every algorithm, method, and experiment
- Core algorithms first, then the environment, then integrated implementation
- Use the exact versions and specifications stated in the paper
- Test each component immediately after implementing it
- Focus on a working implementation rather than a perfect architecture

---

## Implementation Approach

### Incremental Build, File by File
At each step:
1. **Identify**: Check the implementation plan for what to implement next
2. **Implement**: Implement one component at a time
3. **Test**: Test immediately to catch problems early
4. **Integrate**: Integrate with existing components
5. **Validate**: Validate against the paper's specifications

---

## Implementation Order

### Step 1: Setup and Environment Files
```
pyproject.toml     # uv project configuration (created by uv init)
config.py          # All hyperparameters and settings
```

### Step 2: Core Utilities and Base Classes
```
utils/__init__.py
utils/helpers.py   # Common utility functions
```

### Step 3: Main Implementation Modules
```
models/__init__.py
models/network.py      # Core network architecture
models/components.py   # Individual components

algorithms/__init__.py
algorithms/core.py     # Main algorithm implementation
```

### Step 4: Training Pipeline
```
training/__init__.py
training/losses.py    # Loss functions
training/trainer.py   # Training loop
```

### Step 5: Evaluation and Experiments
```
evaluation/__init__.py
evaluation/metrics.py        # Evaluation metrics
experiments/run_main.py      # Main experiment script
```

### Step 6: Entry Point and Documentation
```
main.py            # Main entry point
README.md          # Usage documentation (including uv run commands)
```

### Environment Setup Commands (using uv)
```bash
# At project start
uv init
uv add torch numpy [required packages]

# Run
uv run python main.py
```

---

## Code Quality Standards

### Completeness
- **No** placeholders, TODOs, or incomplete functions
- Full feature implementation with proper error handling
- Complete APIs with correct signatures and documentation
- Every specified feature working out of the box

### Quality
- Production-level code following language best practices
- Comprehensive type hints and docstrings
- Proper logging, validation, and resource management
- Clean architecture with separation of concerns

### Domain-Specific Adaptation

**Research/ML papers:**
- Mathematical accuracy
- Reproducibility (seeds, deterministic operations)
- Evaluation metrics
- Experiment logging

**Systems/Tools:**
- CLI interface
- Configuration management
- Error handling
- Documentation

---

## ✅ Completion Checklist (MANDATORY)

Before considering the work complete, be sure to verify:

```
✅ COMPLETENESS CHECKLIST:
- [ ] Every algorithm mentioned in the paper (including abbreviations and alternative names)
- [ ] Every environment/dataset at the exact version specified
- [ ] Every comparison method referenced in the experiments
- [ ] A working integration that can run the paper's experiments
- [ ] A complete codebase that reproduces all of the paper's metrics, figures, and tables
- [ ] Basic documentation explaining how to reproduce the results

⚠️ If not every item is checked, it is not complete!
```

---

## Critical Success Factors

```
CRITICAL SUCCESS FACTORS:

1. Accuracy:
   - Match the paper's specifications exactly (versions, parameters, settings)
   - Convert equations into code exactly
   - Use hyperparameter values exactly

2. Completeness:
   - Implement all discussed methods, not just the main contribution
   - Also implement the variants needed for ablation studies
   - Also implement what is needed for baseline comparisons

3. Functionality:
   - The code actually works and runs the experiments successfully
   - Training/evaluation runs without errors
   - The paper's results can actually be reproduced
```

---

## Execution Guidelines

### Before Implementing Each File
1. Check the requirements for that file in the implementation plan
2. Check whether the files it depends on have already been implemented
3. Refer to the relevant equations/algorithms in the paper

### While Implementing Each File
1. Write complete import statements
2. Define the class/function structure
3. Convert the paper's equations/algorithms into code
4. Add appropriate docstrings
5. Add error handling

### After Implementing Each File
1. Check for syntax errors
2. Check that all imports resolve
3. Run a simple test if possible
4. **Move to the next file right away** (do not ask for permission)

---

## File Writing Template

### Basic Python File Structure
```python
"""
[File description]

Paper: [Paper title]
Section: [Relevant section number]
"""

import ...

# Paper hyperparameters
PARAM_NAME = value  # Source: Section X / Table Y


class ComponentName:
    """
    [Component description]

    Implementation of Equation X from the paper:
    [Equation]
    """

    def __init__(self, ...):
        ...

    def forward(self, ...):
        # Implementation of Eq. X
        ...


def main():
    """Main entry function"""
    ...


if __name__ == "__main__":
    main()
```

---

## Final Checks

After the implementation is complete:

1. **Execution test**: Does `python main.py` run without errors?
2. **Training test**: Does training proceed on a small dataset?
3. **Result check**: Can the paper's main results be reproduced?
4. **Documentation check**: Is the execution method clear in README.md?

If all items pass, the implementation is complete!

---

## ⚠️ REMEMBER

```
The goal is to reproduce the entire paper.
Not a single part or a minimal example.

The file reading tool is PAGINATED,
so you must call it multiple times to read all relevant parts of the paper.

If you find patterns in reference code, use them only as inspiration,
and always implement according to the paper's original specifications.
```
