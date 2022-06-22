ODAP-B: A One-shot Distributed Algorithm for Modified Poisson Regression for Prospective Studies with Binary Data
==============================================
## Outline
1. Background
2. dCLR workflow


## Background
When analyzing a relatively rare binary outcome, the sparse data problem is a significant challenge1. The lack of sufficient cases (e.g., patients with disease) in the data leads to a biased estimation of the effect of a treatment in observational studies2,3. To tackle this challenge, traditional two-step meta-analysis is commonly used to combine the results across multiple studies. Meta-analysis provides a summary estimate with greater statistical precision but does not mitigate the sparse-data bias2. Although the number of cases is increased by using Individual Participant Data (IPD) meta-analysis, the IPD meta-analysis is not feasible when the individual-level data from different studies cannot be pooled due to privacy concerns. 

The logistic regression model is a natural choice for modeling binary data and provides an odds ratio (OR) for the effect of an intervention or strength of an association by comparing the exposed and unexposed groups. The relative risk (RR) is another metric reporting the effect magnitude of the two groups. The choice between RR and OR is a long-standing debate4-8 and RR is preferred over OR for most prospective studies due to collapsibility, especially when the outcome is not rare9. Poisson regression is usually recommended to estimate the adjusted relative risk directly10 for binary data as it can be used to approximate the binomial distribution when the sample size is large, and probability is small. Zou proposed a modified Poisson regression with a sandwich error term, which allows the direct estimation of the adjusted relative risk with robust variance estimation even when the Poisson model is misspecified for the binary outcome11. 

We proposed a one-shot distributed algorithm for the modified Poisson regression for binary data. In particular, we are interested in the investigation of rare binary data with the Poisson regression model9. Without requiring individual-level data, the proposed distributed algorithm transfers aggregated data across sites once to obtain the estimates of relative risk using the Poisson regression. Along with the consistent estimates of the intervention effects, the sandwich estimation offers a robust variance estimation of the estimated relative risk. 

## Methods
We propose a one-shot distributed modified Poisson regression approach for binary data and refer to it as ODAP-B. The workflow of the proposed algorithm is presented in Figure 1. Assume that there are K sites in total. Using methods developed by Jordan et. al12 and adapted to the clinical setting by Duan et al.13,14, we implemented a surrogate likelihood approach, by constructing the surrogate log-likelihood function whereby only local site patient-level data and gradients from other sites are needed. This procedure preserves the patient-level privacy in the data integration process by only transferring aggregated data across sites once. 
Let ${\theta} = (\alpha,\ \beta,\ {\gamma})$, we construct the surrogate log-likelihood $l_s\left(\{\theta}\right)$ 
where $l_1$ is the local log-likelihood, 
$\nabla$ $l_K(\bar{{\theta}})$ and ${\nabla}^2$ $l_K(\bar{{\theta}})$ are 
the averages of all K sites’ first gradients and second gradients of log-likelihood functions, respectively, and $\bar{{\theta}}$ is the initial value, 
which can be obtained by using the local estimate or a meta-estimate of ${\theta}$ and obtain the proposed ODAP-B estimator 
$\widetilde{{\theta}}.$

