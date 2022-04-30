# Introduction

Neste arquivo é descrita a metodologia utilizada para realização dos experimentos realizados em: **Resampling strategies for imbalanced regression: a survey**. O objetivo é permitir que outros pesquisadores sejam capazes de replicar os resultados apresentados.

# Contents
Este arquivo contém:
- O diretório **appendices** com todos os resultados obtidos.
  - **Appendix A**: Resultados por conjunto de dados para melhor configuração dos modelos de aprendizado e das estratégias de pré-processamento.
  - **Appendix B**: Ranking de médias para cada métrica utilizada.
  - **Appendix C**: Média da quantidade de exemplos de treinamento gerado por cada estratégia de pré-processamento.
- O diretório **data** com os 17 conjuntos de dados utilizados. As principais caracteristicas dos dados são:


|Conjunto de dados | N    | p.total | p.nom | p.num | nRaro | % Raro|
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

em que, N: Número de casos; p.total: Número de atributos; p.nom: Número de atributos nominais; p.num: Número de atributos numéricos; nRaro: Número de casos raros; %Raro: 100 X nRaro/N).


# Tools

Os experimentos foram realizados em Python e utilizados pacotes em R através da biblioteca [rpy2](https://rpy2.github.io/).

- Foram utilizadas as seguintes ferramentas:

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


- Métricas utilizadas:
  - [F1-score](https://github.com/rpribeiro/uba)
  - [SERA](https://github.com/nunompmoniz/IRon)


# How does it work?

Para obter os resultados apresentados deve-se considerar as estratégias de pré-processamento (algoritmos de balanceamento) e parâmetros descritos na tabela a seguir. É importante salientar que as estratégias de pré-processamento devem ser aplicadas somente no conjunto de treinamento.

| Algoritmo  |  Parâmetro |
| -----| ------------------------- |
|  SMT |  u/o = {balance, extreme} |
|  RO  |  u/o = {balance, extreme} |
|  RU |  u/o = {balance, extreme} |
|  GN  |  u/o = {balance, extreme}, δ = {0.05, 0.1, 0.5} |
|  SG |  u/o = {balance, extreme} |
|  WERCS  |  u = {0.5, 0.8}, o = {0.5, 0.8} |

Todos os resultados foram calculados aplicando 2 repeticões com 10-_fold cross-validation_ e foi utilizado o _GridSearchCV_ para buscar os melhores parâmetros dos algoritmos de aprendizado. Foram utilizados os seguintes parâmentros e modelos de aprendizado:

| Algoritmo  |  Parâmetro |
| -----| ------------------------- |
|  BG  |  min_samples_split = 20, max_samples = 0.5 |
|  DT  |   min_samples_split = 20 |
|  MLP |  learning_rate_init = 0.1, momentum = {0.1, 0.2, 0.7}, tol = {0.01, 0.05}, max_inte = 5000 |
|  RF  |  n_estimators = {500, 1500}, max_features = 5|
|  SVM |  gamma = {0.01, 0.001}, C = {10, 300} |
|  XG  |  eta = 0.01, max_depth = {10, 15}, colsample_bytree = {0.2,..., 0.9}, num_round = 25 |


A imagem a seguir descreve os passos realizados. Inicialmente foi feito um pré-processamento dos atributos nominais através do método _LabelEncoder_, para atributos ordinais foi obedecida a ordem pré-definida (ex. _small_ : 1, _medium_: 2, _large_: 3). Em seguida foi separado o conjunto de dados em treinamento (_Train set_) e teste (_Test set_), os dados de treinamento passam pelo processo de reamostragem (_Resampling_), a partir dos dados balanceados (_Balanced train set_) é gerado o modelo de aprendizado (_Model generation_) que é avaliado (_Model evaluating_) e obtido seu desempenho (_Performance estimation_).

![alt text](https://github.com/JusciAvelino/imbalancedRegression/blob/main/diagram.png)
