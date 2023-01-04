# Expert Chase Analysis

We are currently living the advent of the creator economy and the remote work, which was accelerated by the COVID-19 pandemic. I believe that that in the next decade (1) more companies will start looking for experts for project-based jobs and (2) more employed professionals will start consulting and freelancing as a side activity. Also, probably, the rigid 40-hour work week will disappear.

Companies like [Techspert](https://techspert.com) have embraced that change we are living and match companies and professionals. Yet finding proper experts that are willing to offer consultancy is still a challenge. This repository contains a related dataset and deals with one aspect around that challenge, summarized as follows:

> For each client project, suitable experts are searched, to whom an outreach email is sent. The order that the experts appeared in the search is recorded and whether each expert has responded (or not) to each outreach email.

> [The goal] is to **analyse and prepare this data and propose approaches or models that could be investigated to re-rank the profiles so that the top experts have the highest probability of responding positively.**

## Table of Contents

- [Expert Chase Analysis](#expert-chase-analysis)
  - [Table of Contents](#table-of-contents)
  - [Dataset](#dataset)
  - [How to Use This Project](#how-to-use-this-project)
    - [Installing Dependencies for Custom Environments](#installing-dependencies-for-custom-environments)
  - [Notes on the Implemented Analysis and Modeling](#notes-on-the-implemented-analysis-and-modeling)
    - [Assumptions](#assumptions)
    - [Summary of Implementations](#summary-of-implementations)
    - [Notes on Potential Models](#notes-on-potential-models)
  - [Results, Insights](#results-insights)
    - [Basic Findings](#basic-findings)
    - [Relevant Insights](#relevant-insights)
  - [Next Steps and Possible Improvements](#next-steps-and-possible-improvements)
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
├── LearningToRank_Challenge.docx   # Instructions
├── README.md                       # This file
├── conda.yaml                      # Environment dependencies
├── data                            # Dataset
│   └── data_Nov_2022.csv           # (not committed)
├── expert_analysis.ipynb           # Main notebook
└── requirements.txt                # Additional dependencies (empty)
```

At the present development stage, the complete implementation is in the Jupyter notebook [`expert_analysis.ipynb`](expert_analysis.ipynb). You can run the notebook in the following ways:

1. In a custom environment, e.g., locally or on a container. To that end, you can create a [conda](https://docs.conda.io/en/latest/) environment and install the [dependencies](#installing-dependencies-for-custom-environments) as explained below. Then, you need to open the notebook, i.e.: 
 
    ```bash
    jupyter lab . &
    ```

2. In Google Colab. For that, simply click on the following link:

    [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://github.com/mxagar/expert_chase/blob/main/expert_analysis.ipynb)

:warning: The dataset is not available via Google Colab due to confidentiality reasons. Thus, if you want to open the notebook on Google Colab you need upload the dataset on your own.

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

# SpaCy model
python -m spacy download en_core_web_sm

# Optional: Install any pip packages you add later on
pip install requirements.txt

# Optional: Track any changes and versions you have
conda env export > conda_.yaml
pip freeze > requirements_.txt
```

List of most important dependencies:

- Scikit-Learn
- Pandas
- Matplotlib
- Seaborn

## Notes on the Implemented Analysis and Modeling

### Assumptions

### Summary of Implementations

### Notes on Potential Models

## Results, Insights

### Basic Findings

### Relevant Insights


## Next Steps and Possible Improvements

- [ ] A
- [ ] B

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