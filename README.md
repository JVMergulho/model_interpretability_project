# Model Interpretability Project
Repositório para explorar técnicas de interpretabilidade de modelos de machine learning em um problema de classificação multiclasse.

## 1. Dataset
Dataset usado: https://archive.ics.uci.edu/dataset/577/codon+usage

Esse dataset contém informações sobre o uso de códons em diferentes organismos. Cada linha representa um organismo e as colunas representam a frequência relativa de cada códon. O objetivo é prever a classificação do grupo com base no padrão de uso de códons.

A coluna Kingdom contém 11 categorias diferentes, mas para simplificar o problema, agrupamos essas categorias em 4 grupos principais, removendo grupos com poucas amostras e combinando categorias semelhantes.

Grupos construídos:
- Plantae
- Bacteria
- Animalia
- Virus

Para a classificação, usamos as colunas de 6 a 69 como features, que representam a frequência relativa dos códons.

## 2. Modelling
O modelo base foi um Random Forest Classifier com hiperparâmetros ajustados usando o Optuna, resultando em uma acurácia de aproximadamente 96% no conjunto de teste.

## 3. Global Interpretability
Para a interpretabilidade global, utilizamos as seguintes técnicas:
- Global Surrogate Model: Treinamos modelos de árvore de decisão e regressão logística lasso para aproximar o comportamento do Random Forest.
- Permutation Feature Importance: Avaliamos a importância das features com base na mudança na acurácia do modelo ao permutar os valores de cada feature.
- Partial Dependence Plots (PDP): Analisamos o efeito marginal das features mais importantes na predição do modelo.