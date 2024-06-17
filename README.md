# ALK_final_project

### Project goal

In the evolving world of personalized medicine, the use of complete and extensive genetic data is playing an increasingly important role. The analysis and understanding of cancer genetics allows for the identification of new mutations and complex genomic features, allowing for more accurate patient stratification in terms of targeted therapies, identification of resistance biomarkers and prediction of further risk.

The project aims to discover genomic features extracted from whole genome sequencing (WGS) data to identify patients likely to respond to PARP inhibitors (PARPi).


### Biological explanation:


### Methodology

Clinical metadata and raw data from whole-genome sequencing of patients diagnosed with ovarian cancer were downloaded from 3 publicly available repositories collecting genomic and clinical data from oncology patients. A total of 255 samples were collected, for which the original IDs were anonymized.

#### Genomic data processing:

The raw WGS data were processed using the (cgp-wgs pipeline)[https://github.com/cancerit/dockstore-cgpwgs], which enables the detection of all changes present in the cancer genome - from single nucleotide changes to complex genomic rearrangements, such as inversions, deletions, translocations, tandem duplications and copy number variations.

The processed WGS data were used to extract 108 comprehensive genomic features. ###tutaj dodac gdzie jest opis cech

#### Clinical metadata processing:


#### Genomic features preprocessing:

All 108 genomic features were carefully analyzed for variance in all samples. For this purpose, the value of each feature was presented in a (histogram)[https://github.com/KlaudiaPacewicz/ALK_final_project/tree/main/data_preprocessing/genetic_data_preprocessing]. Features that had zero variance were removed. Features defined by complex genomic changes divided into length bins were pooled to obtain greater variance. Ultimately, 82 features remained for further analyzes.

#### Clinical features preprocessing:

### Results



## Final outcome and conclusions


