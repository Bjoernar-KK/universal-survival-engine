# 🧬 universal-survival-engine

An end-to-end, production-grade computational oncology framework for high-dimensional multi-omics survival analysis. This repository implements an empirically validated, leakage-insulated pipeline that transitions from raw transcriptomic feature baselines to biologically-grounded graph-latent spaces and audited clinical prognosis estimators.

Developed entirely as a **Solo Research Project** by **Bjoernar KK**.

---

## 🧭 Core Philosophy: Representation Learning & The Data Firewall

High-dimensional computational oncology datasets (such as TCGA) are notoriously vulnerable to data contamination and look-ahead bias due to the severe sample-to-feature imbalance ($D \gg N$). 

This engine is engineered around two strict principles:
1. **The Strict Anti-Leakage Firewall:** To guarantee unassailable real-world generalizability, all unsupervised variance filters, data-driven binned intervals, and feature scaling (`StandardScaler`) transformations are calculated **exclusively on the active training partition** of each cross-validation fold. Out-of-sample data is completely shielded until the exact moment of inference.
2. **Objective Representation Validation:** Rather than mapping raw features directly to outcomes, the core architecture isolates, compresses, and structures high-dimensional signals into robust latent spaces, forcing the network to memorize true biological patterns over technical noise.

---

## 📊 The Objective Pipeline Flow

The engine is structured as a continuous data-refinement pipeline. Each stage introduces a precise technical constraint that builds an empirical ladder toward optimal, un-leaked prognostic evaluation:

`Stage 0 (Raw Floor)` ➔ `Stage 1 & 2 (Latent Bottleneck)` ➔ `Stage 3 (Downstream Audit)` ➔ `Stage 4 (Graph Topology)` ➔ `Stage 5 (Production Audit)`

* **Stage 0** establishes the baseline performance floor using uncompressed raw data.
* **Stages 1 & 2** act as the mathematical processor, stripping out technical noise and projecting features into a decoupled latent space.
* **Stage 3** isolates and tests the continuous embeddings to prove whether compression preserved or enhanced the prognostic signal.
* **Stage 4** advances the proven embeddings by wrapping them in structured, prior biological graph constraints.
* **Stage 5** executes the ultimate defensive QA gate, running permutation audits to guarantee absolute insulation before deploying the portable clinical estimator.


---

## 🛠️ Step-by-Step Architectural Stages

### 🎛️ Stage 0: Foundational Leakage-Free Engine
* **Technical Objective:** Train a Deep Proportional Hazards Multi-Layer Perceptron (MLP) directly on raw high-dimensional multi-omics features ($60,000+$ dimensions filtered to top-$N$ via active variance).
* **Pipeline Role:** Serves as the control group. It objectively answers: *What happens if we bypass representation learning and feed raw features into a deep survival network under airtight anti-leakage constraints?* It delivers an honest, un-leaked baseline performance score (C-Index Floor).

### 🧬 Stage 1: Joint Denoising & Discrete-Time Compression
* **Technical Objective:** Introduce a dual-task network containing a Denoising Autoencoder (DAE) structurally tied to a discrete-time conditional hazard head. Input features are intentionally corrupted with Gaussian noise/masking.
* **Pipeline Role:** Triggers representation learning. By forcing reconstruction from corrupted inputs, the network is blocked from memorizing raw data-points. The discrete-time survival loss acts as a regularizer, shaping the dense bottleneck layer to map survival risk over data-calibrated binned time intervals while throwing out technical batch effects.

### 💾 Stage 2: Decoupled & Refined Latent Spaces
* **Technical Objective:** Scale the joint architecture into a fully config-decoupled, memory-stable 128-dimensional latent bottleneck engine that exports clean, standalone patient embeddings.
* **Pipeline Role:** Concept refinement and isolation. It strips away the training heads, reads configuration structures natively from `config.yaml`, and outputs pure, 128-dimensional continuous latent vector matrices saved directly to disk. These embeddings represent the distilled essence of the input multi-omics space.

### ⚖️ Stage 3: Latent Representation Utility & Survival Benchmarking Engine
* **Technical Objective:** Transfer the Stage 2 continuous embeddings alongside Stage 0 raw vectors into classical and neural survival learners (e.g., Cox, Random Survival Forests, DeepSurv) under an identical, leakage-controlled evaluation framework.
* **Pipeline Role:** Downstream utility benchmark. By measuring discrimination (C-index) and calibration, Stage 3 objectively quantifies whether the learned representations yield performance improvements and computational efficiency relative to flat, raw feature pipelines. If Stage 2 embeddings outperform or equal Stage 0 with a fraction of the feature dimensions, the representation engine stands validated.

### 🕸️ Stage 4: Biologically-Grounded Pathway-GCN Structural Modeling Engine
* **Technical Objective:** Map high-variance genomic features onto literature-validated oncogenic signaling pathways and driver networks (e.g., Sanchez-Vega et al., 2018; KEGG). Deploy a Graph Convolutional Network (GCN) built with `torch_geometric` using a numerically stable, vectorized discrete hazard head.
* **Pipeline Role:** Paradigm shift from purely statistical representations to structurally and biologically informed graph embeddings. Building on the flat baseline verified in Stage 3, Stage 4 advances the framework by restricting node topologies to real-world functional gene-to-pathway interactions.

### 🛡️ Stage 5: Anti-Leakage Defensive Audit & Portable Production Evaluation Engine
* **Technical Objective:** Subject the high-fidelity graph embeddings generated in Stage 4 to a defensive permutation target control framework, followed by final training inside a decoupled, portable deep discrete hazard production network.
* **Pipeline Role:** The ultimate Quality Assurance gate. Stage 5 closes the pipeline loop by running defensive audits to verify that the GCN performance gains are mathematically sound, completely free of look-ahead bias, and clinically generalizable. It outputs the final, unassailable performance profile (Mean Generalizable C-Index $\pm$ Standard Deviation) via stratified 5-fold cross-validation.

---

## 🚀 Technical Requirements & Engineering Foundations

* **Zero Hard-Coding:** All hyperparameters, network layers, binned time intervals, path resolutions, and architectural configurations are injected dynamically at runtime via a centralized `config.yaml`.
* **OS-Agnostic File Management:** Built using `pathlib` for absolute compatibility across cross-platform execution environments.
* **Environment Anchoring:** Forced deterministic random seeds across PyTorch, NumPy, and system states, with non-deterministic backend optimizations strictly disabled (`torch.backends.cudnn.benchmark = False`).
