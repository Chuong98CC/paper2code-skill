# Phase 0: Reference Code Search - Optional Step

## Purpose
Before implementing a paper, **find similar implementations** to improve implementation quality.
Reference code is for **inspiration**, and the paper's original specification **always takes priority**.

---

## ⚠️ Important Principles (CRITICAL)

```
⚠️ REFERENCE CODE USAGE PRINCIPLES:

1. Reference code is for inspiration
2. The paper's original specification always takes priority
3. Understanding and application, not copying
4. Patterns found in references must also be adapted to the paper's requirements
5. License verification is mandatory

DO:
✓ Refer to structure and patterns
✓ Learn implementation tricks and optimization techniques
✓ Identify common pitfalls
✓ Refer to testing methodology

DON'T:
✗ Copy code verbatim
✗ Copy the reference implementation's bugs along with it
✗ Follow a reference's design that differs from the paper
✗ License violations
```

---

## Search Protocol

### Step 1: Analyze the Paper's References

Identify papers in the paper's References section that are likely to have a GitHub repository:

```
High-priority references:
1. Papers cited in the methodology/implementation section
2. Papers mentioned with "We build upon...", "We extend...", etc.
3. Methods used as baselines
4. Previous papers by the same authors

Exclude:
- The target paper's official implementation (if it exists, just use it)
- Purely theoretical papers
- Irrelevant background citations
```

### Step 2: Find Repositories via Web Search

Search queries using Claude's web search capability:

```
Search query patterns:

1. Direct search:
   - "[paper title] GitHub"
   - "[paper title] code repository"
   - "[author name] [paper title] implementation"

2. Algorithm-based search:
   - "[algorithm name] PyTorch implementation"
   - "[algorithm name] TensorFlow GitHub"
   - "[core methodology] code example"

3. Keyword combinations:
   - "[key term 1] [key term 2] GitHub stars:>100"
   - "[method name] official implementation"
   - "[dataset name] [method name] benchmark"

Search tips:
- Search both the paper's acronym and full name
- Check the authors' GitHub profiles
- Search Papers With Code (paperswithcode.com)
```

### Step 3: Quality Evaluation and Ranking

Evaluate discovered repositories by the following criteria:

```yaml
evaluation_criteria:
  repository_quality:  # 40% weight
    - stars: "[>100: Good, >500: Excellent]"
    - recent_activity: "[commits within 6 months: Active]"
    - documentation: "[README, docstrings quality]"
    - issues_resolved: "[issue response rate]"
    - tests: "[whether test code exists]"

  implementation_relevance:  # 30% weight
    - algorithm_match: "[whether the implemented algorithm matches the paper]"
    - completeness: "[full pipeline vs partial implementation]"
    - paper_citation: "[whether it cites the paper]"

  technical_depth:  # 20% weight
    - code_quality: "[readability, level of organization]"
    - performance: "[whether benchmark results exist]"
    - flexibility: "[configurability, extensibility]"

  academic_credibility:  # 10% weight
    - author_affiliation: "[author affiliation]"
    - official: "[whether it is the official implementation]"
    - peer_reviewed: "[peer reviewed together with the paper]"
```

### Step 4: Select and Analyze the Top 5

For each repository, record the following:

```yaml
selected_references:
  - rank: 1
    title: "[paper/repository title]"
    repository_url: "[GitHub URL]"
    relevance_score: 0.95  # 0-1 scale

    key_contributions:
      - "[what you can learn from this repository 1]"
      - "[what you can learn from this repository 2]"

    implementation_value: |
      [detailed description of how it helps the implementation]

    usage_suggestion: |
      [which parts to reference and how to apply them]

    caveats:
      - "[things to watch out for - parts that differ from the paper]"
      - "[license restrictions]"
```

---

## Output Format

```yaml
reference_search_results:
  search_summary:
    total_found: "[number of relevant repositories found]"
    evaluated: "[number of repositories evaluated]"
    selected: 5

  official_implementation:
    exists: true/false
    url: "[URL if it exists]"
    note: "[if an official implementation exists, use it first]"

  selected_references:
    - rank: 1
      title: "..."
      repository_url: "..."
      relevance_score: 0.95
      key_contributions: [...]
      implementation_value: "..."
      usage_suggestion: "..."
      caveats: [...]

    - rank: 2
      # ... same structure

    # ... rank 3, 4, 5

  search_queries_used:
    - "[search query used 1]"
    - "[search query used 2]"

  papers_with_code_link: "[PWC page URL for the paper]"
```

---

## Usage Guide

### When to Perform This Step

```
Recommended:
✓ When implementing complex algorithms
✓ When the paper lacks implementation details
✓ When implementation patterns for a specific framework (PyTorch, TensorFlow) are needed
✓ When performance optimization tips are needed

Can skip:
- Very simple algorithms
- When the paper has detailed implementation descriptions
- When you already have experience with similar implementations
- When time is limited
```

### How to Use References

```
1. Refer to structure:
   - File organization approach
   - Class/function separation patterns
   - Config management approach

2. Learn implementation tricks:
   - Numerical stability handling
   - Memory optimization
   - Parallelization techniques

3. Testing methodology:
   - Unit test structure
   - Integration test scenarios
   - Benchmark scripts

4. Identify caveats:
   - Common bug patterns
   - Performance bottlenecks
   - Environment compatibility issues
```

---

## ⚠️ Self-Check: Confirm Reference Search Is Complete

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ REFERENCE SEARCH CHECKLIST
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

□ Official implementation existence checked?     → YES / NO
□ Tried at least 3 search queries?               → YES / NO
□ Papers With Code checked?                      → YES / NO
□ Quality of discovered repositories evaluated?  → YES / NO
□ Completed detailed analysis of the top 5?      → YES / NO
□ Checked the license of each reference?         → YES / NO
□ Recorded differences from the paper (caveats)? → YES / NO

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Caveats

```
⚠️ REMEMBER:

Reference code is only supplementary material.

The final implementation must follow the paper's specification.
If you find parts in the reference code that differ from the paper,
follow the paper's specification first.

Bugs in the reference code or inconsistencies with the paper
must not be included in our implementation.
```
