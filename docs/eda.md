# Análise Exploratória de Dados (EDA)

## Introdução

Este documento detalha a Análise Exploratória de Dados (EDA) realizada no dataset de reservas de hotéis, contendo informações sobre dois tipos de hotéis: Hotel Resort e Hotel Urbano. O objetivo desta análise é entender o comportamento das reservas, incluindo cancelamentos, distribuição de hóspedes por país, duração das estadias e outros aspectos relevantes.

## Importação das bibliotecas

* **`Pandas`** é utilizado para manipulação e análise de dados
* **`Seaborn`** é utilizado para criação de gráficos estatísticos
* **`Matplotlib`** é utilizado para criação de gráficos em geral
* **`Numpy`** é utilizado para operações numéricas eficientes
* **`Datetime`** é utilizado para manipulação de datas e horas
* **`Scatter_matrix`** é utilizado para criação de matrizes de dispersão, úteis na análise exploratória
* **`Warnings`** é utilizado para controle de alertas/avisos, aqui configurado para ignorar avisos

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import numpy as np
import warnings
warnings.filterwarnings("ignore")
```

Os dados coletados nos dois hoteis, estão em um único arquivo do tipo csv e para lê-lo usamos a função *'read_csv'* do pandas:

```python
# Carregamento do dataset de reservas de hotéis
df = pd.read_csv('https://raw.githubusercontent.com/matteeussPei/Hotel-Booking-Demand/main/hotel_bookings.csv')
```

## Análise Introdutória

Agora verificamos a **quantidade de registros e variáveis** no arquivo, através da atributo *'shape'* de um dataframe:

```python
# Exibição do número total de variáveis (colunas) e entradas (linhas) no dataset
print('Total de variáveis:', df.shape[1])
print('Total de entradas:', df.shape[0])
```

o arquivo possui um total de : **32 variáveis** e **11939 entradas.**

---

Para saber como os tipos de variáveis estão distribuídos usamos o atributo *'dtypes'*:

```python
df.dtypes.value_counts()
```

obtendo 16 variáveis do tipo **`int64`**, 12 do tipo **`object`** e 4 do tipo **float64.**

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

Nesta seção vimos como os dados estão apresentados: a quantidade de registros, o tipo de cada variável ou se há valores nulos.

## Transformação dos dados

Visto que a variável *'company'* é praticamente nula, será desconsiderada em nossa análise; assim como a coluna *'agent'*, pois se trata do ID da agência de viagens que fez a reserva. Para isso usamos:

```pyhton
df.drop(columns = ['agent', 'company'], inplace=True)
```

Os valores ausentes nas colunas *'country'* e *'children'* serão preenchidos com a moda e mediana, para evitar enviesamento da análise.

```python
df['country'].fillna(df['country'].mode()[0],inplace=True)
df['children'].fillna(df['children'].median(), inplace=True) 
```

---

Criamos também uma nova coluna que contabilize o tempo total de cada reserva, soma das variáveis *'stays_in_week_nights'* e *'stays_in_weekend_nights':*

```pyhton
df['total_days'] = df['stays_in_week_nights'] + df['stays_in_weekend_nights']
```

---

Apagamos os registros duplicados, pois nessa situação reservas duplicadas com certeza é um erro:

```pyhton
df.drop_duplicates(inplace=True)
```

---

E filtramos para que reservas onde a quantidade de adultos, crianças e bebes fosse iguais a zero, fossem desconsideradas, afinal não tem como.

```python
filtro = (df['babies'] == 0) & (df['children'] == 0) & (df['adults'] == 0)
df = df[~filtro]
```

---

AInda nesta seção também iremos renomear elementos da coluna *'meal'*, para melhor compreensão, onde :

* **`Undefined/SC`** - No Meal;
* **`BB`** – Bed & Breakfast;
* **`HB`** – Half board (breakfast and one other meal– usually dinner);
* **`FB`** – Full board (breakfast, lunch and dinner)

```python
df['meal'].replace(['Undefined', 'BB', 'FB', 'HB', 'SC'], 
                   [ 'No Meal', 'Breakfast', 'Full Board', 'Half Board', 'No Meal'],
                   inplace = True)
```

---

Por fim, também iremos substituir as siglas dos países da coluna *'country'* por seus nomes, por exemplo:

* **`AFG`** - Afghanistan
* **`ALB`** - Albania
* **`AGO`** - Angola

Para isso usei um documento que contém o nome dos países e suas siglas, criei um dicionário e fiz a substituição:

```python
dict_country= {}
for i,j in zip(countries_code['alpha-3'], countries_code['name']):
    dict_country[i] = j
```

```python
df['country'].replace(dict_country, inplace= True)
```

## Análise Exploratória

Através do atributo '*value_counts'* observamos que há mais registros de reservas não canceladas do que canceladas:

```python
# quantidade de reservas não canceladas e canceladas
print(df['is_canceled'].value_counts())
```

temos **75166 não canceladas** e **44224 reservas canceladas**.
