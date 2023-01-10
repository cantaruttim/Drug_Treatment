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
```

ao realizarmos a leitura do banco de dados temos:

<img width="267" alt="df" src="https://user-images.githubusercontent.com/81988636/211586257-28d0b094-bd63-4cd7-b699-f6d0ba2bd475.png">

Observe que os valores numéricos são apenas o que estão na coluna Age e Na_to_K. Já as outras colunas se continuarem com valores `categóricos`, o modelo não será possível realizar as previsões, portanto precisamos mudar isso. E iremos utilizar o `LabelEncoder` para tratarmos essas variáveis categóricas.
