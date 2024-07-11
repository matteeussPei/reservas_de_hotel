# Análise Exploratória de Dados (EDA)

## Introdução

Este documento detalha a Análise Exploratória de Dados (EDA) realizada no dataset de reservas de hotéis, contendo informações sobre dois tipos de hotéis: Hotel Resort e Hotel Urbano. O objetivo desta análise é entender o comportamento das reservas, incluindo cancelamentos, distribuição de hóspedes por país, duração das estadias e outros aspectos relevantes.

## Importação das bibliotecas

* Pandas é utilizado para manipulação e análise de dados
* Seaborn é utilizado para criação de gráficos estatísticos
* Matplotlib é utilizado para criação de gráficos em geral
* Numpy é utilizado para operações numéricas eficientes
* Datetime é utilizado para manipulação de datas e horas
* Scatter_matrix é utilizado para criação de matrizes de dispersão, úteis na análise exploratória
* Warnings é utilizado para controle de alertas/avisos, aqui configurado para ignorar avisos

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import numpy as np
import warnings
warnings.filterwarnings("ignore")
```

## Análise Introdutória

Nesta seção vimos como os dados estão apresentados: a quantidade de registros, o tipo de cada variável ou se há valores nulos.
Os dados coletados nos dois hoteis, estão em um único arquivo do tipo csv e para lê-lo usamos a função *'read_csv'* do pandas:

```python
# Carregamento do dataset de reservas de hotéis
df = pd.read_csv('https://raw.githubusercontent.com/matteeussPei/Hotel-Booking-Demand/main/hotel_bookings.csv')
```



---

Agora verificamos a **quantidade de registros e variáveis** no arquivo, através da atributo *'shape'* de um dataframe:

```python
# Exibição do número total de variáveis (colunas) e entradas (linhas) no dataset
print('Total de variáveis:', df.shape[1])
print('Total de entradas:', df.shape[0])
```

o arquivo possui um total de : **32 variáveis** e **11939 entradas.**

---

Na busca por valores ausentes utilizamos o seguinte:

```python
pd.DataFrame({'dados_ausentes(%)': (df.isnull().sum()/df.shape[0])*100}).sort_values('dados_ausentes(%)', ascending=False)
```

como resposta obtemos a porcentagem de valores ausentes de cada variável, e somente **4 (quatro)** apresentaram valores ausentes:

* **`company`** com 94.30%
* **`agent`** com 13.69%
* **`country`** com 0.41%
* **`children`** com 0.003%

---

Para saber como os tipos de variáveis estão distribuídos usamos o atributo *'dtypes'*:

```python
df.dtypes.value_counts()
```

obtendo 16 variáveis do tipo **`int64`**, 12 do tipo **`object`** e 4 do tipo **float64.**

---

## 

Através do atributo '*value_counts'* observamos que há mais registros de reservar não canceladas do que canceladas:

```python
# quantidade de reservas não canceladas e canceladas
print(df['is_canceled'].value_counts())
```

temos 75166 reservas não canceladas e 44224 reservas canceladas.
