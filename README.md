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

## 4. Local Interpretability

Para compreender a tomada de decisão em nível de instância, aplicamos métodos de explicação local em amostras de interesse (acertos de alta confiança e casos de fronteira/erro):

- LIME (Local Surrogate Model): Empregamos o LIME para aproximar o comportamento local do Random Forest através de modelos lineares esparsos. A técnica foi utilizada para validar a influência direcional (positiva ou negativa) dos códons mais impactantes na vizinhança de instâncias específicas.
- SHAP (SHapley Additive exPlanations): Utilizamos o TreeExplainer para decompor a predição na soma das contribuições de cada feature. A análise revelou que o modelo frequentemente decide pelo acúmulo de pequenas contribuições de dezenas de códons ("decisão distribuída") e identificou que erros de baixa confiança ocorrem quando marcadores principais (como CUU e ACA) apresentam sinais contraditórios na mesma amostra.