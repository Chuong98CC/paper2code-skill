# Phase 1: Algorithm Extraction

## Goal
Extract **all technical details** needed for implementation from the research paper.
A developer must be able to implement the entire paper from this extraction result alone.

---

## ⚠️ DO / DON'T Guidelines (CRITICAL)

```
DO:
✓ Copy pseudocode exactly from the paper (do not change a single character)
✓ Record equations exactly along with their equation numbers (Eq. X)
✓ Search for hyperparameters everywhere: text, tables, captions, appendices
✓ Identify and record items that are missing but essential for implementation
✓ Cite the source (Section X, Table Y, Page Z) for all information
✓ Keep variable names, symbols, and subscripts exactly as in the paper

DON'T:
✗ Do not modify equations or pseudocode to "make them easier to understand"
✗ Do not guess parameter values that are not in the paper
✗ Do not record information without a source
✗ Do not substitute "commonly used" values
✗ Do not skip unclear parts (record them in missing_but_critical)
```

---

## ⚠️ Output Format Restrictions

```
⚠️ MANDATORY OUTPUT FORMAT:
- Output in YAML format only
- Pure YAML only, with no markdown explanation or preamble
- All required fields must be filled in
- For fields with no information, record "Not specified in paper"
- Add an "[INFERRED]" tag to guessed values

Output start: "```yaml"
Output end: "```"
```

---

## Extraction Protocol

### 1. Algorithm Scan
Find and extract all of the following from the paper:
- All content in the Method/Algorithm section
- Algorithm boxes (Algorithm 1, 2, 3...)
- Equations and formulas (all Equations)
- Pseudocode
- Implementation details

### 2. In-Depth Algorithm Extraction
For **every** algorithm/method/procedure found:

```yaml
algorithm_name: "[exact name in the paper]"
section: "[e.g., Section 3.2]"
algorithm_box: "[e.g., Algorithm 1 on page 4]"

pseudocode: |
  [Copy the paper's pseudocode exactly]
  Input: ...
  Output: ...
  1. Initialize ...
  2. For each ...
     2.1 Calculate ...
  [Keep the exact format and numbering]

mathematical_formulation:
  - equation: "[copy the equation exactly, e.g., L = L_task + λ*L_explain]"
    equation_number: "[e.g., Eq. 3]"
    where:
      L_task: "task loss"
      L_explain: "explanation loss"
      λ: "weighting parameter (default: 0.5)"

step_by_step_breakdown:
  1. "[Detailed description of what Step 1 does]"
  2. "[What Step 2 computes and why]"

implementation_details:
  - "Uses softmax temperature τ = 0.1"
  - "Gradient clipping at norm 1.0"
  - "Initialize weights with Xavier uniform"
```

### 3. Component Extraction
For **every** component/module mentioned:

```yaml
component_name: "[e.g., Mask Network, Critic Network]"
purpose: "[the role of this component in the system]"
architecture:
  input: "[shape and meaning]"
  layers:
    - "[Conv2d(3, 64, kernel=3, stride=1)]"
    - "[ReLU activation]"
    - "[BatchNorm2d(64)]"
  output: "[shape and meaning]"

special_features:
  - "[distinctive characteristics]"
  - "[special initialization method]"
```

### 4. Training Procedure Extraction
Extract the **complete** training process:

```yaml
training_loop:
  outer_iterations: "[count or condition]"
  inner_iterations: "[count or condition]"

  steps:
    1. "Sample batch of size B from buffer"
    2. "Compute importance weights using..."
    3. "Update policy with loss..."

  loss_functions:
    - name: "policy_loss"
      formula: "[exact equation]"
      components: "[meaning of each term]"

  optimization:
    optimizer: "Adam"
    learning_rate: "3e-4"
    lr_schedule: "linear decay to 0"
    gradient_norm: "clip at 0.5"
```

### 5. Hyperparameter Collection
Search **everywhere**: text, tables, captions:

```yaml
hyperparameters:
  # Training
  batch_size: 64
  buffer_size: 1e6
  discount_gamma: 0.99

  # Architecture
  hidden_units: [256, 256]
  activation: "ReLU"

  # Algorithm-specific
  explanation_weight: 0.5
  exploration_bonus_scale: 0.1
  reset_probability: 0.3

  # Source
  location_references:
    - "batch_size: Table 1"
    - "hidden_units: Section 4.1"
```

---

## Output Format

```yaml
complete_algorithm_extraction:
  paper_structure:
    method_sections: "[3, 3.1, 3.2, 3.3, 4]"
    algorithm_count: "[total number of algorithms found]"

  main_algorithm:
    # Write details in the format above

  supporting_algorithms:
    - # Detailed information for each supporting algorithm

  components:
    - # All components and architectures

  training_details:
    # Complete training procedure

  all_hyperparameters:
    # All parameters and values, with sources

  implementation_notes:
    - "[Implementation hints mentioned in the paper]"
    - "[Tricks mentioned in the text]"

  missing_but_critical:
    - "[Things not specified but essential]"
    - "[Together with suggested default values]"
```

---

## Important Principles

1. **Be thorough**: A developer must be able to implement the entire paper **from this extraction result alone**
2. **Be accurate**: Copy equations, variable names, and values **exactly**
3. **Leave nothing out**: Every algorithm, every equation, every parameter
4. **Cite sources**: Record where in the paper each piece of information came from
5. **Identify gaps**: Identify what is missing from the paper but needed for implementation

---

## ⚠️ Self-Check: Mandatory Verification Before Completion

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ SELF-CHECK BEFORE FINISHING (all must be YES to complete)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Algorithm extraction check:
□ Are all Algorithm boxes (Algorithm 1, 2, ...) extracted?  → YES / NO
□ Are all procedures in the Method section included?        → YES / NO
□ Does every equation have an Equation number?              → YES / NO

Hyperparameter check:
□ Are all parameters mentioned in the body text collected?        → YES / NO
□ Are all parameters mentioned in tables collected?               → YES / NO
□ Were parameters mentioned in captions/appendices also checked?  → YES / NO

Completeness check:
□ Is the training procedure fully described?                          → YES / NO
□ Is every term of the loss function defined?                         → YES / NO
□ Is missing essential information recorded in missing_but_critical?  → YES / NO

Output format check:
□ Is the output in pure YAML format?  → YES / NO
□ Are all required fields filled in?  → YES / NO

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ If even one is NO, keep extracting until it is complete!
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
