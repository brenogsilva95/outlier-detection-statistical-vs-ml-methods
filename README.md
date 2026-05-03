# outlier-detection-statistical-vs-ml-methods
Comparison of statistical and machine learning approaches for outlier detection with animated visualization of multivariate data.

Post: https://www.linkedin.com/posts/brenogdsilva_datascience-machinelearning-nlp-activity-7455265908752711680-fRY6?utm_source=share&utm_medium=member_desktop&rcm=ACoAADzYEn0BidO853LZcLlVhNbNq-HOPuFNURk

# Outlier Detection: Statistical vs Machine Learning Perspectives

## Introduction

Outlier detection is a fundamental problem in statistics and data science, with applications ranging from fraud detection and quality control to anomaly detection in high-dimensional data.

Traditionally, statistical methods such as the Interquartile Range (IQR) have been used to identify extreme values. However, these approaches are often limited to univariate analysis and may fail in complex, multivariate scenarios.

Modern machine learning techniques, such as Local Outlier Factor (LOF) (Breunig et al., 2000) and Isolation Forest (Liu et al., 2008), provide more flexible frameworks by incorporating local density and isolation mechanisms.

This project presents a comparative and visual analysis of different outlier detection methods, highlighting how distinct modeling assumptions lead to different interpretations of what constitutes an anomaly.

## Problem Formulation

Given a dataset:

$$
\mathbf{X} = \{x_1, x_2, \dots, x_n\}, \quad x_i \in \mathbb{R}^d
$$

the objective is to identify observations that deviate significantly from the underlying distribution.

Formally, we seek to detect points such that:

$$
x_i \not\sim P(X)
$$

where $P(X)$ is the unknown data-generating distribution.

## Methodology

### 1. Interquartile Range (IQR)

The IQR method detects outliers based on quartiles:

$$
IQR = Q_3 - Q_1
$$

An observation is considered an outlier if:

$$
x < Q_1 - 1.5 \cdot IQR \quad \text{or} \quad x > Q_3 + 1.5 \cdot IQR
$$

This approach is applied independently to each variable, making it inherently univariate.

---

### 2. Local Outlier Factor (LOF)

LOF measures the local density deviation of a point relative to its neighbors.

The local reachability density is defined as:

$$
lrd_k(x) = \left( \frac{\sum_{o \in N_k(x)} \text{reach-dist}_k(x,o)}{|N_k(x)|} \right)^{-1}
$$

The LOF score is:

$$
LOF_k(x) = \frac{\sum_{o \in N_k(x)} \frac{lrd_k(o)}{lrd_k(x)}}{|N_k(x)|}
$$

Values significantly greater than 1 indicate potential outliers.

---

### 3. Isolation Forest

Isolation Forest isolates anomalies by randomly partitioning the data.

The anomaly score is defined as:

$$
s(x, n) = 2^{-\frac{E(h(x))}{c(n)}}
$$

where:

- $E(h(x))$ is the expected path length  
- $c(n)$ is a normalization factor  

Outliers tend to have shorter path lengths and higher anomaly scores.

---

## Simulation Design

The dataset is simulated with:

- A main cluster (normal observations)
- Global outliers (far from the main distribution)
- Local outliers (within range but in sparse regions)

This allows evaluating how each method behaves under different anomaly structures.

---

## Results

The results show that:

- IQR identifies global extreme values but fails to detect local anomalies  
- LOF captures local density variations and detects contextual outliers  
- Isolation Forest effectively isolates both global and local anomalies  

From a statistical perspective:

$$
\text{Different assumptions} \Rightarrow \text{Different outliers}
$$

This highlights that outlier detection is not a unique solution problem, but depends on the chosen modeling framework.

---

## Data Science Interpretation

In real-world applications:

- Statistical methods are simple and interpretable  
- Machine learning methods capture complex structures  
- Choice of method depends on the data geometry  

Outlier detection is therefore both a statistical inference problem and a modeling decision.

---

## Conclusion

This project demonstrates that different methods lead to different interpretations of anomalies.

Understanding the assumptions behind each technique is essential before applying them in practice.

Rather than asking "which method is best", a more appropriate question is:

$$
\text{Which method aligns with the structure of my data?}
$$

---

## References

- Breunig, M. M., Kriegel, H. P., Ng, R. T., & Sander, J. (2000). LOF: Identifying density-based local outliers.  
- Liu, F. T., Ting, K. M., & Zhou, Z. H. (2008). Isolation Forest.  
- Tukey, J. W. (1977). Exploratory Data Analysis.  
- Chandola, V., Banerjee, A., & Kumar, V. (2009). Anomaly detection: A survey.  
