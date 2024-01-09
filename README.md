# Malaria lipid metabolism

Joint analysis of scRNA-seq from the IDC stages of <I>P. falciparum</I> and <I>P. berghei</I> led to the identification of a gene involved in lipid metabolism, named CAP. Experimental evidence indicates that CAP mediates its biosynthesis of phosphatidylcholine and phosphatidylethanolamine through interaction with the host CTL1.

# Script guidance

The project includes raw count matrices and R scripts to analyse scRNA-seq of <I>P. falciparum</I> and <I>P. berghei</I> parasite cells, along with bulk RNA-seq for CAP Knockout in <I>P. berghei</I>. For lipidomics analysis, we exclusively used [MetaboAnalystR](https://www.metaboanalyst.ca/docs/RTutorial.xhtml).

1) Data   
   pf_IDC_10X, pb_IDC_10X: raw count matrices of scRNA-seq from [MCA](https://www.malariacellatlas.org).  
   Exprotein_gene_list.xlsx: list of genes that encode exported proteins.  
   Gene_MIS_Score.xlsx: mutagenesis index scores [(MISs)](https://www.science.org/doi/10.1126/science.aap7847) of <I>P. falciparum</I> genes.  
   Genes_related_to_lipid_metabolism: Plasmodium conserved genes involved in lipid metabolism.  
   Gene_Orth_Data.xlsx: one-to-one orthologs across ten Plasmodium species.  
   Protein_sequence_of_candidategenes.Rds: Protein sequences of 6 candidate genes.  
   raw_counts.txt:  raw count matrices of bulk RNA-seq.
   
3) Analysis  
   Pf_IDC_seurat.Rds: SeuratObject of <I>P. falciparum</I>.  
   Pb_IDC_seurat.Rds: SeuratObject of <I>P. berghei</I>.  
   Mfuuzz_X_Y.Rds: The result files of Mfuzz analysis, "X" denotes the strain while "Y" signifies the file content.
   
5) Script  
   . 
