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
   03_01_pb_cl.Rds, 03_02_pb_df.Rds, 03_03_pb_Mfuzzgene.Rds: SeuratObject of <I>P. falciparum</I>.  
   03_04_pf_cl.Rds, 03_05_pf_df.Rds, 03_06_pf_Mfuzzgene.Rds: SeuratObject of <I>P. berghei</I>.  
   
5) Script  
   01_Scmap_Related_Fig1.Rmd: [Scmap](https://www.cell.com/cell/fulltext/S0092-8674(21)00583-3?_returnURL=https%3A%2F%2Flinkinghub.elsevier.com%2Fretrieve%2Fpii%2FS0092867421005833%3Fshowall%3Dtrue](https://www.nature.com/articles/nmeth.4644)) performed stage clustering of single-cell transcriptomic data.  
   02_Expression_LipidGene_Related_FigS1.Rmd: [ComplexHeatmap](https://academic.oup.com/bioinformatics/article/32/18/2847/1743594?login=false) demonstrated the dynamics of conserved lipid metabolism-related genes.  
   03_Mfuzz_Related_Fig1.Rmd: [Mufzz](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2139991/) analysis found the genes with high expression in the mid- and late- trophozoite stages.  
   04_Randomforest_Related_Fig1.Rmd: RandomForest analysis calculated lipid metabolism-related score for unknown function genes.   
   05_DESeq2_Related_Fig3.Rmd: [DESeq2](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-014-0550-8) analyzed the transcriptome differences after CAP knockout.  
