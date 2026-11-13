# Machine Learning Analysis of Network Traffic for Cyberattack Detection

**Module:** Fundamentals of AI & Data Science (COMP H2706) | **Academic project:** April 2026  
**Focus:** Network data exploration, Random Forest classification/regression and critical evaluation

## Project overview

I analysed a labelled network-traffic dataset containing **benign** and **brute-force** examples. The work had two goals: classify the traffic type and predict numerical **average packet size**. I used exploratory analysis to understand the data before training and evaluating models.

The important result is **not** that I built a successful detection system. The Random Forest classifier classified benign traffic very well but missed almost all brute-force cases. Identifying this failure was the main security lesson of the project.

## Data and methodology

- **Features explored:** Login attempts, failed logins, bytes sent/received, packet rate, connection count, port number, session retries, anomaly score, average packet size and other recorded traffic measurements.
- **Exploration:** Class-distribution charts, histograms, correlation heatmap and comparisons of selected feature values by traffic type.
- **Preparation:** Missing-value handling, encoding categorical values and creating additional derived indicators.
- **Models:** Random Forest **classifier** for `attack_category`; Random Forest **regressor** for `avg_packet_size`.
- **Split and evaluation:** 80/20 training/test split; confusion matrix for classification; actual-vs-predicted and residual charts for regression.

## Findings

The report's classification confusion matrix shows:

| Actual traffic | Predicted benign | Predicted brute-force |
| --- | ---: | ---: |
| Benign | 832 | 0 |
| Brute-force | 367 | 1 |

On this test split the model detected **1 out of 368 brute-force cases** (about **0.3% recall**). This means the apparent performance for benign traffic did **not** translate to effective attack detection. The imbalance between benign and attack examples, along with feature overlap, were discussed as likely contributors.

The Random Forest regressor followed the general average-packet-size trend better, although its residuals showed prediction errors. No unsupported deployment or real-time detection claims are made.

## Lessons and next steps

- In threat detection, an overall accuracy number can hide dangerously low attack recall.
- Inspect the confusion matrix and minority-class outcomes, not just the total score.
- Possible future improvements include investigating class balancing and alternative evaluation/feature strategies. These were **recommendations**, not implementations described in the report.

## My contribution

I explored and prepared the traffic data, trained and evaluated Random Forest classification and regression models, examined the resulting charts and explained what the weak brute-force detection performance meant for a cybersecurity setting.

## Evidence

- [Selected, sanitised pages from the AI/Data Science project report](evidence/sanitised-report-excerpts.pdf)
- [Classifier confusion matrix from the report](evidence/confusion-matrix.png)
- [Regression actual vs predicted chart](evidence/regression-chart.png)

**Evidence note:** The uploaded source material was the assessment report, not Python scripts, a notebook or the dataset. Accordingly, this portfolio provides results and documentation **without claiming to include runnable code**. The source report documents **Random Forest**, not a logistic-regression comparison.
