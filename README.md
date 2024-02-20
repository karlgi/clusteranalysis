# Data driven subclassification of ANCA associated vasculitis – model-based clustering of the FAIRVASC cohort
This is the repository containing the code for the statistical analysis in the paper: Data driven subclassification of ANCA associated vasculitis – model-based clustering of the FAIRVASC cohort. 

[FAIRVASC](https://fairvasc.eu/) (Findable, Interoperable, Accessible, Reusable Vasculitis) is a research project of the European Vasculitis Society (EUVAS) and RITA European Reference Network, bringing together leading scientists, clinicians and patient organisations. The FAIRVASC consortium is made up of 10 partners, including several patient registries in AAV. In 2023, the to-date largest cohort in AAV was [presented](https://doi.org/10.1136/ard-2023-224571) by the FAIRVASC consortium. Retrospective observational data from six European registries were quality controlled and harmonised to a common schema.

To further explore the phenotypic spectrum of AAV, we here perform an unbiased data-driven subclassification of AAV using model-based clustering, utilising this large, harmonised cohort of real-world patient data. This is the code for this analysis. 

### Workflow: 
1. To start: registry_prepared.csv are files where registry is the registry name (czech, fvsg, gevas, polvas, rkd, skane). This is the structure of these files:

| Name | id    | age    | creatinine| crp    | gender| constitutional| musculoskeletal| cutaneous| eye    | mucosa | ent    | chest  | cardio | abdominal| kidney | cns    | pns    | anca    | followutime | dateofdiagnosis | dateoffollowup | death | dateofdeath | eskd | dateofeskd | maindiagnosis | registry |
|:---:| :---:  | :---:  | :---:| :---:   | :---:| :---:| :---:| cutaneous|:---:  | :---:|:---:| :---: | :---:| :---:| :---:| :---:| :---:    |:---:   | :---:| :---: | :---: | :---: | :---: | eskd | :---: | :---: | :---:|
| Class| string| numeric| numeric   | numeric| string| numeric       | numeric        | numeric  | numeric| numeric| numeric| numeric| numeric| numeric  | numeric| numeric| numeric| nominal
| numeric | date | data | logical | date | logical | date | string | string |



id	age	creatinine	crp	gender	constitutional	musculoskeletal	cutaneous	eye	mucosa	ent	chest	cardio	abdominal	kidney	cns	pns	anca	followuptime	dateofdiagnosis	dateoffollowup	death	dateofdeath	eskd	dateofeskd	maindiagnosis	registry<img width="1450" alt="image" src="https://github.com/karlgi/clusteranalysis/assets/76054859/f7a666cb-8e61-4398-a911-44dc11e67353">

   
3. Imputation of data: full_matrix_generation.rmd
Here all registry_prepared.csv are imported. Rows containing more than 50% missing values are removed. The rows are shuffled. Variables are selected and data missingness is explored. Data is imputed to generate 10 complete sets. This data is saved in imputed_data.rda. 

4.	Model-based clustering: cluster_generation.rmd
Here the file imputed_data.rda is imported. Model-based clustering is run over the 10 datasets and the results saved in res_X.rda where X is the number of the complete data frame from 1-10.

5.	Exploration and relabeling of clusters: explore_results.rmd
Here res_1.rda to res_10.rda are imported. The optimal clustering solution is found, and clusters (and parameters) relabelled according to Stephens method. Relabelled cluster data is saved as res_X_high.rda, where X is the iteration from 1-10.

6.	Description and outcome analysis: describe_clusters.rmd
Here relabeled clusters are explored. In this file we also import imputed_data.rda to use for the pooled analysis. Clusters are explored with descriptive statistics and prediction of outcome. 
