# Expert Chase Analysis

We are currently living the advent of the creator economy and the remote work, which was accelerated by the COVID-19 pandemic. I believe that that in the next decade (1) more companies will start looking for experts for project-based jobs and (2) more employed professionals will start consulting and freelancing as a side activity. Also, probably, the rigid 40-hour work week will disappear.

Companies like [Techspert](https://techspert.com) have embraced that change we are living and match companies and professionals. Yet finding proper experts that are willing to offer consultancy is still a challenge. This repository contains a related dataset and deals with one aspect around that challenge, summarized as follows:

> For each client project, suitable experts are searched, to whom an outreach email is sent. The order that the experts appeared in the search is recorded and whether each expert has responded (or not) to each outreach email.
>
> [The goal] is to **analyze and prepare this data and propose approaches or models that could be investigated to re-rank the profiles so that the top experts have the highest probability of responding positively.**

## Table of Contents

- [Expert Chase Analysis](#expert-chase-analysis)
  - [Table of Contents](#table-of-contents)
  - [Dataset](#dataset)
  - [How to Use This Project](#how-to-use-this-project)
    - [Installing Dependencies for Custom Environments](#installing-dependencies-for-custom-environments)
  - [Implemented Analysis and Modeling](#implemented-analysis-and-modeling)
    - [Reduced Dataset](#reduced-dataset)
    - [Summary of Assumptions](#summary-of-assumptions)
    - [Summary of Findings and Results](#summary-of-findings-and-results)
      - [Hypothesis Tests](#hypothesis-tests)
      - [Models](#models)
  - [Next Steps and Possible Improvements](#next-steps-and-possible-improvements)
    - [Notes on Further Potential Models](#notes-on-further-potential-models)
  - [Authorship](#authorship)

## Dataset

The dataset [`data/data_Nov_2022.csv`](data/data_Nov_2022.csv) contains 371,804 entries of search results, each with the following seven columns/values:

> 1. `person-id`: a unique ID of a single person
> 2. `timestamp`: when the search was performed
> 3. `search-id`: a unique ID of a single search for a particular project
> 4. `search-ranking`: the rank of the person in the search result
> 5. `countries`: the domicile country-codes of the person
> 6. `email-domains`: the email domains of the person
> 7. `outreach-success`: "1" means that the outreach is successful, otherwise "0"

A straightforward approach would consist in treating `outreach-success` as the dependent variable and the rest as the independent variables. However, the goal is to improve the values of `search-ranking` based on the features of entries that have `outreach-success = 1`.

## How to Use This Project

The directory of the project consists of the following files:

```
.
├── LearningToRank_Challenge.docx             # Instructions
├── README.md                                 # This file (Markdown)
├── README.pdf                                # This file (PDF)
├── assets                                    # Results plots        
│   ├── feature_comparison_test.png
│   └── ...
├── conda.yaml                                # Environment dependencies
├── data                                      # Dataset (different versions)
│   ├── data_Nov_2022.csv                     # Original
│   ├── data_Nov_2022_preprocessed.csv        # Pre-processed
│   └── data_Nov_2022_reduced_experts.csv     # Pre-processed and reduced
├── expert_analysis.ipynb                     # Main notebook
├── requirements.txt                          # Additional dependencies (empty)
├── rf1.pickle                                # Model 1 serialized
├── rf2.pickle                                # Model 2 serialized
└── rf3.pickle                                # Model 3 serialized
```

At the present development stage, the complete implementation is in the Jupyter notebook [`expert_analysis.ipynb`](expert_analysis.ipynb). You can run the notebook in a custom environment, e.g., locally or in a container. For instance, to run it locally, you can create a [conda](https://docs.conda.io/en/latest/) environment and install the [dependencies](#installing-dependencies-for-custom-environments) as explained below. Then, you need to open the notebook, i.e.: 
 
```bash
jupyter lab . &
```

<!--
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://github.com/mxagar/expert_chase/blob/main/expert_analysis.ipynb)
:warning: The dataset is not available via Google Colab due to confidentiality reasons. Thus, if you want to open the notebook on Google Colab you need upload the dataset on your own.
-->

### Installing Dependencies for Custom Environments

If you'd like to control where the notebook runs, you need to create a custom environment and install the required dependencies. A quick recipe which sets everything up with [conda](https://docs.conda.io/en/latest/) is the following:

```bash
# Create environment with YAML, incl. pip packages
# Note 1: no versions are specified, because
# the project solution doesn't require any at this stage.
# The package manager resolves any version inconsistencies.
# Note 2: the selected packages are basic for many Data Science
# problems, the YAML file could be further pruned for the task.
conda env create -f conda.yaml
conda activate expert-env

# Optional: Install any pip packages you add later on
# Currently, requirements.txt is empty, because I moved
# all packages to conda.yaml 
pip install requirements.txt
```

List of most important dependencies:

- Pandas
- Scikit-Learn
- Scipy
- Matplotlib
- Seaborn

## Implemented Analysis and Modeling
<!-- A description of interesting parts of your solution and potential improvements or further work -->

The main notebook is structured in 4 parts that were implemented chronologically, following the typical data science project workflow. Each part/section is composed of several subsections, which contain, among others, the findings discovered at each stage. In the following, a brief content description of each part is provided:

1. **Dataset: Load and First Exposure** &mdash; As the title specifies, here, the first contact with the dataset is carried out. The following objectives are met:
   - Understand the features and their relationship.
   - Determine the needs for cleaning and encoding (e.g., processing for time, countries and emails).
   - Compute basic descriptive statistics (e.g., outreach success rate).

2. **Data Preprocessing, Cleaning and Basic Feature Engineering** &mdash; This section is the mo

3. **More Exploratory Data Analysis and Hypothesis Testing**: Once we have the pre-processed and reduced dataset, we can explore it visually and with statistical tests on it. In this section, first, the reduced dataset is split in two groups: entries of experts with positive (successful) outreach and entries with negative outreach. Then, plots are generated for these two groups: (i) ranking distributions, (ii) box pots (numerical variables), (iii) bar charts (binary variables). Finally, hypothesis tests are performed on the two groups for each feature. Hypothesis testing helps to identify whether two samples belong to the same population by comparing their means (e.g., T Test) or proportions (Z Test). A significance level is chosen, alpha, and if the probability of the computed statistic yields a smaller *p-value*, both samples are considered to be different. In the context 

4. **Modeling: First Approach** &mdash; Even though in the original challenge it is not required, I have built some simple models out of genuine curiosity:
   - Model 1: A random forest classifier which predicts the outreach success given all the features available (including the ranking values).
   - Model 2: A random forest classifier which predicts the outreach success given all the features available except the ranking values.
   - Model 3: A random forest regressor which tries to predict the best ranking given the rest features, except the outreach success.

### Reduced Dataset

The pre-processed and reduced dataset...

### Summary of Assumptions
<!-- A list of assumption you made and justification of your design decisions -->

- The requirements for the hypothesis tests are not checked (i.e., it is assumed they are met).

### Summary of Findings and Results
<!-- A summary of any findings when preparing the data -->

This section refers to the outcomes obtained in the parts 3 and 4 of the notebook.

#### Hypothesis Tests

As far as the hypothesis tests are concerned, we have the following results, supported by the appended figures:

- The following experts are associated with positive outreach, thus, their ranking should be minimized (smaller ranking is better):

  - `num_searches`: Number of appearances of the expert in the original dataset.
  - `extension_academia`: Whether the expert has an email with an academia extension.
  - Countries where the expert lives: US, NL.
  - `num_emails`: Number of emails of the expert.

- The following features are associated with negative outreach, thus, their ranking should be maximized:

  - `extension_country`: Whether the expert has an email with company extension.
  - Countries where the expert lives: ES, GB, FR, DE, CA, IT, SE.

In the following, two figures are shown:

- The ranking distributions of the groups with positive and negative outreach values.
- The T and Z statistics for each feature considering the sample populations of the groups with positive and negative outreach values. The `alpha = 0.05` or `T/Z approx. 2` threshold is drawn; feature bars that cross it denote significantly different groups. Additionally, the sign of the statistic is color-coded: red is negative (larger mean/proportion for positive outreach), blue positive (larger mean/proportion for negative outreach).

<p align="center">
  <img src="./assets/search_ranking_distribution.png" alt="Search ranking distribution." width=800px>
</p>

<p align="center">
  <img src="./assets/feature_comparison_test.png" alt="T/Z Test statistics." width=400px>
</p>

#### Models

Among models 1 & 2, the latter is the most interesting one, because it predicts outreach success without considering the ranking values. Since the goals is to improve the ranking system, it is sensible to build a model which predicts the outreach independently of the ranking; then, we obtain its most important features and adjust the ranking later on. A model which is built with the ranking values is of less use (model 1).

Unfortunately, the ROC AUC of model 2 is quite low: 0.69. However, the Gini coefficients of the features are in line with the results from the hypothesis tests, being the most predictive features:

- `num_searches`: Number of appearances of the expert in the original dataset.
- `num_emails`: Number of emails of the expert.
- `extension_academia`: Whether the expert has an email with an academia extension.
- `countries_US`: Whether the expert lives in the US.
- `extension_company`: Whether the expert has an email with company extension.

In its current state, model 3 is a poor predictor, with an R2 = 0.15. Thus, the model fails to predict the ranking values from the rest of the features.

In the following figures the ROC AUC of model 2 and its feature importances are shown.

<p align="center">
  <img src="./assets/model2_roc_curve_test.png" alt="ROC Curve." width=400px>
</p>

<p align="center">
  <img src="./assets/model2_feature_importances.png" alt="Feature importances." width=450px>
</p>


## Next Steps and Possible Improvements

- [ ] A
- [ ] Get domain-related information that could be helpful; for instance:
  - [ ] How is ranking determined?
  - [ ] Get more information about expert candidates, e.g., years of experience, number of companies they've worked in, whether they've done consulting or not, etc.
  - [ ] Which is the exact definition of a successful outreach? For instance, a rejection email is a success?

### Notes on Further Potential Models
<!-- Brief notes on potential models that could be trained on this data -->



<!--
## References, Interesting Links

- Link
- Link
-->

## Authorship

Mikel Sagardia, 2022.  
No guarantees.

<!--
If you find this repository useful, you're free to use it, but please link back to the original source.
-->