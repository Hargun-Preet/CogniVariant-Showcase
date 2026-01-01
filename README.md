# 🧬 CogniVariant: AI-Powered Genomic Variant Analysis

[![Next.js](https://img.shields.io/badge/Frontend-Next.js%2016-black?style=flat-square&logo=next.js)](https://nextjs.org/)
[![FastAPI](https://img.shields.io/badge/Backend-FastAPI-009688?style=flat-square&logo=fastapi)](https://fastapi.tiangolo.com/)
[![Modal](https://img.shields.io/badge/Compute-Modal%20H100-blue?style=flat-square)](https://modal.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)

> 🔒 **Note:** The source code for this project is currently private to protect intellectual property and preserve the integrity of the active development phase.
> 
> Detailed code walkthroughs, architecture deep-dives, and live demos are available upon request for interview purposes.

CogniVariant is a full-stack genomic analysis platform that leverages the state-of-the-art **Evo 2 Large Language Model** to predict the pathogenicity of **Single Nucleotide Variants (SNVs)**. By deploying a Python backend on serverless **NVIDIA H100 GPUs** using Modal, the app provides real-time AI scoring to determine if specific DNA mutations are **Pathogenic** or **Benign**.

---

## 🚀 Project Overview

DNA is the "source code" of life, represented by the bases **A, T, G, and C**. Small changes—mutations—can lead to significant health risks. For example, a single nucleotide swap in the **BRCA1** gene can dramatically increase cancer susceptibility.

CogniVariant bridges the gap between raw genomic data and clinical insight, allowing users to:

- **Analyze**: Search for specific genes (e.g., BRCA1) and browse their reference sequences.
- **Predict**: Use the Evo 2 model to calculate pathogenicity scores for custom mutations.
- **Validate**: Compare AI predictions against established [ClinVar](https://www.ncbi.nlm.nih.gov/clinvar/) classifications (Pathogenic / Benign).

---

## 🏗️ System Architecture

### 1. Backend Architecture (Modal + GPU Lifecycle)
*Orchestration of container lifecycles to minimize H100 cold starts.*

<img width="800" alt="Backend Flow" src="https://github.com/user-attachments/assets/642b9bfc-c3be-4993-89fe-5d0313ab04f7" />

### 2. Frontend Data Flow
*Federated data architecture fetching live genomic data from UCSC and NCBI APIs.*

<img width="800" alt="Frontend Sequence" src="https://github.com/user-attachments/assets/13e3a057-afee-48ad-af52-7e48c59c342e" />

### 💡 Technical Highlights:

- **Cold Start Optimization**: To handle the massive size of the Evo 2 model, I implemented a custom Modal Lifecycle Hook (@enter). This pre-loads the model into GPU memory when the container starts, rather than on every request.

- **Smart Caching**: Model weights are stored in a persistent Modal Volume mapped to /.cache/huggingface, preventing expensive re-downloads on every deployment.

- **Federated Data Architecture**: The app does not store terabytes of genomic data. Instead, it acts as an intelligent orchestrator, fetching reference sequences live from UCSC and clinical data from NCBI/ClinVar, ensuring the data is always up-to-date.
---

## ✨ Key Features

- 🧠 **Evo 2 Core**: High-fidelity variant effect prediction using the latest Evo 2 genomic foundation model.
- ⚡ **Serverless GPU Compute**: Backend hosted on **Modal**, utilizing NVIDIA H100s for high-performance, low-latency inference.
- 🔍 **Interactive Genome Browser**: Explore genome assemblies (hg38) and search for genes via UCSC and NCBI APIs.
- ⚖️ **ClinVar Comparison**: Side-by-side view of AI-predicted scores vs. official ClinVar clinical classifications.
- 🎨 **Modern T3 Stack**: Built with Next.js 14, TypeScript, Tailwind CSS, and Shadcn UI.

---

## 🔬 The Science: Evo 2 Model

Evo 2 is a breakthrough genomic foundation model based on the **StripedHyena 2** architecture. It was trained exclusively on the "language of biology" across all domains of life using the **Savanna** framework.

- **Official Repository**: [Arc Institute – Evo 2 GitHub](https://github.com/arcinstitute/evo2)
- **Research Paper**: [Genome modeling and design across all domains of life with Evo 2 (bioRxiv 2025)](https://www.biorxiv.org/content/10.1101/2025.02.18.638918v1)

### How It Works

Evo 2 treats individual nucleotides (A, T, G, C) as tokens, learning the statistical "grammar" of healthy DNA at single-nucleotide resolution with up to **1 million base pair context lengths**.

The model calculates the **Log-Likelihood Ratio (LLR)** for a mutation:

$$\text{LLR} = \log\left(\frac{P(\text{mutant})}{P(\text{reference})}\right)$$

#### Interpretation
- **Low / Negative LLR**: Mutation is unlikely/surprising $\rightarrow$ likely **Pathogenic**.
- **High / Neutral LLR**: Mutation fits biological context $\rightarrow$ likely **Benign**.

---

## 🛠️ Tech Stack

| Layer | Technologies |
| :--- | :--- |
| **Frontend** | Next.js 14, React, TypeScript, Tailwind CSS, Shadcn UI |
| **Backend** | [Python 3.12](https://www.python.org/downloads/), FastAPI, [Modal](https://modal.com/) (Serverless H100 GPU) |
| **AI / ML** | Evo 2 (LLM), PyTorch, Transformer Engine |
| **Data APIs** | UCSC Genome Browser API, NCBI E-utilities (ClinVar) |

---

### 📂 Project Structure
```plaintext

📂 CogniVariant
├── 📂 evo2-backend         # Python/Modal Logic
│   ├── 📄 main.py          # Modal entry point & @enter logic
│   ├── 📄 requirements.txt # PyTorch, StripedHyena, etc.
│   └── 📂 utils            # Sequence tokenization helpers
├── 📂 evo2-frontend        # Next.js Application
│   ├── 📂 src
│   │   ├── 📂 components   # GenomeBrowser, VariantCard, Heatmap
│   │   ├── 📂 hooks        # Custom hooks for UCSC/NCBI APIs
│   │   └── 📄 page.tsx     # Main dashboard
│   └── 📄 tailwind.config  # Styling configuration
└── 📄 README.md            # You are here
```

---

## 📄 License
Distributed under the MIT License. See LICENSE for more information.

## 🤝 Acknowledgments
Special thanks to the Arc Institute for releasing the Evo 2 model and weights.

## Research Citation:
Brixi, G., et al. (2025). Genome modeling and design across all domains of life with Evo 2. [bioRxiv](https://www.biorxiv.org/content/10.1101/2025.02.18.638918v1).

---

## 📬 Contact for Access
Want to see the code? Due to the competitive nature of the project, the source is private. [Request Access for Interview](mailto:singhhargun077@gmail.com?subject=Request%20Access%20to%20CogniVariant%20Repo)

---


