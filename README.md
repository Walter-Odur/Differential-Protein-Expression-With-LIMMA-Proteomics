# Proteomics Tutorial: Differential Protein Expression Analysis in Tamoxifen-Resistant ER+ Breast Cancer

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![R](https://img.shields.io/badge/R-%3E%3D4.3-blue.svg)](https://www.r-project.org/)
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey.svg)]()

A complete, reproducible, publication-quality label-free quantitative (LFQ) proteomics pipeline analyzing tamoxifen resistance in estrogen receptor-positive (ER+) breast cancer.

---

## Overview

This tutorial implements an end-to-end clinical proteomics workflow from raw MaxQuant output to validated biomarker candidates. It was developed as a graduate-level assignment at Makerere University and demonstrates best practices in computational proteomics.

### What You Will Learn

| Step | Topic | Key Methods |
|------|-------|-------------|
| 1 | Data import and cleaning | Contaminant removal, zero-to-NA conversion |
| 2 | Quality control | PCA batch detection, outlier flagging |
| 3 | Filtering and transformation | 70% valid values filter, log2 transform |
| 4 | Missing value imputation | Sequential regression (Impseq) for MNAR data |
| 5 | Exploratory analysis | PCA, correlation heatmaps |
| 6 | Differential expression | limma with empirical Bayes (trend + robust) |
| 7 | Results visualization | Volcano plot, heatmaps, boxplots |
| 8 | Functional enrichment | GO, KEGG, Reactome, GSEA |
| 9 | Network analysis | STRING PPI, data-driven co-expression |
| 10 | Independent validation | Bootstrap AUC, permutation Wilcoxon |

### Key Findings

- **NDUFB4** and **PDCD4** are significantly downregulated in tamoxifen-resistant tumors
- Resistant tumors show coordinated upregulation of the mitochondrial respiratory electron transport chain
- 66.7% of discovery-significant proteins replicate their direction of change in an independent cohort

---

## Repository Structure

```
.
├── PROTEOMICS_ASSIGNMENT_BREAST_CANCER.Rmd   # Main analysis (run this)
├── references.bib                             # BibTeX citations
├── springer-vancouver-brackets.csl            # Citation style (numbered)
├── data/
│   ├── BreastCancer_MSc2026_DiscoveryData_A.xlsx   # Discovery dataset
│   └── BreastCancer_Msc2026_Validation_B.xlsx      # Validation dataset
├── figures/                                   # Generated plots (PDF + PNG)
│   ├── volcano-plot-1.png
│   ├── heatmap-top-proteins-1.png
│   ├── gsea-analysis-1.png
│   └── ... (22 figures total)
├── results/
│   ├── DiscoveryA_limma_results.csv           # Full DE results table
│   ├── DiscoveryA_limma_SVA_sensitivity.csv   # SVA comparison
│   └── DiscoveryA_signature.csv               # Significant proteins
├── .gitignore
├── LICENSE
└── README.md
```

---

## Quick Start

### Prerequisites

- **R** >= 4.3 ([download](https://cran.r-project.org/))
- **RStudio** (recommended) or any R IDE
- **XeLaTeX** for PDF rendering (included with [TinyTeX](https://yihui.org/tinytex/) or MiKTeX)

### Run the Analysis

1. **Clone** the repository:
   ```bash
   git clone https://github.com/Walter-Odur/Differential-Protein-Expression-With-Limma-Proteomics.git
   cd Differential-Protein-Expression-With-Limma-Proteomics
   ```

2. **Open** `PROTEOMICS_ASSIGNMENT_BREAST_CANCER.Rmd` in RStudio

3. **Knit** to PDF (Ctrl+Shift+K) or run:
   ```r
   rmarkdown::render("PROTEOMICS_ASSIGNMENT_BREAST_CANCER.Rmd", output_format = "pdf_document")
   ```

All R packages are automatically installed on first run. The full pipeline takes approximately 5-10 minutes.

---

## Datasets

Both datasets are publicly available from ProteomeXchange/PRIDE:

| Dataset | Accession | Samples | Role |
|---------|-----------|---------|------|
| Discovery (A) | [PXD000484](https://www.ebi.ac.uk/pride/archive/projects/PXD000484) | 56 (24 OR, 32 PD) | Primary analysis |
| Validation (B) | [PXD000485](https://www.ebi.ac.uk/pride/archive/projects/PXD000485) | 56 (41 OR, 15 PD) | Independent replication |

- **OR** = Objective Responders (TTP > 6 months)
- **PD** = Progressive Disease (TTP < 6 months)

---

## Pipeline Diagram

```
Raw Excel (MaxQuant LFQ) 
    │
    ├── Step 1: Import, clean contaminants, build LFQ matrix
    │
    ├── Step 2: QC (outlier detection, PCA batch check)
    │
    ├── Step 3: Filter (70% valid values) → Log2 transform
    │
    ├── Step 4: Impseq imputation (MNAR-aware)
    │
    ├── Step 5: Exploratory PCA + correlation heatmap
    │
    ├── Step 6: limma DE (eBayes, trend=TRUE, robust=TRUE)
    │           └── SVA sensitivity check
    │
    ├── Step 7: Visualization (volcano, heatmap, boxplots)
    │
    ├── Step 8: Enrichment (GO, KEGG, Reactome, GSEA)
    │
    ├── Step 9: Networks (STRING PPI + co-expression)
    │
    └── Step 10: Independent validation (bootstrap AUC, permutation Wilcoxon)
```

---

## R Packages Used

| Category | Packages |
|----------|----------|
| Data handling | readxl, dplyr, tidyr, tibble, stringr |
| Visualization | ggplot2, ggrepel, ggpubr, patchwork, viridis, RColorBrewer, pheatmap, EnhancedVolcano, ComplexHeatmap, circlize |
| Statistics | limma, sva, preprocessCore, matrixStats, rrcovNA, pROC, coin |
| Enrichment | clusterProfiler, org.Hs.eg.db, enrichplot, ReactomePA, STRINGdb |
| Networks | igraph, ggraph, tidygraph |

---

## Citation

If you use this tutorial in your work, please cite:

```
Odur, W. & Kipuyo, H.E. (2025). Differential Protein Expression Analysis: 
Tamoxifen Response in ER+ Breast Cancer. Makerere University, MSc Bioinformatics.
```

### Key References

- Cox, J. & Mann, M. (2014). MaxQuant enables high peptide identification rates. *Nat. Biotechnol.*
- Peng, J. et al. (2024). Systematic benchmarking of proteomics workflows. *Nat. Commun.*
- Ritchie, M.E. et al. (2015). limma powers differential expression analyses. *Nucleic Acids Res.*
- Fiorillo, M. et al. (2021). Mitochondrial bioenergetics in breast cancer. *Cancers*

---

## Authors

- **Walter Odur** (2025/HD07/26017U)
- **Haggai Elisha Kipuyo** (2025/HD07/30926T)

MSc Bioinformatics, Makerere University

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
