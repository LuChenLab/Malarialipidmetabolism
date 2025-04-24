# Malaria Lipid Metabolism Analysis & MRS R Package

This repository includes:

1. 🔍 **Data analysis scripts** to identify lipid metabolism-related genes in *Plasmodium* species using scRNA-seq and bulk RNA-seq.
2. 📦 **MRS R package**, a PU-learning-based framework for gene classification using only positive samples.

---

## 📊 1. Malaria Lipid Metabolism Analysis

We jointly analyzed scRNA-seq data from *Plasmodium falciparum* and *Plasmodium berghei* IDC stages. A lipid metabolism gene, **CAP**, was identified and shown to regulate phosphatidylcholine and phosphatidylethanolamine biosynthesis via interaction with host CTL1.

### 📁 Dataset Overview

| File | Description |
|------|-------------|
| `01_01_Pb_seurat.Rds`, `01_02_Pf_seurat.Rds` | Seurat objects from [Malaria Cell Atlas](https://www.malariacellatlas.org) |
| `02_Gene_Orth_Data.xlsx` | One-to-one orthologs across *Plasmodium* species |
| `03_LipidGene.xlsx` | Annotated lipid metabolism-related genes |
| `04_RF_GeneInfo.xlsx` | Features for RF model |
| `05_raw_counts.txt` | Bulk RNA-seq raw counts for CAP knockout |

### 📜 Key Scripts

| Script | Description |
|--------|-------------|
| `01_Scmap_Related_Fig1.Rmd` | Cell type/stage assignment using [scmap](https://www.nature.com/articles/nmeth.4644) |
| `02_Expression_LipidGene_Related_FigS1.Rmd` | Gene expression heatmap using [ComplexHeatmap](https://academic.oup.com/bioinformatics/article/32/18/2847/1743594) |
| `03_Mfuzz_Related_Fig1.Rmd` | Temporal clustering with [Mfuzz](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2139991/) |
| `04_Randomforest_Related_Fig1.Rmd` | Lipid gene prediction via Random Forest |
| `05_DESeq2_Related_Fig3.Rmd` | DE analysis of CAP knockout using [DESeq2](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-014-0550-8) |

---

## 🧠 2. MRS: Metabolism-Related Score Model

MRS is a machine learning package built on [`caret`](https://github.com/topepo/caret), designed for binary classification problems where only **positive samples** are available.

It implements a **Spy PU-learning** pipeline to identify reliable negatives, compares 10 classifiers, supports ablation-based feature selection, and provides end-to-end model evaluation.

### ⚙️ Key Features

- Spy PU-learning with tunable parameters
- Model comparison (XGBoost, RF, SVM, etc.)
- Feature selection via ablation (optional)
- Final model tuning + performance visualization
-  PR / ROC curves for training and test sets

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
# PR Curve
Plot_pr_curves(final_model$train_pr_list, final_model$test_pr, title = "Precision-Recall Curves")

# ROC Curve
Plot_roc_curves(final_model$train_roc_list, final_model$test_roc, title = "ROC Curves")
```
