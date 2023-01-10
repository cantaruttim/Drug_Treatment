## Drug Treatment
 
O objetivo desse projeto é utilizar os parâmetros clínicos e bioquímicos para a previsão do melhor medicamento a ser utilizado na farmacoterapia de pacientes. Considerando a análise inicial do dataset iremos tratar a princípio de drogas que são utilizadas no sisterma cardiovascular, em especial para para medicamentos para a pressão. 

Iniciamos esse projeto importando as bibliotecas.

```
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
import plotly.express as px
import plotly.graph_objects as go
from sklearn.preprocessing import LabelEncoder
```

ao realizarmos a leitura do banco de dados temos:

<img width="267" alt="df" src="https://user-images.githubusercontent.com/81988636/211586257-28d0b094-bd63-4cd7-b699-f6d0ba2bd475.png">

Observe que os valores numéricos são apenas o que estão na coluna Age e Na_to_K. Já as outras colunas se continuarem com valores `categóricos`, o modelo não será possível realizar as previsões, portanto precisamos mudar isso. E iremos utilizar o `LabelEncoder` para tratarmos essas variáveis categóricas.

#### Dados para os modelos

Para usarmos como variáveis preditoras, vamos usar as colunas da `Age` até o valor de `Na_to_k`. Então selecionamos essas colunas com o código a seguir.

```
X = df.iloc[:, 0:5].values
X
```

Fazemos o mesmo para a variável previsora `y`, que contem o "rótulo" de qual medicamento foi prescrito para aquela condição. 
Já adiantando um ponto importante, adicionamos ao valor de y o método `LabelEncoder()` que trata as variáveis categóricas em variáveis numéricas, que serão utilizadas pelo modelo para realizar as previsões.

```
 y = df.iloc[:, 5].values
label_encoder_resultado = LabelEncoder()

y = label_encoder_resultado.fit_transform(y)
```

Aplicando o mesmo método para os valores categóricos da variável `X`, temos:

```
label_encoder_sexo = LabelEncoder()
label_encoder_bp = LabelEncoder()
label_encoder_Cholesterol = LabelEncoder()

X[:,1] = label_encoder_sexo.fit_transform(X[:,0])
X[:,2] = label_encoder_bp.fit_transform(X[:,1])
X[:,3] = label_encoder_Cholesterol.fit_transform(X[:,2])
```

Agora para os valores de `X` temos :

```
array([[23, 8, 8, 8, 25.355],
       [47, 30, 30, 30, 13.093],
       [47, 30, 30, 30, 10.114],
       [28, 12, 12, 12, 7.798],
       [61, 44, 44, 44, 18.043],
       [22, 7, 7, 7, 8.607],
       [49, 32, 32, 32, 16.275],
       [41, 25, 25, 25, 11.037],
       [60, 43, 43, 43, 15.171],
       [43, 27, 27, 27, 19.368],
       [47, 30, 30, 30, 11.767],
       [34, 18, 18, 18, 19.199],
       [43, 27, 27, 27, 15.376],
       [74, 56, 56, 56, 20.942],
       [50, 33, 33, 33, 12.703],
       [16, 1, 1, 1, 15.516],
       [69, 52, 52, 52, 11.455],
       [43, 27, 27, 27, 13.972],
       [23, 8, 8, 8, 7.298],
           ...
           
```

### Modelos

```
from sklearn.model_selection import cross_val_score, KFold
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier
from sklearn.neighbors import KNeighborsClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.svm import SVC
from sklearn.neural_network import MLPClassifier
```



