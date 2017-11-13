# DSCancerGenomics

---

Data Source: 
Genomic/Methylation data from the National Cancer Institute's GDC Data Repository. 

Link:
https://portal.gdc.cancer.gov/repository?filters=~%28op~%27and~content~%28~%28op~%27in~content~%28field~%27files.data_category~value~%28~%27DNA%2A20Methylation%29%29%29%29%29

---
Cleaning and Merging Processes:
1. Invoked package 'dplyr' and 'tidyr' for subsequent table mechanics.
2. After downloading the zip files, data tables were read into RStudio by calling read.table().
3. Adjusted column names with colnames() to correct the read.table() translation error.
4. Selected columns 1 through 11 to remove empty cells.
5. Added column 'Cancer_Type', and manually specified the kind of cancer associated with the observations using mutate().
6. Merged the four resultant data tables together into master dataframe by calling rbind().
7. Removed columns using select(): Transcript_ID, Beta_value, Gene_Symbol, REF, CGI_Coordinate; since they would not contribute to our analytical questions.
8. Removed rows using filter() that failed to have data in columns Position_to_TSS, and Feature_Type, both variables which would be pertinent to our analysis.
9. Separated multiple observations within rows: Gene_Type and Position_to_TSS, by ';' separator using strsplit() and unnest().
---

Column Names Key:

"Chromosome" = chr + human chromosome number;

"Start" = base pair position of feature beginning;

"End" = base pair position of feature end;

"Gene_Type" = type of gene (ie. Protein-coding, noncoding RNA, etc.);

"Position_to_TSS" = base pair distance to translation start site (negative sign indicates feature is 5' (upstream) of translation start site, no sign indicates feature is 3' (downstream) of site);

"Feature_Type" = position of feature observed, (N_Shore = upstream of CpG island, S_Shore = downstream of island, or Island = within CpG island).

