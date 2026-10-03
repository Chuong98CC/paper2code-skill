# Paper2Code Skill for Claude Code

> Transform research papers into executable code with a structured, multi-phase pipeline.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code](https://img.shields.io/badge/Claude-Code-blueviolet)](https://claude.ai/code)
[![Agent Skills](https://img.shields.io/badge/Agent-Skills-green)](https://agentskills.io)

## Why This Exists

There are great paper-to-code tools like [DeepCode](https://github.com/HKUDS/DeepCode), but they require separate API costs for each run. If you're already using **Claude Code** with a subscription, why pay extra?

This skill brings the same structured, multi-phase approach directly into Claude Code — **no additional API costs**, just your existing subscription.

## Overview

**Paper2Code** is a Claude Code Skill that systematically converts research papers (PDF/arXiv) into fully functional, reproducible code. Unlike naive approaches that simply feed papers to an LLM, this skill uses a **structured intermediate representation (YAML)** to ensure accuracy and completeness.

### Key Features

- **4+2 Phase Pipeline**: Algorithm Extraction → Concept Analysis → Code Planning → Implementation (+ Reference Search & Memory Management)
- **Structured YAML Intermediate Representation**: Not just code generation, but systematic knowledge extraction
- **Self-Check Mechanisms**: Built-in verification at each phase to ensure completeness
- **Behavioral Controls**: DO/DON'T guidelines to prevent common implementation mistakes
- **Reference-Augmented Generation**: Optional reference code search for implementation quality

## Quick Start

### Installation

#### For Humans

**Option 1: Personal Installation (Recommended)**
```bash
# Clone the repository
git clone https://github.com/issol14/paper2code-skill.git

# Copy to your Claude skills directory
cp -r paper2code-skill/skills/paper2code ~/.claude/skills/
```

**Option 2: Project Installation**
```bash
# Add to your project's .claude/skills directory
mkdir -p .claude/skills
cp -r paper2code-skill/skills/paper2code .claude/skills/
```

**Option 3: Let Claude do it for you**

Just paste this into Claude Code:
```
Install the paper2code skill from https://github.com/issol14/paper2code-skill
```

---

<details>
<summary><b>📋 For LLM Agents (click to expand)</b></summary>

If you're an LLM Agent helping a user install paper2code-skill, follow these steps:

### Step 1: Check Prerequisites

```bash
# Check if pdftotext is available (optional but recommended)
command -v pdftotext &> /dev/null && echo "pdftotext: OK" || echo "pdftotext: Not installed (optional)"
```

If pdftotext is not installed, inform the user:
```
pdftotext is recommended for PDF processing. Install with:
- Ubuntu/Debian: sudo apt install poppler-utils
- macOS: brew install poppler
- Windows: Install poppler and add to PATH
```

### Step 2: Create Skills Directory

```bash
# Create the Claude skills directory if it doesn't exist
mkdir -p ~/.claude/skills
```

### Step 3: Clone and Install

```bash
# Clone the repository
git clone https://github.com/issol14/paper2code-skill.git /tmp/paper2code-skill

# Copy skill files to Claude skills directory
cp -r /tmp/paper2code-skill/skills/paper2code ~/.claude/skills/

# Clean up
rm -rf /tmp/paper2code-skill
```

### Step 4: Verify Installation

```bash
# Verify the skill files exist
ls ~/.claude/skills/paper2code/
```

Expected output should show:
```
01_algorithm_extraction.md
02_concept_analysis.md
03_code_planning.md
04_implementation_guide.md
05_reference_search.md
06_memory_management.md
README.md
SKILL.md
```

### Step 5: Confirm to User

Tell the user:
```
paper2code-skill has been installed successfully!

You can now use it by providing a paper URL or PDF path:
- "https://arxiv.org/abs/2301.12345 implement this paper"
- "/path/to/paper.pdf implement this paper"

The skill will automatically activate when you request paper implementation.
```

</details>

### Usage

Once installed, Claude Code will automatically activate the skill when you request paper implementation:

```
# From arXiv URL
"https://arxiv.org/abs/2301.12345 implement this paper"

# From PDF file
"/path/to/paper.pdf implement the algorithm from this paper"

# Specific section
"Implement only Algorithm 2 from Section 3 of this paper"
```

### Detailed Usage Examples

#### Example 1: Full Paper Implementation
```
User: https://arxiv.org/abs/2312.00752 implement this paper

Claude: I'll analyze the paper and convert it to code.

[Phase 1: Extracting algorithms...]
→ Saved 01_algorithm_extraction.yaml

[Phase 2: Analyzing concepts...]
→ Saved 02_concept_analysis.yaml

[Phase 3: Creating implementation plan...]
→ Saved 03_implementation_plan.yaml

[Phase 4: Implementing code...]
→ Created config.py
→ Created models/network.py
→ ...
→ Created main.py
→ Created README.md

Implementation complete. Run with `python main.py`.
```

#### Example 2: With Reference Search
```
User: Implement this paper. First, search for similar implementations.

Claude: I'll search for reference code before implementing.

[Phase 0: Searching reference code...]
→ Found 5 related implementations
→ Saved reference_search.yaml

[Proceeding with Phase 1-4...]
```

#### Example 3: Specific Algorithm Only
```
User: Implement only the Self-Attention part from Algorithm 2

Claude: I'll focus on implementing Self-Attention from Algorithm 2.
[Extracting and implementing the specific algorithm...]
```

### Output Structure

After implementation, you'll get:
```
paper_workspace/
├── 01_algorithm_extraction.yaml   # Extracted algorithms & equations
├── 02_concept_analysis.yaml       # Paper structure analysis
├── 03_implementation_plan.yaml    # Detailed implementation plan
└── src/
    ├── config.py                  # Hyperparameters & settings
    ├── models/
    │   ├── __init__.py
    │   └── network.py             # Neural network architecture
    ├── algorithms/
    │   └── core.py                # Main algorithm implementation
    ├── training/
    │   ├── losses.py              # Loss functions
    │   └── trainer.py             # Training loop
    ├── evaluation/
    │   └── metrics.py             # Evaluation metrics
    ├── main.py                    # Entry point
    ├── requirements.txt           # Dependencies
    └── README.md                  # Usage documentation
```

## Pipeline Overview

```
[Paper Input: PDF/arXiv URL]
        │
        ▼
┌─────────────────────────────────────┐
│ Phase 0: Reference Search (Optional)│
│ → Find similar implementations      │
└─────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────┐
│ Phase 1: Algorithm Extraction       │
│ → Extract all algorithms, equations │
│ → Output: YAML specification        │
└─────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────┐
│ Phase 2: Concept Analysis           │
│ → Map paper structure               │
│ → Identify components & experiments │
└─────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────┐
│ Phase 3: Implementation Plan        │
│ → 5-section detailed plan           │
│ → File structure & dependencies     │
└─────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────┐
│ Phase 4: Code Implementation        │
│ → File-by-file implementation       │
│ → Complete, runnable codebase       │
└─────────────────────────────────────┘
```

## Skill Structure

```
paper2code/
├── SKILL.md                      # Main skill entry point
├── 01_algorithm_extraction.md    # Phase 1: Algorithm extraction protocol
├── 02_concept_analysis.md        # Phase 2: Paper structure analysis
├── 03_code_planning.md           # Phase 3: Implementation planning
├── 04_implementation_guide.md    # Phase 4: Code generation guide
├── 05_reference_search.md        # Phase 0: Reference code search (optional)
└── 06_memory_management.md       # Context/memory management guide
```

## What Makes This Different?

| Aspect | Naive Approach | Paper2Code Skill |
|--------|---------------|------------------|
| Process | Direct paper → code | Structured multi-phase pipeline |
| Intermediate | None | YAML knowledge representation |
| Verification | Manual | Built-in self-check at each phase |
| Completeness | Often partial | Systematic with checklists |
| Reproducibility | Inconsistent | Explicit success criteria |

## Core Principles

### Behavioral Controls
```
DO:
✓ Implement exactly what the paper specifies
✓ Write simple, direct code
✓ Test each component immediately
✓ Move to next file without asking permission

DON'T:
✗ Ask "Should I implement the next file?"
✗ Over-engineer or add unnecessary abstractions
✗ Skip unclear parts (document in missing_but_critical)
✗ Guess parameter values not in the paper
```

### Quality Standards
- **Completeness**: No placeholders or TODOs
- **Accuracy**: Exact equations, parameters from paper
- **Executability**: Code runs without errors
- **Reproducibility**: Can reproduce paper results

## Requirements

- **Claude Code** with Claude subscription
- **pdftotext** (for PDF processing): `sudo apt install poppler-utils`

## FAQ

<details>
<summary><b>Q: What types of papers work best?</b></summary>

Primarily optimized for **ML/DL research papers**, but works with any paper that has clearly described algorithms:
- Deep learning models (Transformer, CNN, GNN, etc.)
- Reinforcement learning algorithms
- Optimization algorithms
- Data processing pipelines

</details>

<details>
<summary><b>Q: What if the implementation differs from the paper?</b></summary>

1. Check the generated YAML files to verify algorithm extraction accuracy
2. Look for missing information in the `missing_but_critical` section
3. Provide the paper's Appendix or Supplementary Material
4. Request re-implementation of specific parts: "Re-implement the loss calculation in Algorithm 2"

</details>

<details>
<summary><b>Q: Can it handle long papers?</b></summary>

Yes, following the guidelines in `06_memory_management.md`:
- Section-by-section analysis
- Context management through intermediate YAML saves
- Recoverable checkpoints when needed

</details>

<details>
<summary><b>Q: When should I use reference code search?</b></summary>

Useful when:
- The paper lacks implementation details
- You need specific framework patterns
- You want to reference implementation tricks for complex algorithms

Request it by saying "Also search for similar implementations" or "Find reference code first".

</details>

<details>
<summary><b>Q: How is code quality ensured?</b></summary>

Each Phase has built-in **Self-Check mechanisms**:
- Phase 1: Verify all algorithms/equations extracted
- Phase 2: Confirm component relationships and experiment requirements
- Phase 3: Check 5 required sections and content balance
- Phase 4: Final completion checklist (executability, reproducibility, etc.)

</details>

## Acknowledgments

This skill was inspired by [DeepCode](https://github.com/HKUDS/DeepCode) from HKU Data Intelligence Lab, which pioneered the structured approach to paper-to-code conversion with multi-agent orchestration.

## License

MIT License - See [LICENSE](LICENSE) for details.

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

---

**Note**: This skill is designed for use with Claude Code. For information about the Agent Skills standard, see [agentskills.io](https://agentskills.io).
