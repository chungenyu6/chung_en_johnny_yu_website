# (STOPPED) SCoOP: Semantic Consistent Opinion Pooling for Uncertainty Quantification in Multiple Vision Language Model Systems 


- [Chung-En Johnny Yu](https://scholar.google.com/citations?user=OQ6yRW0AAAAJ), [Brian Jalaian](https://scholar.google.com/citations?user=exiqJqcAAAAJ), and [Nathaniel D Bastian](https://scholar.google.com/citations?user=M2aMMxQAAAAJ)
- \[[Website](research/2026/scoop/scoop)\] \[[arXiv](https://arxiv.org/abs/2603.23853v1)\] \[[GitHub](https://github.com/chungenyu6/SCoOP)\]

## Abstract

Combining multiple Vision-Language Models (VLMs) can enhance multimodal reasoning and robustness, but aggregating heterogeneous models' outputs amplifies uncertainty and increases the risk of hallucinations. We propose SCoOP (Semantic-Consistent Opinion Pooling), a training-free uncertainty quantification (UQ) framework multi-VLM systems through uncertainty-weighted linear opinion pooling. Unlike prior UQ methods designed for single models, SCoOP explicitly measures collective, system-level uncertainty across multiple VLMs, enabling effective hallucination detection and abstention for highly uncertain samples. On ScienceQA, SCoOP achieves an AUROC of 0.866 for hallucination detection, outperforming baselines (0.732-0.757) by approximately 10-13%. For abstention, it attains an AURAC of 0.907, exceeding baselines (0.818-0.840) by 7-9%. Despite these gains, SCoOP introduces only microsecond-level aggregation overhead relative to the baselines, which is trivial compared to typical VLM inference time (on the order of seconds). These results demonstrate that SCoOP provides an efficient and principled mechanism for uncertainty-aware aggregation, advancing the reliability of multimodal AI systems.

## How it Works

SCOOP unifies the outputs of different VLMs into a single probability space without requiring additional training or labeled data.

### The Workflow:

1. **Query & Sample:** Multiple VLMs (e.g., Gemma, InternVL, DeepSeek) receive the same input and generate several responses.
    
2. **Semantic Clustering:** Responses are mapped to a unified set of options.
    
3. **Uncertainty Weighting:** Each model is assigned a weight based on its individual confidence (inverse of its entropy).
    
4. **Opinion Pooling:** The system aggregates these weighted opinions to produce a final response and a system-level uncertainty score. 

![System Overview](research/2026/scoop/overview)

> **Figure 1: System Overview.** SCOOP detects hallucinations by calculating a collective system uncertainty score across heterogeneous models.
> 

---

## Key Results

### 1. Superior Hallucination Detection

On the ScienceQA benchmark, SCOOP achieves an **AUROC of 0.866**, outperforming standard aggregation methods like Majority Voting and Naive Selection by **10-13%**.

### 2. Reliable Abstention

SCOOP allows systems to "know when they don't know". It attains an **AURAC of 0.907**, meaning it can effectively reject highly uncertain samples to maintain high overall system accuracy.

> **Figure 3: Performance Comparison**SCOOP consistently provides better separation of hallucinatory and correct responses compared to individual VLMs or unweighted baselines.
> 

### 3. Trivial Overhead

Despite the massive gains in reliability, SCOOP adds only **microsecond-level latency** for aggregation. This is negligible compared to the seconds-long inference time of typical VLMs, making it ready for real-world deployment.

---

## Why SCOOP?

- 
    
    **Training-Free:** Works with off-the-shelf, black-box VLMs.
    
- 
    
    **Scalable:** Maintains dominant performance gains as you scale from small to extra-large model parameters.
    
- 
    
    **Robust:** Extends reliability signals even when individual models in the system are performing poorly.
    