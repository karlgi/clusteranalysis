# Workflow: 
To start: registry_prepared.csv are files where registry is the registry name (czech, fvsg, gevas, polvas, rkd, skane). This is the structure of these files:
   
|      **Name**              | id       | age     | creatinine | crp     | gender  | constitutional | musculoskeletal | cutaneous | eye     | mucosa   | ent     | chest   | cardio  | abdominal | kidney | cns     | pns     | anca    | followuptime | dateofdiagnosis | dateoffollowup | death | dateofdeath | eskd | dateofeskd | maindiagnosis | registry |
|:-------------|:--------:|:-------:|:----------:|:-------:|:-------:|:--------------:|:---------------:|:---------:|:-------:|:--------:|:-------:|:-------:|:-------:|:---------:|:------:|:-------:|:-------:|:-------:|:------------:|:---------------:|:--------------:|:-----:|:-----------:|:----:|:----------:|:-------------:|:--------:|
| **Class**    | string   | numeric   | numeric   | numeric| string   | numeric        | numeric            | numeric      | numeric     | numeric          |numeric         | numeric        |numeric        |numeric           |numeric      | numeric         |numeric         | string   | numeric         | date    | date   | logical    | date            | logical     | date      | string   | string    |
| **Information** | ...  | years   | mikromol/l     | mg/L  |  0 - No, 1-Yes  |  0 - No, 1-Yes         |  0 - No, 1-Yes           |  0 - No, 1-Yes     |  0 - No, 1-Yes   |  0 - No, 1-Yes    | 0 - No, 1-Yes  |  0 - No, 1-Yes   | 0 - No, 1-Yes  | 0 - No, 1-Yes     |  0 - No, 1-Yes | 0 - No, 1-Yes   | 0 - No, 1-Yes  | PR3 positive, MPO positive, ANCA negative | in days      |yyyy-mm-dd         | yyyy-mm-dd        | TRUE, FALSE| yyyy-mm-dd      | TRUE, FALSE| yyyy-mm-dd   | GPA, MPA        | Czech, FVSG, GEVAS, POLVAS, RKD, Skåne   |

1. Imputation of data: full_matrix_generation.rmd
Here all registry_prepared.csv are imported. Rows containing more than 50% missing values are removed. The rows are shuffled. Variables are selected and data missingness is explored. Data is imputed to generate 10 complete sets. This data is saved in imputed_data.rda. 

2.	Model-based clustering: cluster_generation.rmd
Here the file imputed_data.rda is imported. Model-based clustering is run over the 10 datasets and the results saved in res_X.rda where X is the number of the complete data frame from 1-10.

3.	Exploration and relabeling of clusters: explore_results.rmd
Here res_1.rda to res_10.rda are imported. The optimal clustering solution is found, and clusters (and parameters) relabelled according to Stephens method. Relabelled cluster data is saved as res_X_high.rda, where X is the iteration from 1-10.

4.	Description and outcome analysis: describe_clusters.rmd
Here relabeled clusters are explored. In this file we also import imputed_data.rda to use for the pooled analysis. Clusters are explored with descriptive statistics and prediction of outcome. 
