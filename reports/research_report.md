# GeneScope: Differential Gene Expression Analysis of Lung Adenocarcinoma

## 1. Executive Summary & Research Question
- **Research Question:** Which specific genes exhibit statistically significant differential expression between human lung adenocarcinoma tissue and non-tumor control lung tissue?
- **Dataset:** NCBI GEO Accession **GSE10072** (Affymetrix Human Genome U133A Array, GPL96).
- **Key Finding:** Identified **859** significantly differentially expressed probes ($q < 0.05$, $|\log_2 \text{FC}| > 1.0$), with **297** upregulated genes and **562** downregulated genes in tumor tissues relative to normal controls.

---

## 2. Methodology & QC
1. **Dataset Ingestion:** 107 total samples (58 Lung Adenocarcinoma, 49 Normal Lung Control).
2. **Quality Control:** 
   - Checked global intensity range (3.67 to 15.25), confirming $\log_2$ transformed values.
   - Boxplot analysis confirmed cross-sample median alignment.
   - Unsupervised 2D PCA demonstrated clear separation between Tumor and Normal groups along PC1 (26.2% variance).
3. **Statistical Testing:**
   - Two-sample Welch's $t$-test calculated per probe.
   - Benjamini-Hochberg False Discovery Rate (FDR) correction applied ($q < 0.05$).
   - Biological significance threshold set to $|\log_2 \text{FC}| > 1.0$ (2-fold change).

---

## 3. Biological Findings & Key Drivers
- **Oncogenic Upregulation:**
  - `SPP1` (Osteopontin): $+4.36\ \log_2 \text{FC}$ ($q = 3.97 \times 10^{-34}$), a prominent biomarker for tumor invasion, cell survival, and metastasis.
- **Differentiated Tissue Loss (Downregulated):**
  - `AGER` (Advanced Glycation End-product Receptor): $-4.42\ \log_2 \text{FC}$ ($q = 1.52 \times 10^{-34}$), reflecting the loss of normal lung alveolar architecture.
  - Endothelial markers (`CDH5`, `PECAM1`, `VWF`): Markedly lower expression in tumor masses compared to healthy vascular tissue.

---

## 4. Deliverables & Reproducibility
- **Figures:**
  - `results/figures/heatmap_top40_degs.png`
- **Data Tables:**
  - `results/tables/differential_expression_results.csv` (Full set of 22,283 analyzed probes)
  - `results/tables/significant_degs_fdr05_fc1.csv` (859 significant DEGs)
- **Environment:** Executed on CachyOS Linux, Python 3.12, using `pandas`, `SciPy`, `statsmodels`, `scikit-learn`, `Matplotlib`, and `Seaborn`.

---

## 5. Limitations & Future Directions
- **Assay Platform:** Microarray hybridization measures intensity within a lower dynamic range than RNA-sequencing read counts.
- **Uncontrolled Covariates:** Smoking history, tumor stage, and patient age should be modeled using multifactor linear models (e.g., `limma` or `statsmodels` OLS) in future extensions.
