# MLOps-specialization-coursera
Machine Learning Engineering for Production (MLOps) Specialization on Coursera


## Table of Contents 
- [Course 1: Introduction to ML Life Cycle and Deployment](#course-1-introduction-to-ml-life-cycle-and-deployment)
    - [Week 1: Overview of the ML Lifecycle and Deployment](#week-1-overview-of-the-ml-lifecycle-and-deployment)
    - [Week 2: Select and Train a Model](#week-2-select-and-train-a-model)


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
| Software | 
| Input | 
| Output | 


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



