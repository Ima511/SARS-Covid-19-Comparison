<div align="center">

<img src="https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
<img src="https://img.shields.io/badge/Biopython-1.81-darkgreen?style=for-the-badge"/>
<img src="https://img.shields.io/badge/scikit--learn-ML-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white"/>
<img src="https://img.shields.io/badge/ESMFold-AI%20Structure-blueviolet?style=for-the-badge"/>
<img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge"/>

<br><br>

# 🧬 SpikeScope — SARS-CoV-2 Spike Protein Mutation Analyzer

### *An AI-powered computational pipeline for variant comparison, structural analysis, and mutation risk prediction*

<br>

[![Live Tool](https://img.shields.io/badge/🌐%20Live%20Web%20Tool-Click%20to%20Open-00d4ff?style=for-the-badge)](https://ima511.github.io/SARS-Covid-19-Comparison/)
[![GitHub](https://img.shields.io/badge/GitHub-Ima511-181717?style=for-the-badge&logo=github)](https://github.com/Ima511/SARS-Covid-19-Comparison)

</div>

---

## 📌 Overview

**SpikeScope** is a full computational biology pipeline that performs comparative genomic and structural analysis of SARS-CoV-2 spike protein variants. Built entirely with Python and Biopython, it integrates classical sequence alignment, AI-based 3D structure prediction, ACE2 binding site analysis, and machine learning — all wrapped in an interactive browser-based visualization tool.

This project was developed as part of original undergraduate research into spike protein mutational evolution across COVID-19 variants of concern (VOC).

---

## 🎯 Research Question

> *"How do specific mutations in the SARS-CoV-2 spike protein alter its 3D structure and ACE2 receptor binding affinity — and can machine learning predict which mutations are clinically dangerous?"*

---

## ✨ Key Features

| Feature | Description |
|---|---|
| 🔗 **Global Sequence Alignment** | Needleman-Wunsch pairwise alignment across all major variants |
| 🗺️ **Mutation Mapping** | Visual position-by-position mutation map with density plots |
| 🤖 **AI Structure Prediction** | ESMFold API integration for 3D protein structure prediction |
| 📊 **pLDDT Confidence Analysis** | Structural stability comparison using ESMFold confidence scores |
| 🎯 **ACE2 Binding Site Analysis** | Tracks mutations at all 24 known ACE2 contact residues |
| 🧪 **Physicochemical Profiling** | Molecular weight, isoelectric point, GRAVY, instability index |
| 🌡️ **Similarity Heatmap** | Cross-variant identity matrix across Wild Type, Alpha, Delta, Omicron, XBB |
| 🤖 **ML Risk Classifier** | Random Forest classifier predicting mutation danger using physicochemical features |
| 🌐 **Interactive Web Tool** | Browser-based SpikeScope tool — no installation needed |

---

## 🦠 Variants Analyzed

```
Wild Type  ──────────────────────────────────── Wuhan-Hu-1 (Reference)
    │
    ├──▶  Alpha   (B.1.1.7)    [NCBI: QVE55289]
    │
    ├──▶  Delta   (B.1.617.2)  [NCBI: QWK65231]
    │         │
    │         └──▶  Omicron  (B.1.1.529) [NCBI: UHV89245]
    │                   │
    │                   └──▶  XBB  [NCBI: UQV14743]
    │
    └──▶  Wild Type            [NCBI: QHD43416]
```

---

## 🗂️ Project Structure

```
SARS-Covid-19-Comparison/
│
├── index.html                    # 🌐 SpikeScope interactive web tool
├── covid_analysis_pipeline.py    # 🐍 Full Biopython analysis pipeline
│
├── outputs/
│   ├── similarity_heatmap.png    # Cross-variant identity matrix
│   ├── mutation_map.png          # Delta vs Omicron mutation positions
│   ├── structural_comparison.png # ESMFold pLDDT confidence plot
│   ├── ml_results.png            # Random Forest results + confusion matrix
│   ├── feature_importance.png    # ML feature importance chart
│   ├── Delta_structure.pdb       # Predicted 3D structure — Delta
│   ├── Omicron_structure.pdb     # Predicted 3D structure — Omicron
│   └── WildType_structure.pdb    # Predicted 3D structure — Wild Type
│
└── README.md
```

---

## 🚀 Quick Start

### Option 1 — Use the Web Tool (No Setup Needed)

👉 **[Open SpikeScope in your browser](https://ima511.github.io/SARS-Covid-19-Comparison/)**

```
1. Click on Sequence 1 box  →  ACTIVE badge appears
2. Click a variant chip      →  Sequence loads into that box
3. Click on Sequence 2 box  →  ACTIVE badge switches
4. Click another variant     →  Second sequence loads
5. Click ⚡ Analyze Mutations →  Full results in seconds
```

---

### Option 2 — Run the Python Pipeline

#### Prerequisites

```bash
pip install biopython numpy pandas scipy matplotlib seaborn scikit-learn requests
```

#### Verify Installation

```python
import Bio, numpy, pandas, sklearn, matplotlib, seaborn, requests
print("All packages ready!")
print(f"Biopython version: {Bio.__version__}")
```

#### Run the Pipeline

```bash
git clone https://github.com/Ima511/SARS-Covid-19-Comparison.git
cd SARS-Covid-19-Comparison
python covid_analysis_pipeline.py
```

> ⚠️ Add your email to `Entrez.email = "your@email.com"` before running — required by NCBI.

---

## 🔬 Pipeline Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    ANALYSIS PIPELINE                            │
│                                                                 │
│  PHASE 1  →  Fetch sequences from NCBI via Entrez API           │
│     ↓                                                           │
│  PHASE 2  →  Physicochemical property analysis                  │
│     ↓                                                           │
│  PHASE 3  →  Cross-variant similarity heatmap                   │
│     ↓                                                           │
│  PHASE 4  →  Deep mutation analysis (Needleman-Wunsch)          │
│             → Substitutions / Insertions / Deletions            │
│     ↓                                                           │
│  PHASE 5  →  AI structure prediction (ESMFold API)              │
│             → Saves .pdb files for PyMOL visualization          │
│     ↓                                                           │
│  PHASE 6  →  Structural confidence comparison (pLDDT scores)    │
│             → Highlights disordered vs stable regions           │
│     ↓                                                           │
│  PHASE 7  →  ACE2 contact residue analysis                      │
│             → Tracks all 24 key binding positions               │
│     ↓                                                           │
│  PHASE 8  →  Random Forest ML classifier                        │
│             → Predicts mutation risk: Neutral / Dangerous        │
│             → Feature importance + ROC-AUC evaluation           │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📊 Results Summary

### Sequence Identity Matrix

| Variant | Wild Type | Alpha | Delta | Omicron | XBB |
|---|---|---|---|---|---|
| **Wild Type** | 100% | ~99.7% | ~99.6% | ~98.2% | ~97.8% |
| **Alpha** | ~99.7% | 100% | ~99.3% | ~98.0% | ~97.5% |
| **Delta** | ~99.6% | ~99.3% | 100% | ~98.1% | ~97.6% |
| **Omicron** | ~98.2% | ~98.0% | ~98.1% | 100% | ~99.1% |
| **XBB** | ~97.8% | ~97.5% | ~97.6% | ~99.1% | 100% |

> *Values are approximate. Run the pipeline for exact figures.*

### Key ACE2 Contact Mutations — Delta vs Omicron

```
Position 417  :  K → N   ⚠️  HIGH RISK   — Known immune escape mutation
Position 484  :  E → A   ⚠️  HIGH RISK   — Reduces antibody neutralization
Position 493  :  Q → R   ⚠️  HIGH RISK   — Enhanced ACE2 binding
Position 501  :  N → Y   ⚠️  HIGH RISK   — Increased transmissibility
Position 505  :  Y → H   ⚡  MEDIUM RISK  — Structural change at contact site
```

### ML Classifier Performance

```
              precision    recall    f1-score
Neutral           0.97      0.98        0.97
Dangerous         0.85      0.82        0.83

ROC-AUC Score:  0.91
```

---

## 🌐 SpikeScope Web Tool Features

The `index.html` is a fully self-contained interactive tool:

```
🔵  Click-to-select active sequence boxes
🟢  5 variant quick-load chips (WT / Alpha / Delta / Omicron / XBB)
📊  Real-time sequence identity percentage bar
🗺️  Visual mutation position map with RBD region highlight
🎯  ACE2 contact site status (24 positions, color coded)
⚠️  Mutation risk table — HIGH / MEDIUM / LOW
🔗  Full alignment viewer with color-coded matches and mismatches
🧪  Physicochemical property comparison panel
⬇️  Export all mutations as CSV
📄  Export full analysis as text report
```

---

## 🧪 Key Biological Concepts

| Concept | Tool Used | Purpose |
|---|---|---|
| Global sequence alignment | Needleman-Wunsch (Biopython) | Full-length sequence comparison |
| Protein structure prediction | ESMFold (Meta AI) | 3D conformation from sequence |
| Structural confidence | pLDDT score | Identify flexible/disordered regions |
| Binding site analysis | ACE2 contact residues from literature | Find functionally critical mutations |
| Mutation classification | Physicochemical property delta | Conservative vs non-conservative |
| Risk prediction | Random Forest (scikit-learn) | Predict clinical danger of mutations |

---

## 📚 Dependencies

```python
biopython    >= 1.81   # Sequence analysis, NCBI Entrez, alignment
numpy        >= 1.24   # Numerical computing
pandas       >= 2.0    # Data manipulation
scipy        >= 1.10   # Statistical analysis
matplotlib   >= 3.7    # Plotting and figure generation
seaborn      >= 0.12   # Heatmaps and statistical visualization
scikit-learn >= 1.3    # Random Forest ML classifier
requests     >= 2.28   # ESMFold API calls
```

---

## 🗃️ Data Sources

| Database | Data Used | Accession IDs |
|---|---|---|
| **NCBI Protein** | Spike protein sequences | QHD43416, QVE55289, QWK65231, UHV89245, UQV14743 |
| **ESMFold API** | AI 3D structure prediction | api.esmatlas.com |
| **Literature** | ACE2 contact residues | Lan et al. 2020, Nature |

---

## 🔭 Future Work

- [ ] Add phylogenetic tree visualization using `Bio.Phylo`
- [ ] Integrate AlphaFold2 for higher-resolution structure prediction
- [ ] Expand ML classifier with BLOSUM62 substitution matrix features
- [ ] Add protein-protein docking score for ACE2 binding affinity
- [ ] Support user-uploaded custom sequences in web tool
- [ ] Add JN.1 and KP.2 variant sequences
- [ ] Deploy web tool on Streamlit for Python-powered backend

---

## 👨‍🔬 Author

**Ima511**  
Student | Software Engineer 
🔗 [GitHub Profile](https://github.com/Ima511)

---

## 📖 Citation

If you use this tool or pipeline in your research, please cite:

```bibtex
@misc{spikescope2025,
  author       = {Ima511},
  title        = {SpikeScope: AI-Powered SARS-CoV-2 Spike Protein Mutation Analyzer},
  year         = {2025},
  publisher    = {GitHub},
  journal      = {GitHub repository},
  howpublished = {\url{https://github.com/Ima511/SARS-Covid-19-Comparison}}
}
```

Also cite Biopython:
> Cock et al. (2009). Biopython: freely available Python tools for computational molecular biology and bioinformatics. *Bioinformatics*, 25(11), 1422–1423.

---

## 📄 License

This project is licensed under the **MIT License** — see [LICENSE](LICENSE) for details.

---

<div align="center">

```
Made with 🧬 Python · Biopython · ESMFold · scikit-learn
```

⭐ **Star this repo if it helped your research!** ⭐

</div>
