# Introduction

This file is discribes the methodology used to perform the experiments presented in: **Resampling strategies for imbalanced regression: a survey**.

# Contents
This file contains:
- **code.ipynb** with the code implemented.
- **appendices** with all the results:
  - **Appendix A**: Results by dataset for better configuration of learning models and resampling strategies.
  - **Appendix B**: Average number of training examples generated by each resampling strategy.
- **data** with the 17 datasets. The main characteristics of the data are:


|Datasets | N    | p.total | p.nom | p.num | nRare | % Rare|
| -----------------|------|---------|--------|------|-------|-------|
|Abalone           |4177  | 8       | 1      | 7    | 679   | 16,3  |
|a3                |198   | 11      | 3      | 8    | 32    | 16,2  |
|a6                |198   | 11      | 3      | 8    | 32    | 16,2  |
|a4                |198   | 11      | 3      | 8    | 30    | 15,2  |
|a1                |198   | 11      | 3      | 8    | 28    | 14,1  |
|a7                |198   | 11      | 3      | 8    | 27    | 13,6  |
|boston            |506   | 13      | 0      | 13   | 65    | 12,8  |
|a2                |198   | 11      | 3      | 8    | 22    | 11,1  |
|a5                |198   | 11      | 3      | 8    | 21    | 10,7  |
|fuelCons          |1764  | 38      | 12     | 26   | 164   | 9,3   |
|heat              |7400  | 11      | 3      | 8    | 664   | 9,0   |
|availPwr          |1802  | 16      | 7      | 9    | 157   | 8,7   |
|cpuSm             |8192  | 13      | 0      | 13   | 713   | 8,7   |
|maxTorq           |1802  | 33      | 13     | 20   | 129   | 7,2   |
|ConcrStr          |1030  | 8       | 0      | 8    | 55    | 5,3   |
|Accel             |1732  | 15      | 3      | 12   | 89    | 5,1   |
|airfold           |1503  | 5       | 0      | 5    | 62    | 4,1   |

(N: number of cases; p.total: number of attributes; p.nom: number of nominal attributes; p.num: number of numeric attributes; nRare: number of rare cases; %Rare: 100 ?? NRaro/N )).


# Tools

The experiments were performed in Python and used packages in R through the library [rpy2](https://rpy2.github.io/).

- Packages:

  - [Scikit-learn](https://scikit-learn.org/stable/)
    - BaggingRegressor
    - DecisionTreeRegressor
    - MLPRegressor
    - RandomForestRegressor
    - SVR
  - [XGBoost](https://xgboost.readthedocs.io/)
    - XGBoost
  - [smogn 0.1.2](https://pypi.org/project/smogn/)
    - SMOGN
  - [resreg 0.2](https://pypi.org/project/resreg/)
    - WERCS
  - [UBL](https://github.com/paobranco/UBL)
    - SMOTER
    - Random over-sampling 
    - Random under-sampling
    - Gaussian Noise Introduction


- Metrics:
  - [F1-score](https://github.com/rpribeiro/uba)
  - [SERA](https://github.com/nunompmoniz/IRon)

# References

Paula Branco, Rita P Ribeiro, and Luis Torgo. 2016. UBL: an R package for utility-based learning. arXiv preprint arXiv:1604.08079 (2016).
Paula Branco, Luis Torgo, and Rita P Ribeiro. 2019. Pre-processing approaches for imbalanced distributions in regression. Neurocomputing 343
(2019), 76???99. (https://arxiv.org/abs/1604.08079) 

Paula Oliveira Branco, Lu??s Torgo, and Rita Paula Ribeiro. 2017. SMOGN: a pre-processing approach for imbalanced regression. In First International
Workshop on Learning with Imbalanced Domains: Theory and Applications, Vol. 74. 36???50.(http://proceedings.mlr.press/v74/branco17a)

Lu??s Torgo, Rita P Ribeiro, Bernhard Pfahringer, and Paula Branco. 2013. Smote for regression. In Portuguese conference on artificial intelligence.
Springer, 378???389. (https://link.springer.com/chapter/10.1007/978-3-642-40669-0_33)

Rita P Ribeiro and Nuno Moniz. 2020. Imbalanced regression and extreme value prediction. Machine Learning 109, 9 (2020), 1803???1835. (https://link.springer.com/article/10.1007/s10994-020-05900-9)
