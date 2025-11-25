## CausalFairnessInAction

As machine learning (ML) systems are increasingly deployed in high-stakes domains, the need for robust methods to assess fairness has become more critical. While statistical fairness metrics are widely used due to their simplicity, they are limited in their ability to explain why disparities occur, as they rely on associative relationships in the data. In contrast, causal fairness metrics aim to uncover the underlying data-generating mechanisms that lead to observed disparities, enabling a deeper understanding of the influence of sensitive attributes and their proxies. Despite their promise, causal fairness metrics have seen limited adoption due to their technical and computational complexity. To address this gap, we present CausalFairnessInAction, the first open-source Python package designed to compute a diverse set of causal fairness metrics at both the group and individual levels.The metrics implemented are broadly applicable across classification and regression task (with easy extensions for intersectional analysis) and were selected for their significance in the fairness literature. We also demonstrate how standard statistical fairness metrics can be decomposed into their causal components, providing a complementary view of fairness grounded in causal reasoning.

The package currently implements algorithms for three key measures established in the causal fairness literature:

| **Metric**                                             | **Query Addressed**                                                                                                                                                                                                                                       | **Level**     | **Supported Metric Decomposition** | **Counterfactual Estimation Procedure**                                       |
|--------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------|--------------------------------------------------------------------------------|
| Counterfactual Effects (for Statistical Parity)        | What would the disadvantaged (advantaged) group's acceptance rate be if they had the identity (A), mediating characteristics (M), or confounding characteristics (C) of the advantaged (disadvantaged) group?                                             | Aggregate     | Direct, Indirect, Spurious         | Conditional probabilities (computed or estimated using GMM)                   |
| Counterfactual Equalized Odds                          | What would the disadvantaged (advantaged) group's error rate be if they had the identity (A), mediating characteristics (M), or confounding characteristics (C) of the advantaged (disadvantaged) group?                                                  | Aggregate     | Direct, Spurious                   | Conditional probabilities (computed or estimated using GMM)                   |
| Counterfactual Fairness                                | What would the disadvantaged (advantaged) individual's predicted Y be if they had the identity (A), mediating characteristics (M), and confounding characteristics (C) of the advantaged (disadvantaged) group?                                          | Individual    | N/A                                | Predictions from functional relationships of fitted SCM                       |


## Useage [Forthcoming]

The core of the *CausalFairness* package is the `CausalFairnessDecomposition` class, built on the standard fairness model. It accepts $X, Y, \hat{Y}$, lists for $A, M$, optionally $C$, derived from an SCM (algorithmically discovered or expert-curated) or a DAG, and a task-type flag (regression/classification). The class provides three main methods:

- `analyse_mean_difference` - causal decompositon of statistical parity using the Counterfactual Effects framework; 
- `analyse_equalized_odds` - causal decomposition of error rates; 
- `analyse_counterfactual_fairness` - individual-level counterfactual fairness analysis. 

Each method compares the outcome(acceptance rate, error rates, or predicted outcome $\hat{Y}_i$) in two counterfactual worlds: one with observed $A$, and one with counterfactual $A$. 

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the CC-BY-NC 4.0 License.

