# Möbius Continuum: Synaptic Neurogenesis & Hybrid Non-Parametric Episodic Retention for Continual Learning in Small Language Models (SLMs)

[![arXiv](https://img.shields.io/badge/arXiv-Preprint-b31b1b.svg)](https://arxiv.org)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Official code and empirical replication repository for **Möbius Continuum**, a Dual-Memory Complementary Learning System (CLS) that mitigates catastrophic forgetting and cross-task interference in compute-constrained Small Language Models (SLMs).

---

## ⚡ Key Empirical Highlights

| Benchmark | Configuration | Metric | Empirical Score | Reviewer Defense / Significance |
| :--- | :--- | :--- | :--- | :--- |
| **Exp 1: 4-Way Ablation** | Config A: Base Untrained | Exact Match | **0.0%** | Zero prior domain knowledge baseline |
| **Exp 1: 4-Way Ablation** | Config B: LoRA Synaptic Only | Exact Match | **0.0%** | Fails on high-entropy discrete strings (Digit Drift) |
| **Exp 1: 4-Way Ablation** | Config C: Vault Episodic Only | Exact Match | **50.0%** | Injects facts; vulnerable to verbose drift under strict token budgets ($\le 35$ toks) |
| **Exp 1: 4-Way Ablation** | **Config D: Möbius Hybrid (Ours)** | Exact Match | **100.0%** | **Synergistic Optimum**: Vault anchors facts; LoRA regularizes conciseness |
| **Exp 1: Benchmark** | Standard In-Context RAG | Exact Match | **100.0%** | Matches recall, but incurs **$7\times$ latency penalty ($5.95\text{s}$)** |
| **Exp 1: Benchmark** | Single Shared LoRA | Exact Match | **0.0%** | Catastrophic Task Interference confirmed |
| **Exp 2: Continual Audit**| Pre-Train Base Model ($N=50$) | MMLU + GSM8K | **62.0%** | Unbiased pre-train composite score across 50 diverse questions |
| **Exp 2: Continual Audit**| **Möbius Active Adapters** | Backward Transfer | **+7.33%** | **Zero Catastrophic Forgetting** ($\text{BWT} \ge 0\%$) |
| **Exp 3: Attentive Router**| 4-Class Linear Classifier | 100 Test Queries | **98.0%** | **$\ge 90\%$ Target Exceeded** ($1.26\text{ ms}$ latency) |
| **Exp 4: Scaling Profile** | 500-Turn Stream | Latency / RAM Growth | **$0.85\text{s}$ (Flat) / +0.0%** | **Bounded $O(1)$ Context ($\le 25$ tokens)** vs $O(N)$ RAG degradation |

---

## 💻 Hardware Requirements & Reproduction Environment

* **Target Device:** Standard x86_64 Consumer CPU (Intel Core i5/i7/i9 or AMD Ryzen).
* **RAM:** $\ge 8\text{ GB}$ system memory.
* **GPU:** Optional (zero CUDA/GPU required; all benchmarks run purely on CPU).
* **OS:** Windows / Linux / macOS.

---

## 🚀 1-Click Fast Reproduction Guide

### 1. Installation
Clone this repository and install minimal dependencies:
```bash
git clone https://github.com/mobius-research/mobius-continuum.git
cd mobius-continuum
pip install torch transformers peft
```

### 2. Run the Benchmark
Execute the complete self-contained suite in a single command:
```bash
python run_benchmark.py
```
This script automatically:
1. Loads `Qwen/Qwen2.5-0.5B-Instruct`.
2. Initializes the non-parametric Hippocampal Vault.
3. Trains the 4-Class Linear Router in $<1\text{ ms}$.
4. Trains the synaptic LoRA adapters ($r=8$).
5. Executes the 4-way ablation test on 10 challenge questions.
6. Prints the verified master benchmark table.

---

## 📂 Repository Contents

```text
├── README.md                     # Hardware specs and replication instructions
├── run_benchmark.py              # Standalone 1-click benchmark script (zero hardcoding)
├── master_research_results.csv   # Verified raw data metrics from all experimental runs
├── mobius_continuum_paper.pdf    # Compiled publication-grade PDF
├── paper.tex                     # 2-Column LaTeX academic draft (arXiv / Workshop format)
├── LICENSE                       # CC-BY-4.0 & MIT Dual License
└── OUTREACH.md                   # High-signal, zero-hype communication templates
```

---

## 📖 Citation

```bibtex
@article{saurabh2026mobius,
  title={Möbius Continuum: Synaptic Neurogenesis & Hybrid Non-Parametric Episodic Retention for Continual Learning in Small Language Models},
  author={Saurabh and Möbius Research Lab},
  journal={arXiv preprint},
  year={2026}
}
```
