## Atenção: 
- Os dados usados para esse projeto foram coletados na plataforma Kaggle. 
- O problema apresentado é fictício, criado com o intuito de aprender Ciência de Dados
- O projeto foi orientado pela Comunidade DS
<hr>


> **Resumo**: Projeto de Ciência de dados utilizando Machine Learning - Classificação para detecção de doenças cardíacas em estágios iniciais presando pela melhor precisão como score final. O projeto end-to-end foi realizado com método CRISP-DM e passou pelas seguintes etapas: ETL, Estatistica Descritiva, Feature Engineering, Preparação dos dados (Enconding, rescalling e transformação), Feature Selection, Treinamento de Machine Learning, Hiperparameter fine Tuning, Tradução e interpretação do erro,

# CardioCatch Disease

# 1. Business Problem.
Cadio Catch Diseases é uma empresa especializada em detecção de doenças cardíacas em estágios iniciais. O seu modelo de negócio é do tipo Serviço, ou seja, a empresa ofereço o diagnóstico precoce de uma doença cardiovascular por um certo preço.
Atualmente, o diagnóstico de uma doença cardiovascular é feita manualmente por uma equipe de especialistas.A precisão atual do diagnóstico varia entre 55% e 65%, devido a complexidade do diagnóstico e também da fadiga da equipe que se revezam em turnos para minimizar os riscos. O custo de cada diagnóstico, incluindo os aparelhos e a folha de pagamento dos analistas, gira em torno de R$ 1.000,00.
O preço do diagnóstico, pago pelo cliente, varia de acordo com a precisão conseguida pelo time de especialistas, o cliente paga R$500,00 a cada 5% de acurácia acima de 50%. Por exemplo, para uma precisão de 55%, o diagnóstico custa R$500,00 para o cliente, para uma precisão de 60%, o valor é de R$ 1000,00 e assim por diante. Se a precisão do diagnóstico for 50% o cliente não paga por ele.

Observe que a variação da precisão dada pelo time de especialistas, faz com que a empresa tenha ora uma operação com lucro, receita maior que o custo, ora uma operação com prejuízo, receita menor que o custo. Essa instabilidade do diagnóstico faz com que a empresa tenha um Cashflow imprevisível.
O seu objetivo como o Cientista de Dados contratado pela Cardio Catch Diseases é criar uma ferramenta que aumente a precisão do diagnóstico e que essa precisão seja estável para todos os diagnósticos.
Portanto o seu trabalho como Data Scientist é criar um ferramenta de classificação de doentes, como umaprecisão estável. Junto com a ferramenta, você precisa enviar um relatório para o CEO da Cardio Catch Diseases, reportando os resultados e respondendo às seguintes perguntas: 

1. Qual a Acurácia e a Precisão da ferramenta?
2. Quanto lucro a Cardio Catch Diseases passará a ter com a nova ferramenta?
3. Qual a Confiabilidade do resultado dados pela nova ferra enta?

**Principais Ferramentas utilizadas:** 
- Python (pandas, math, inflection, numpy, seaborn, matplotlib, tabulate), 
- Machine Learning (XGBoost, random, scipy, sklearn: Random Forest, LinearRegression, Lasso, boruta) 
- Estatística (Skleanin.metrics, RobustScaler, MinMaxScaler, LabelEncoder) 
- API (pickle, request, Flask, json)
- Render, Telegram, VSCode, Jupyter Notebook

## 2. Planejamento

A construção do projeto foi realizada com a metodologia CRISP-DM, isto é, um método cíclico de solução de problemas de Ciência de Dados. O objetivo é entregar valor o mais rápido possível para o negócio e melhorar continuamente a solução. Para saber mais leia em [Medium](https://medium.com/comunidadeds/voc%C3%AA-tem-os-dados-tem-o-problema-de-neg%C3%B3cio-mas-e-agora-o-que-fazer-bf3b2d06482)

Principais etapas do planejamento: 
**Step 01. Data Description; Step 02. Feature Engineering; Step 03. Exploratory Data Analysis; Step 04. Data Preparation; Step 05. Feature Selection; Step 06. Machine Learning Modelling; Step 07. Hyperparameter Fine Tunning; Step 08. Convert Model Performance to Business Values:**


## 3. Business Assumptions.

### Dados:
- Age | Objective Feature | age | int (days)
- Height | Objective Feature | height | int (cm) |
- Weight | Objective Feature | weight | float (kg) |
- Gender | Objective Feature | gender | categorical code | 1 - women, 2 - men 
- Systolic blood pressure | Examination Feature | ap_hi | int |
- Diastolic blood pressure | Examination Feature | ap_lo | int |
- Cholesterol | Examination Feature | cholesterol | 1: normal, 2: above normal, 3: well above normal |
- Glucose | Examination Feature | gluc | 1: normal, 2: above normal, 3: well above normal |
- Smoking | Subjective Feature | smoke | binary |
- Alcohol intake | Subjective Feature | alco | binary |
- Physical activity | Subjective Feature | active | binary |
- Presence or absence of cardiovascular disease | Target Variable | cardio | binary |

### Outliers

O filtro dos outliers foram feitos com base na literatura.

- Altura: Foram desconsiderados valores menores que: **120 cm**  e maiores que: **200 cm**
- Peso: Foram desconsiderados valores menores que: **40 kg** e maiores que: **170 kg**
- ap_hi: Foram desconsiderados valores menores que: **90 mmHg** e maiores que: **200 mmHg**
- ap_lo: Foram desconsiderados valores menores que: **30 mmHg** e maiores que: **150 mmHg**

# 4. Top 3 Data Insights

Para facilitar a criação de hipósteses foi criado o mapa mental abaixo: 
<div align="center">
<img src="https://imgur.com/IzZnQje" />
</div><br>


De acordo com o nosso banco dde dados foi possível validar as seguintes hipóteses:

**Hypothesis 01:**
Pessoas com IMC alto tem mais propensão à desenvolver problemas cardíacos
**True**
<div align="center">
<img src="https://imgur.com/M61cjHM" />
</div><br>

**Hypothesis 02:**
Fumantes tem mais propensão à desenvolver problemas cardíacos
**False.**
<div align="center">
<img src="https://imgur.com/BTItbwi" />
</div><br>

**Hypothesis 03:**
Pessoas que bebem tem mais propensão à desenvolver problemas cardíacos
**False.**
<div align="center">
<img src="https://imgur.com/UKKrcNC" />
</div><br>


# 5. Machine Learning Model Applied

Foram treinados alguns modelos de ML e dentre eles foi separado os modelos com melhores parâmetros para fazer avaliação de performance. 
<div align="center">
<img src="https://imgur.com/6hLimWs" />
</div><br>

Escolhi seguir com os modelos: XGBoostClassifier, LGBMClassifier, LogistiRegression e SGDClassifier pois apresentaram o melhor balanço entre Precisão, Recall e f1-score.


# 6. Machine Learning Modelo Performance

Dos 4 modelos escolhidos o XGBoostClassifier e o LGBMClassifier apresentaram o melhor desempenho na matriz de confusão, e na curva ROC. 
Contudo, preferi seguir com o XGBoostClassifier por ser mais rápido e mais optimizado de maneira geral. 

Avaliação da Matrix de confusão:
<div align="center">
<img src="https://imgur.com/0usIK4Y" />
</div><br>

Avaliação da Curva ROC:
<div align="center">
<img src="https://imgur.com/CH8YXK0" />
</div><br>


# 7. Business Results e Conclusão

Os calculos finais foram calculados com base na métrica pré-estabelecida pela área de negócio: a precisão. Com isso, se o modelo fosse implementado poderia ser esperado um retorno de $180,490,556.97 no melhor cenário, no pior cenário: $163,173,926.15 tendo uma média de: $171,832,241.56.

Somente com esse resultado já vemos um retorno financeiro muito vantajogo para empresa. Contudo, seria importante levar em consideração que, se tratando de um problema médico, caberia avaliar se a precisão seria a melhor escolha. Isso porque as chances de falsos negativos podem ser grande, logo, seria um problema para o paciente deixar de ter o diagnóstico de um problema cardíaco. Neste caso, um bom parâmetro de avaliação poderia ser o equilíbio entre a precisão e o recall, como por exemplo o f1-score.


# 10. Next Steps to Improve
- Colocar o modelo em produção em núvem.
- Se fosse possível, solicitar mais variáveis relacionados à saúde para a área de negócio afim de melhorar a precisão/f1-score
- Desenvolver e oferecer um serviço ao cliente, para que ele tenha acesso ao seu status de saúde.
