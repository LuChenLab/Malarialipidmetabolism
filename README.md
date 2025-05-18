# Malaria Lipid Metabolism Analysis & MRS R Package

> **Note**: All analyses and the development of the MRS package were conducted using **R version 4.0.2**, ensuring compatibility and reproducibility within this environment.

This repository includes:

1. 📊 **Malaria Lipid Metabolism Analysis** — A computational pipeline based on single-cell RNA-seq and bulk RNA-seq to identify conserved lipid metabolism-related genes in *Plasmodium* species and prioritize functional candidates for downstream validation.

2. 🤖 **MRS (Metabolism-Related Score) R Package** — A machine learning framework built on Spy-PU learning (Spy-based positive-unlabeled learning), designed for gene classification in datasets containing only positive samples. Includes model comparison, feature selection, and final model training.

---

## 📊 1. Malaria Lipid Metabolism Analysis

We jointly analyzed scRNA-seq data from *Plasmodium falciparum* and *Plasmodium berghei* IDC stages. A lipid metabolism gene, **CAP**, was identified and shown to regulate phosphatidylcholine and phosphatidylethanolamine biosynthesis via interaction with host CTL1.

<div align="center">
  <img src="image/01_scRNA-seq_Data.png" alt="Malaria scRNA-seq data overview" width="650"/>
  <p>
  <strong>Figure 1.</strong>
  UMAP visualization of IDC-stage scRNA-seq for
  <i>P. falciparum</i> and <i>P. berghei</i>, downloaded from the
  <a href="https://www.malariacellatlas.org" target="_blank">Malaria Cell Atlas</a>.
</p>
</div>

### 📁 Dataset Overview

This folder contains the core input data used in this project, including both gene expression matrices and corresponding phenotype annotations.

| File / Folder       | Description |
|---------------------|-------------|
| `01_01_Pb_10X/`     | Single-cell RNA-seq dataset of *Plasmodium berghei*, including the raw gene expression matrix and cell-level phenotype annotations. Data sourced from the [Malaria Cell Atlas](https://www.malariacellatlas.org). |
| `01_01_Pf_10X/`     | Single-cell RNA-seq dataset of *Plasmodium falciparum*, including the raw gene expression matrix and cell-level phenotype annotations. Data sourced from the [Malaria Cell Atlas](https://www.malariacellatlas.org). |
| `04_raw_counts.txt` | Bulk RNA-seq raw count matrix from the CAP knockout experiment (no phenotype file provided). |


## 📜 Key Scripts

The analysis scripts are organized by module prefix:

- `01_` scripts: Single-cell preprocessing, Seurat object construction, scmap-based annotation, and transcriptomic feature analysis.
- `02_` scripts: Gene temporal expression analysis using [Mfuzz](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2139991/), aimed at identifying conserved trophozoite-stage upregulated genes.
- `03_` scripts: Target gene prioritization using the MRS package.
- `04_` scripts: Differential expression (DE) analysis of CAP knockout bulk RNA-seq data using [DESeq2](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-014-0550-8).

| Script | Description |
|--------|-------------|
| `01_01_Making_SeuratObject_Pb_10X.Rmd` | Constructs Seurat object from *P. berghei* 10X data. |
| `01_02_Making_SeuratObject_Pf_10X.Rmd` | Constructs Seurat object from *P. falciparum* 10X data. |
| `01_03_Scmap.Rmd` | Performs cell type and stage assignment using [scmap](https://www.nature.com/articles/nmeth.4644). |
| `01_04_scRNAseq_conclusion.Rmd` | Summary of single-cell RNA-seq results and temporal feature characteristics. |
| `02_01_Mfuzz_Pb.Rmd` | Temporal expression clustering for *P. berghei* using Mfuzz. |
| `02_02_Mfuzz_Pf.Rmd` | Temporal expression clustering for *P. falciparum* using Mfuzz. |
| `02_03_Mfuzz_Conclusion.Rmd` | Summary and comparison of dynamic gene expression patterns. |
| `03_01_LipidGene_expression.Rmd` | Expression analysis of lipid metabolism-related genes. |
| `03_02_ML_for_candidate_gene.Rmd` | Machine learning-based gene scoring and selection using the MRS package. |
| `04_DESeq2.Rmd` | Differential expression analysis for CAP knockout using DESeq2. |


## 📊 Analysis Outputs

This folder contains `.Rds` files with processed results from each major analysis step. Files with `pb` and `pf` denote *P. berghei* and *P. falciparum*, respectively.

| File(s) | Description |
|---------|-------------|
| `01_04_DE_pb.Rds`, `01_04_DE_pf.Rds` | Stage-specific marker genes identified from single-cell data for each species. |
| `01_04_dds_res.Rds` | DESeq2 pseudobulk result object combining both species. |
| `02_01_pb_mfuzz_cl.Rds`, `02_02_pf_mfuzz_cl.Rds` | Mfuzz clustering results (cluster labels). |
| `02_01_pb_mfuzz_df.Rds`, `02_02_pf_mfuzz_df.Rds` | Preprocessed expression matrices used in Mfuzz analysis. |
| `02_01_pb_mfuzz_gene.Rds`, `02_01_pf_mfuzz_gene.Rds` | Final selected conserved stage-enriched genes. |
| `02_01_pb_mfuzz_plotdata.Rds`, `02_01_pf_mfuzz_plotdata.Rds` | Processed data for Mfuzz cluster visualization. |
| `03_02_PosNegData.Rds` | Dataset for the MRS-based gene prioritization model. |

---

## 🤖 2. MRS: Metabolism-Related Score Model

MRS is a machine learning package built on [`caret`](https://github.com/topepo/caret), designed for binary classification problems where only **positive samples** are available.

It implements a **Spy-PU learning** pipeline to identify reliable negatives, compares 10 classifiers, supports ablation-based feature selection, and provides end-to-end model evaluation.

<div align="center">
  <img src="image/02_MRS.png" alt="MRS R package workflow" width="1600"/>
  <p><strong>Figure 2.</strong> Workflow of the MRS package for Spy-PU learning-based gene classification.</p>
</div>


### ⚙️ Key Features

- Spy-PU learning with tunable parameters
- Model comparison (XGBoost, RF, SVM, etc.)
- Feature selection via ablation (optional)
- Final model tuning + performance visualization

## 💻 Environment & Dependencies
The MRS package was developed under R version 4.0.2, and depends on core packages including caret, pROC, PRROC, and doParallel, among others. Please refer to the package DESCRIPTION file for a complete list and version requirements.

## 🚀 Getting Started

```r
# Install from source
devtools::install_local("MRS_1.0.0.tar.gz")

# Step 1: Prepare data
prep <- Prepare_classification_data(my_data)

# Step 2 (optional): PU-learning
pu_data <- Identify_reliable_negatives(prep$trainData, spy_ratio = 0.3, threshold_quantile = 0.05)

# Step 3: Train and compare models
models <- Train_multiple_models(prepared_data = prep)

# Step 4: Evaluate training performance
train_eval <- Evaluate_train_performance(models, prepared_data = prep)

# Step 5: Evaluate test performance
test_eval <- Evaluate_test_performance(models, prepared_data = prep)

# Step 6 (optional): Feature selection
fs_result <- Feature_selection_ablation(prepared_data = prep, model_name = "XGBoost")

# Step 7: Final tuning
final_model <- Tune_model_eval("XGBoost", prepared_data = fs_result)

# Step 8: Plotting
# PR Curve
Plot_pr_curves(final_model$train_pr_list, final_model$test_pr, title = "Precision-Recall Curves")

# ROC Curve
Plot_roc_curves(final_model$train_roc_list, final_model$test_roc, title = "ROC Curves")
```

---

## 📚 References

1. **Howick VM**, Russell AJC, Andrews T, Heaton H, Reid AJ, Natarajan K, Butungi H, Metcalf T, Verzier LH, Rayner JC, Berriman M, Herren JK, Billker O, Hemberg M, Talman AM, Lawniczak MKN. (2019). *The Malaria Cell Atlas: Single parasite transcriptomes across the complete Plasmodium life cycle*. **Science**, 365(6455):eaaw2619. https://doi.org/10.1126/science.aaw2619

2. **Kuhn M.** (2008). *Building Predictive Models in R Using the caret Package*. **Journal of Statistical Software**, 28(5), 1–26. https://doi.org/10.18637/jss.v028.i05

3. **Liu B.**, **Dai Y.**, **Li X.**, **Lee W.S.**, and **Yu P.S.** (2003). *Building text classifiers using positive and unlabeled examples*. In *Proceedings of the Third IEEE International Conference on Data Mining (ICDM)*, pp. 179–186. https://doi.org/10.1109/ICDM.2003.1250918


## 🔗 Cite This Repository

If you use the **Malaria Lipid Metabolism Analysis** pipeline or the **MRS** R package in your work, please cite this repository:

> This repository accompanies a manuscript currently under peer review. Citation details will be updated upon publication.

