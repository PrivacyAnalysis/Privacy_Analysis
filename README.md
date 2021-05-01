# Privacy and Bias analysis of MIMIC-III dataset

## AC221 Critical Thinking in Data Science, Spring 2021

### Group Number 36

* Yujie Cai
* Jiahui Tang
* Xin Zeng

## Overview

In this project, we are incentivized to scrutinize those medical datasets first, to examine the need and effectiveness of de-identification, and further what kind of biases will be harmful if ignored when using the datasets. 

## Software Organization

* Directory Structure

```
    Privacy_Analysis/

      ​	Part I_data_processing.ipynb

      ​	Part II_ K-anonmity & I-Diversity.ipynb

      ​	Part III_ Modeling.ipynb

```


## Conclusion 

MIMIC-III is a rich dataset to work with. Through the exploration of privacy issues and bias embedded in this dataset, we can now summarize the answer of our four central questions:

1) what are the consequences and evaluation of already-implemented de-identification procedures? 

* The existing methods of de-identification of date shifts and text removal are effective. However, we pose concerns of mis-representation of age variables and difficulties in conducting longitudinal studies. 

2) What are the consequences and evaluation of other de-identification procedures that we can apply on the dataset? 

* We managed to apply row suppression, adding synthetic records, column suppression (blurring), and generalization to raise the k-anonymity measurement of the dataset and achieve a higher privacy level. However, we discover the trade off of accuracy, information, and privacy. Moreover, we argue that l-diversity is a better method than k-anonymity to de-identify the dataset. 

3) What kind of bias should we take into account? 

* We shall consider historical and representation bias in MIMIC data generation. Specifically, attributes like ethnicity and insurance type are worth noticing because bias can be propagated into predicting mortality. When building models, we use FNR, FNP to assess the bias in modeling, and we are aware of evaluation bias if we use the same type of metrics. We care more about group fairness and accuracy of the algorithm. We discover that the most complex LightGBM model provides highest accuracy and the baseline logistic model has resulted in unbalanced FNR and FNP across ethnic groups and insurance types, but balanced rate across gender.

4) How can we mitigate them and what are the consequences of the mitigation?

* We use two in-processing methods to try to mitigate the bias in modeling. First is to try on different algorithms (models) and we use LightGBM model to significantly reduce the FNR and FNP across gender, ethnicity, and insurance type. However, the drawback is that sometimes we overtune the balance of certain groups in ethnicity and insurance type. Another method we implement is to change the threshold of classification in logistic regression, specifically for reducing the imbalance of black and white group. We find that the threshold to be either too low or too high than the conventional 0.5, making this method less pragmatic. 
