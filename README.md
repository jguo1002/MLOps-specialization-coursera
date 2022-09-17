# MLOps-specialization-coursera
Machine Learning Engineering for Production (MLOps) Specialization on Coursera


## Table of Contents 
- [Course 1: Introduction to ML Life Cycle and Deployment](#course-1-introduction-to-ml-life-cycle-and-deployment)
    - [Week 1: Overview of the ML Lifecycle and Deployment](#week-1-overview-of-the-ml-lifecycle-and-deployment)
    - [Week 2: Select and Train a Model](#week-2-select-and-train-a-model)
    - [Week 3: Data Labeling](#week-3-data-labeling)
- [Course 2: Machine Learning Data Lifecycle in Production](#course-2-machine-learning-data-lifecycle-in-production)
    - [Week 1: Collecting, Labeling and Validating Data](#week-1-collecting-labeling-and-validating-data)
    - [Week 2: Feature Engineering, Transformation and Selection](#week-2-feature-engineering-transformation-and-selection)


## Course 1: Introduction to ML Life Cycle and Deployment

### Week 1: Overview of the ML Lifecycle and Deployment

| Depolyment Patterns | Description |
| -- | -- |
| Shadow mode | Have a machine learning algorithm shadow the human inspector and run parallel with the human inspector. The learning algorithms output is not used for any decision.
| Canary | Roll out to a small fraction of traffic. Then either gradually ramp up (if it’s going well) or rollback (if not) 
| Blue green | Assign traffic to a green (new) deployment from a blue (old) deployment

**Degree of automation**

Human only -> Shadow mode -> AI assistance -> Partial automatio -> Full automation 

**Model monitoring**

| Type of Metrics | Metric Examples | 
| -- | -- | 
| Software | Memory, compute, latency, throughput, server load | 
| Input | Avg input lenght, avg input volume, Num missing values, Avg image brightness
| Output | # times retrun "" (null), # times user redoes search, # times user switch to typing, CTR


### Week 2: Select and Train a Model

**How to establish a baseline?**


<details>
<summary>
Click to see the answewr
</summary>

- Human level performance (HLP). Generally it's more effective for establishing the baseline on unstructured data than structured data. 
- Literature search for state-of-the-art/open source
- Older system

</details>
<br />

**What do precision and recall mean?**

<details>
<summary>
Click to see the answewr
</summary>

| Metric | Formula | Layman definition 1 | Layman definition 2| 
| -- | -- | -- | -- | 
| Precision | $\frac{TP}{TP + FP}$ | TP / **Predicted** positive | How believable the model is when it says an instance is a positive?
| Recal | $\frac{TP}{TP + FN}$ | TP / **Real** positive | How often was the model able to find positives?

</details>
<br />

### Week 3: Data Labeling

**What are the differences between structured and unstructured data in terms of labeling and data augmentation?** 

> It is generally easier for humans to label data and to apply data augmentation on unstructured data than structured data.

**What is data provenance and data lineage? Why we need them?**

> - Data provenance: where the data comes from? 
> - Data lineage: sequence of steps
> - Tools: extensive documention, tensorflow transform

[⬆️ Back to Top](#table-of-contents)

## Course 2: Machine Learning Data Lifecycle in Production

### Week 1: Collecting, Labeling and Validating Data 

**What are the examples where ML systems fail the users it serves?**

> - Representation harm: a system amplifies or reflects a negative stereotype about particular groups
> - Opportunity denial: a system makes predictions that have negative real life consequences that could result in lasting impacts. 
> - Disproportionate product failure: outputs are skewed for particular groups of users. 
> - Harm by disadvantage: system infers disadvantageous associations between different demographic characteristics and the user behaviors.

**What is direct labeling? What are its pros and cons?**

> A way of continuously creating new training data to use in the model. It takes the features themselves from the inference requests that the model is getting. E.g., actual clicks and predicted clicks. 
>
> Pros: 
> - continous training data creation
> - labels evolve quickly
> - strong label signals
> 
> Cons:
> - the inherent nature of the problem
> - failure to capture ground truth
> - custom design

```
Data issues
├── Drift
│   ├── Data drift
│   └── Concept drift
├── Skew
│   ├── Schema skew
│   ├── Feature skew
│   └── Distribution skew
```
**What is drift and skew?**

| Concept | Definiton | 
| -- | -- |
| Drift | Changes in data over time, such as data collected once a day |
| Skew | Differences between two static versions, or different sources, e.g., training v.s. serving set | 

**What is data drift and concept drift?**

| Concept | Definiton | 
| -- | -- |
| Data drift | Changes in the statistical properties of the features due to seasonality, trend, or unexpected events | 
| Concept drift | Changes in statistical properties of the labels over time. The mapping found during training is no longer valid |

**What is schema skew and distribution skew?**

| Concept | Definiton | Probably caused by | 
| -- | -- | -- |
| Schema skew | The training and schema as serving data do not conform to the same schema. e.g., integer -> float, string -> category |  | 
| Feature skew | Changes in the feature values between training and serving | A data source that provides some feature values is modified between training and serving time <br/> Different logic for generating features, e.g., transformation only in one of the two code paths, Java v.s. Python| 
| Distribution skew | A divergence of training and serving datasets. The changes in distribution of individual features, e.g., range 1-100 in training changed to 5-600 in serving.  | Faulty sampling method during training <br/> Different data sources for training and serving data <br/> Trend, seasonality, changes in data over time | 

**What is data shift, covariate shift, and concept shift？**

| Type | Changed | Unchanged | 
| -- | -- | -- |
| Data shift | joint probability of x and y  |  | 
| Covariate shift | marginal distribution of x  | conditional distribution of y given x  |
| Concept shift | conditional distribution of y given x | marginal distribution of x

**What measure is typically used to determine the degree of data drift?**

> Chebyshev distance (L-infinity)

[⬆️ Back to Top](#table-of-contents)

### Week 2: Feature Engineering, Transformation and Selection

Transformation 
Training: Full pass requires the entire dataset
Serving: Instance level

**When to do transformation and what are the pros and cons?**
| When | Pros | Cons |
| -- | -- | -- |
| Preprocess trainset | Run once <br> Compute on entire | Transformations reproduced at serving <br> Slow iteration, each time make a change need to do a full pass | 
| Within model | Easy iteration, part of the model <br> Guarantee the transformation | Expensive <br> Long model latency, GPU in training but CPU in serving <br> Batch transform skew |

**What is feature cross?**

> It combines multiple features into a new feature. 

**What are supervised feature selection methods and what are their differences?**

| Method | Sub-method | How-to | Model-related | 
| -- | -- | -- | -- |  
| Filter | Correlation | Select features correlated with label, remove mutual correlated features | No |
|  | Univariate | Selecting the best features based on univariate statistical tests, e.g., Anova F-test | No |
| Wrapper | Forward | Add features one by one | Yes |
|  | Backward  | Start with all features, remove one by one | Yes |
|  | Recursive (RFE) | Fit the model and  rank important features, remove least important ones until the desired feature number | Yes |
| Embedded | L1 / L2 regularization | Introduces a penalty term to the loss function which leads to the least important features being eliminated | Yes |
|  | Feature importance | Assign scores and drop features scored lower than importance | Yes |
|  |  |

Pearson, Kendall Tau Rank, Spearman
F-test, mutual information, Chi square