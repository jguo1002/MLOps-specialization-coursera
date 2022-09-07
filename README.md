# MLOps-specialization-coursera
Machine Learning Engineering for Production (MLOps) Specialization on Coursera


## Table of Contents 
- [Course 1: Introduction to ML Life Cycle and Deployment](#course-1-introduction-to-ml-life-cycle-and-deployment)
    - [Week 1: Overview of the ML Lifecycle and Deployment](#week-1-overview-of-the-ml-lifecycle-and-deployment)
    - [Week 2: Select and Train a Model](#week-2-select-and-train-a-model)
    - [Week 3: Data Labeling](#week-3-data-labeling)
- []()


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