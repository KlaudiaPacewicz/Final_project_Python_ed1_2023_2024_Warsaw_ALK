# ALK_final_project

## AIM OF THE PROJECT

In the evolving world of personalized medicine, the use of complete and extensive genetic data is playing an increasingly important role. The analysis and understanding of cancer genetics allows for the identification of new mutations and complex genomic features, allowing for more accurate patient stratification in terms of targeted therapies, identification of resistance biomarkers and prediction of further risk.

The project aims to discover genomic features extracted from whole genome sequencing (WGS) data to identify patients likely to respond to PARP inhibitors (PARPi).


## METHODOLOGY

[Clinical metadata and raw data from whole-genome sequencing](https://github.com/KlaudiaPacewicz/ALK_final_project/tree/main/original_input_data) of patients diagnosed with ovarian cancer were downloaded from 3 publicly available repositories collecting genomic and clinical data from oncology patients. A total of 255 samples were collected, for which the original IDs were anonymized.

### 1. Genomic data processing

The raw WGS data were processed using the [cgp-wgs pipeline](https://github.com/cancerit/dockstore-cgpwgs), which enables the detection of all changes present in the cancer genome - from single nucleotide changes to complex genomic rearrangements, such as inversions, deletions, translocations, tandem duplications and copy number variations. Raw data were succesfully processed for 247 samples.

The processed WGS data were used to extract 108 comprehensive genomic features. ###tutaj dodac gdzie jest opis cech

Additionaly, for 247 samples HRD score was calculated using [hrd pipeline](https://github.com/eyzhao/hrdetect-pipeline).

### 2. Genomic features preprocessing

All 108 genomic features were carefully analyzed for variance in all samples. For this purpose, the value of each feature was presented in a [histogram](https://github.com/KlaudiaPacewicz/ALK_final_project/tree/main/data_preprocessing/genetic_data_preprocessing). Features that had zero variance were removed. Features defined by complex genomic changes divided into length bins were pooled to obtain greater variance. Ultimately, 82 features remained for further analyzes.

### 4. Clinical metadata processing

[Clinical metadata preprocessing](https://github.com/KlaudiaPacewicz/ALK_final_project/tree/main/data_preprocessing/clinical_metadata_preprocessing) consisted of:
* selection of patients treated with platinum-based chemotherapy and/or PARP inhibitors
* calculation of the progression-free survival period (counted from the time of initiation of therapy until reported disease progression or recurrence)
* the period during which the disease was stable (counted from the start of therapy to the last response recorded as 'stable disease')

The clinical metadata processed in this way was used for further labeling of samples.

### 5. Clinical features extraction

[Clinical features](https://github.com/KlaudiaPacewicz/ALK_final_project/tree/main/clinical_features) were extracted from the processed clinical metadata and used for correlation with genomic features. The clinical features include: patient's age, type of tumor (primary tumor or metastasis) or family history of cancer.


### 6. Sample labeling

Based on the processed clinical metadata, [4 output files](https://github.com/KlaudiaPacewicz/ALK_final_project/tree/main/labels/basis_for_sample_labeling) were prepared on the basis of which various labels could be generated depending on the interpretation of clinical data:
  * Repository1_samples_with_labels.csv:
      * samples treated with platinum-based chemotherapy or PARPi having one of the following labels: *true_responder, responder_based_on_PFS, responder_based_on_SD, true_nonresponder,              nonresponder_based_on_PFS nonresponder_based_on_SD*
  * Repository1_test_samples_without_label.csv:
      * samples treated with other treatment
  * Repository2_samples_with_labels.csv:
     * pre-treated samples having one of the following labels: *possible_responder, possible_nonresponder*
  * Repository3_samples_with_labels.csv:
    * samples treated with platinum-based chemotherapy or PARPi having one of the following labels: *true_responder, responder_based_on_PFS, true_nonresponder*

Finally, 4 sets of [labels](https://github.com/KlaudiaPacewicz/ALK_final_project/tree/main/labels) were prepared

## RESULTS

Nine different [models](https://github.com/KlaudiaPacewicz/ALK_final_project/tree/main/models) were tested using the logistic regression algorithm. In each model, different methods of labeling samples and genomic features were tested.  When evaluating each model, risk estimation was taken into account, with the most important model measure being recall for positive samples. After evaluating all approaches, model 4 was selected as the final model.

The final logistic regression model was trained with 5-fold cross validation on samples with v1 labels. The average results of the basic metrics on the training model are as follows:

| mean_roc_auc | mean_precision | mean_average_precision | mean_recall | mean f1 | mean balanced_accuracy | mean positive_likelihood_ratio |
|----------|----------|----------|
| 0.63    | 0.7   | 0.72  | 0.76 | 0.72 | 0.61 | 1.41


The final model was saved as ' final_model_for_parpi_response_prediction' in the ['final_model'](https://github.com/KlaudiaPacewicz/ALK_final_project/tree/main/final_model) folder. The final model was tested on [unlabeled samples](https://github.com/KlaudiaPacewicz/ALK_final_project/blob/main/final_model/Model_test_on_blind_samples.ipynb) and compared to HRD status to evaluate the results.


## CONLCUSIONS


