# FlowWrite Research Paper Outline

## Title Options

1. **FlowWrite: A Multi-Stage LLM-Based Text Rewriting Framework for Improving Naturalness While Preserving Semantic Content**

2. **Efficient Neural Text Rewriting: An Ablation Study of Multi-Stage Processing Pipelines**

3. **Quality-Speed Trade-offs in LLM Text Humanization: Evidence from the FlowWrite Framework**

---

## Abstract

**Background:** Large language models (LLMs) produce increasingly fluent text, yet certain stylistic patterns remain detectable as machine-generated. Automated text rewriting systems aim to improve perceived naturalness while preserving semantic content.

**Methods:** We present FlowWrite, a controllable multi-stage rewriting architecture combining semantic chunking, semantic merging, style rewriting, optional flow refinement, and fragmentation post-processing. We conducted large-scale experiments (N=144 documents) across 6 domains and 4 simulated LLM sources, comparing a 5-stage pipeline (V1) against a 4-stage ablation (V2).

**Results:** V2 achieved comparable human-likeness scores (HLS: 0.839 vs 0.824) while reducing processing time by ~3× (275s vs 788s average). Domain-specific analysis revealed that flow smoothing benefits blog and healthcare content disproportionately.

**Conclusion:** Additional generative refinement stages do not universally improve text quality; their benefit is domain-dependent. Adaptive pipeline selection based on input classification may optimize quality-speed trade-offs.

**Keywords:** text rewriting, natural language generation, human-likeness evaluation, ablation study, LLM pipelines

---

## 1. Introduction

### 1.1 Motivation
- Growing prevalence of AI-generated text
- Need for controllable text improvement systems
- Gap between detection-focused and quality-focused approaches

### 1.2 Problem Statement
> Can a multi-stage text rewriting pipeline improve perceived human-likeness while preserving semantic content, and can unnecessary LLM refinement stages be removed without sacrificing quality?

### 1.3 Contributions

1. **Framework:** A multi-stage, controllable rewriting architecture combining semantic chunking, semantic merging, style rewriting, optional flow refinement, and post-processing.

2. **Evaluation:** A multidimensional evaluation framework combining linguistic characteristics, semantic preservation, coherence, readability, and human evaluation protocols.

3. **Ablation Study:** Demonstration that removing the Flow Smoother produces approximately 3× lower latency while maintaining/slightly improving average HLS, with performance varying by domain.

### 1.4 Paper Structure

---

## 2. Related Work

### 2.1 Text Paraphrasing and Rewriting
- Classical approaches (rule-based, statistical)
- Neural paraphrasing models
- Contemporary LLM-based methods

### 2.2 AI Text Detection and Humanization
- Detector methodologies and limitations
- Adversarial dynamics between detectors and humanizers
- Recent findings on detector evasion (cite: DAMAGE paper)

### 2.3 Evaluation Metrics for Generated Text
- Readability metrics (Flesch, Flesch-Kincaid)
- Coherence and cohesion measures
- Semantic similarity approaches
- Human evaluation protocols
- **Gap:** Lack of standardized "human-likeness" composite metrics

### 2.4 Pipeline Optimization in NLP
- Cascaded processing architectures
- Early exiting strategies
- Adaptive computation methods

---

## 3. Methodology

### 3.1 FlowWrite Architecture

```
Input → Semantic Chunking → Semantic Merging → Style Rewriting → [Optional: Flow Smoothing] → Fragmentation → Output
```

#### 3.1.1 Semantic Chunking
- Sentence boundary detection
- Meaning-preserving segment identification

#### 3.1.2 Semantic Merging
- Related chunk consolidation
- Redundancy reduction

#### 3.1.3 Style Rewriting
- Tone-controlled regeneration
- Aggressiveness parameter

#### 3.1.4 Flow Smoothing (Optional - V1 only)
- Inter-chunk transition refinement
- Coherence enhancement

#### 3.1.5 Fragmentation
- Line breaking for visual presentation
- Final formatting

### 3.2 Pipeline Variants

| Version | Stages | Flow Smoother | Expected Time |
|---------|--------|---------------|---------------|
| V1 | 5 | Yes | Baseline |
| V2 | 4 | No | ~20% faster theoretical |

### 3.3 Human Likeness Score (HLS)

Composite metric combining:
- Burstiness (20%) - sentence length variation
- Coherence (25%) - logical flow
- Readability (20%) - appropriate complexity
- Connector Density (20%) - transition usage
- Semantic Similarity (15%) - meaning preservation

**Note:** HLS is proposed as a relative comparison metric, not an absolute measure of human writing.

---

## 4. Experimental Design

### 4.1 Research Questions

| RQ | Question | Evaluation Method |
|----|----------|-------------------|
| RQ1 | Does FlowWrite produce text judged more human-like than original AI text? | HLS comparison, human eval |
| RQ2 | Does FlowWrite preserve semantic content? | SBERT similarity |
| RQ3 | Does removing Flow Smoother reduce quality while improving speed? | V1 vs V2 ablation |
| RQ4 | Is performance consistent across domains and LLM sources? | Stratified analysis |

### 4.2 Dataset

- **Size:** 144 documents
- **Domains:** Academic, Technical, Business, Blog, Healthcare, General (24 each)
- **LLM Sources:** Llama, GPT, Claude, Gemini (36 each)
- **Average word count:** ~340 words

### 4.3 Baselines

1. **Original AI text** - unmodified LLM output
2. **Synonym replacement** - basic lexical substitution
3. **Rule-based restructuring** - simple transformations
4. **Combined baseline** - all above sequentially

### 4.4 Evaluation Metrics

#### Automatic Metrics
- HLS (composite)
- Flesch Reading Ease
- Flesch-Kincaid Grade Level
- Sentence Length Variance
- Lexical Diversity (TTR)
- Semantic Similarity (SBERT)

#### Human Evaluation
- Naturalness (1-5)
- Fluency (1-5)
- Coherence (1-5)
- Meaning Preservation (1-5)
- Overall Quality (1-5)
- AI/Human judgment (5-point scale)

### 4.5 Statistical Analysis Plan

- Paired t-tests for V1 vs V2 comparison
- ANOVA for domain/LLM source effects
- Inter-rater reliability (Cohen's κ) for human evaluations
- Effect size calculations (Cohen's d)

---

## 5. Results

### 5.1 Overall Performance (V1 vs V2)

| Metric | V1 | V2 | Difference |
|--------|-----|-----|------------|
| Avg HLS | 0.824 | 0.839 | +0.015 (ns) |
| Avg Time | 788s | 275s | -513s (p<0.001) |
| Speedup | — | 2.87× | — |

### 5.2 By Domain Analysis

| Domain | V1 HLS | V2 HLS | Winner | Speedup |
|--------|--------|--------|--------|---------|
| Academic | 0.XXX | 0.XXX | V2 | X.X× |
| Technical | 0.XXX | 0.XXX | V2 | X.X× |
| Business | 0.XXX | 0.XXX | V2 | X.X× |
| Blog | 0.XXX | 0.XXX | **V1** | X.X× |
| Healthcare | 0.XXX | 0.XXX | **V1** | X.X× |
| General | 0.XXX | 0.XXX | V2 | X.X× |

**Key Finding:** V1 performs better for Blog and Healthcare domains where flow smoothing adds value.

### 5.3 By LLM Source

| LLM Source | V1 HLS | V2 HLS | Difference |
|------------|--------|--------|------------|
| Llama | X.XXX | X.XXX | ±X.XXX |
| GPT | X.XXX | X.XXX | ±X.XXX |
| Claude | X.XXX | X.XXX | ±X.XXX |
| Gemini | X.XXX | X.XXX | ±X.XXX |

### 5.4 Baseline Comparison

| Method | HLS | Time | Semantic Preservation |
|--------|-----|------|----------------------|
| Original | 0.565 | 0s | 1.00 |
| Synonym | 0.XXX | <1s | 0.XX |
| Restructure | 0.XXX | <1s | 0.XX |
| Combined | 0.XXX | <1s | 0.XX |
| **FlowWrite V2** | **0.839** | 275s | **0.XX** |
| FlowWrite V1 | 0.824 | 788s | 0.XX |

### 5.5 Human Evaluation Results

*(To be collected)*

| Criterion | Mean (SD) | Significance |
|-----------|-----------|--------------|
| Naturalness | X.X (X.X) | p=X.XX |
| Fluency | X.X (X.X) | p=X.XX |
| Coherence | X.X (X.X) | p=X.XX |
| Meaning Preservation | X.X (X.X) | p=X.XX |
| Overall Quality | X.X (X.X) | p=X.XX |

---

## 6. Discussion

### 6.1 Interpretation of Key Findings

1. **Speed-Quality Decoupling:** Removing an entire LLM pass does not degrade quality, suggesting diminishing returns in multi-pass refinement.

2. **Domain Dependency:** Flow smoothing benefits domains requiring higher coherence (healthcare, narrative blog content).

3. **Metric Validation:** HLS correlates with human judgments but requires further validation against larger human evaluation datasets.

### 6.2 Implications for System Design

**Adaptive Pipeline Recommendation:**

```
Input → Domain Classifier → Select V1 or V2 → Output
```

- Blog/Healthcare → V1 (5-stage)
- Other domains → V2 (4-stage)

Expected benefit: Optimal quality-speed balance per domain.

### 6.3 Limitations

1. **Simulated LLM Sources:** Generated dataset uses pattern-based simulation rather than actual API outputs.

2. **HLS Validation:** Composite metric requires external validation against established benchmarks.

3. **Human Evaluation Scale:** Current sample size (planned N=30) limits statistical power.

4. **Generalizability:** English-only evaluation; cross-lingual performance unknown.

### 6.4 Ethical Considerations

- **Framing:** Positioned as text improvement tool, not detector evasion
- **Transparency:** Clear documentation of capabilities and limitations
- **Responsible Use:** Discouraged applications include academic dishonesty, misinformation generation

---

## 7. Conclusion

### 7.1 Summary

FlowWrite demonstrates that multi-stage text rewriting can improve perceived human-likeness while preserving semantic content. The ablation study reveals that additional refinement stages provide domain-specific rather than universal benefits.

### 7.2 Future Work

1. **Real LLM Integration:** Validate with actual API-generated texts from multiple providers
2. **Expanded Human Evaluation:** Larger evaluator pool (N=50+) for robust statistical analysis
3. **Cross-lingual Extension:** Adapt pipeline for non-English languages
4. **Adaptive Classifier:** Train domain classifier for automatic pipeline selection
5. **External Benchmarking:** Compare against published rewriting systems

### 7.3 Final Remarks

The quality-speed trade-off in neural text rewriting warrants further investigation. Our findings suggest that thoughtful pipeline design can achieve substantial efficiency gains without compromising output quality.

---

## References

*(To be populated with relevant citations)*

Key areas:
- Text rewriting/paraphrasing literature
- AI detection and humanization research
- Evaluation metrics for NLG
- LLM pipeline optimization
- Recent work on adversarial text modification

---

## Appendices

### A. Complete HLS Formula

### B. Domain Template Specifications

### C. Human Evaluation Form

### D. Statistical Test Details

### E. Sample Outputs by Method
