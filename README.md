# Malaria lipid metabolism

Joint analysis of scRNA-seq from the IDC stages of <I>P. falciparum</I> and <I>P. berghei</I> led to the identification of a gene involved in lipid metabolism, named CAP. Experimental evidence indicates that CAP mediates its biosynthesis of phosphatidylcholine and phosphatidylethanolamine through interaction with the host CTL1.

# Script guidance

The project includes raw count matrices and R scripts to analyze scRNA-seq of <I>P. falciparum</I> and <I>P. berghei</I> parasite cells, along with bulk RNA-seq for CAP Knockout in <I>P. berghei</I>. For lipidomics analysis, we exclusively used [MetaboAnalystR](https://www.metaboanalyst.ca/docs/RTutorial.xhtml).

1) Data   
   01_01_Pb_seurat.Rds, 01_02_Pf_seurat.Rds: SeuratObject of <I>P. falciparum</I> and <I>P. berghei</I>. Raw count matrices of scRNA-seq from [MCA](https://www.malariacellatlas.org).  
   02_Gene_Orth_Data.xlsx: One-to-one orthologs across ten Plasmodium species.
   03_LipidGene.xlsx: Gene involved in lipid metabolism of <I>P. falciparum</I>.  
   04_RF_GeneInfo： Gene information for random forest.  
   05_raw_counts.txt:  raw count matrices of bulk RNA-seq.
   
3) Analysis  
   Pf_IDC_seurat.Rds: SeuratObject of <I>P. falciparum</I>.  
   Pb_IDC_seurat.Rds: SeuratObject of <I>P. berghei</I>.  
   Mfuuzz_X_Y.Rds: In the result files of Mfuzz analysis, "X" denotes the strain while "Y" signifies the file content.
   
5) Script  
   01_Fig1_Pf_Pb_SeuratObject.Rmd: [Seurat](https://www.cell.com/cell/fulltext/S0092-8674(21)00583-3?_returnURL=https%3A%2F%2Flinkinghub.elsevier.com%2Fretrieve%2Fpii%2FS0092867421005833%3Fshowall%3Dtrue) performed dimensionality reduction and stage clustering of single-cell transcriptomic data.  
   02_Fig1_Dynamic_expression_of_Lipid_gene.Rmd: [ComplexHeatmap](https://academic.oup.com/bioinformatics/article/32/18/2847/1743594?login=false) demonstrated the dynamics of conserved lipid metabolism-related genes.  
   03_Fig1_Pf_Pb_Mfuzz.Rmd: [Mufzz](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2139991/) analysis found the genes with high expression in the mid- and late- trophozoite stages.  
   04_Fig1_RF.Rmd: RandomForest analysis calculated lipid metabolism-related score for unknown function genes.   
   05_Fig3_DESeq2_CAPKO.Rmd: [DESeq2](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-014-0550-8) analyzed the transcriptome differences after CAP knockout.  
