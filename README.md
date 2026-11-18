# RicciRAG

**Geometric Attention Regularization via Spectral Ricci Flow for Hallucination-Resistant Retrieval-Augmented Generation**

**Manseerat Kaur Aulakh**, Vishwanath Bijalwan, Rajni Mohana, Geetanjali Babbar
Amity School of Engineering & Technology, Amity University Punjab, Mohali, India

*Accepted at the International Conference on Emerging Digital Intelligence and Generative Engineering (EDIGE 2026), IEEE.*

## TL;DR
RAG systems degrade when the retrieved passages mix topics. RicciRAG treats **retrieval coherence as a geometric property** of the retrieved set: it computes **Ollivier–Ricci curvature** on the retrieval graph, smooths the edge weights with **discrete Spectral Ricci Flow**, and uses them to modulate transformer attention. It needs no supervision and no fine-tuning.

## Method
1. Build a graph over the top-K retrieved passages, weighted by embedding similarity.
2. Compute Ollivier–Ricci curvature on each edge (via Wasserstein-1 distances).
3. Run T steps of Spectral Ricci Flow to reshape the edge weights.
4. Use the curvature-adjusted weights to regularise attention, with strength λ.

## Key results (controlled study)
40-passage, five-domain MS MARCO-style corpus with synthetic embeddings.

| Finding | Result |
|---|---|
| Curvature separates topics | intra-topic κ = 0.401 vs. inter-topic κ = 0.229 (75% separation, consistent across all 5 domains) |
| Flow convergence | curvature range contracts by 38.5% in T = 11 steps; spectral gap stays stable |
| Retrieval topic-mismatch rate | 0.391 → 0.180 (−54.0%) |
| Retrieval quality | Precision@5 +0.187, NDCG@5 +0.081 |
| Robustness | holds for λ ∈ [0.05, 0.30] |

> **Scope:** these numbers measure *retrieval-level topic contamination*, not hallucination in the generated text. A pre-registered end-to-end protocol on TruthfulQA (with six negative controls and Holm–Bonferroni-corrected statistics) is specified and implemented but has not yet been run at scale.

## Limitations
The controlled study uses synthetic embeddings. The exact W1 solver becomes expensive above about 100 passages. Evaluation on real corpora with large language models (FactScore, TruthfulQA) is future work.

## Code
The code is not yet public.

## Citation
```bibtex
@inproceedings{aulakh2026riccirag,
  title     = {Geometric Attention Regularization via Spectral Ricci Flow for Hallucination-Resistant Retrieval-Augmented Generation},
  author    = {Aulakh, Manseerat Kaur and Bijalwan, Vishwanath and Mohana, Rajni and Babbar, Geetanjali},
  booktitle = {International Conference on Emerging Digital Intelligence and Generative Engineering (EDIGE)},
  publisher = {IEEE},
  year      = {2026},
  note      = {Accepted}
}
```
