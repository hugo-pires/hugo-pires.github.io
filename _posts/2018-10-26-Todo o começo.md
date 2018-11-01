---
published: true
---
# Os vinhos do primeiro ano da "Grandes Escolhas"

Ao longo do seu primeiro ano de existência, nas edições que vão de Junho de 2017 a Maio de 2018, a ["Vinho Grandes Escolhas"](https://grandesescolhas.com/) provou e avaliou centenas de vinhos de todo o país (e alguns do estrangeiro). Sobre cada um deles estão disponíveis algumas variáveis que nos permitiram construir um dataset já previamente compilado.

Os dados estão guardados num ficheiro Excel e queremos que estejam em memória para que possamos usar o Python e trabalhar sobre eles. É aqui que entra uma biblioteca que nos vai acompanhar por muito tempo nesta análise, o **Pandas** - https://pandas.pydata.org/. Comecemos por importá-la usando uma convenção:

```python
import pandas as pd
```

Uma das suas principais vantagens é que torna muito fácil carregar em memória (numa *dataframe*) dados de diferentes formatos - os mais habituais serão EXCEL, CSV, JSON, mas também outros menos comuns que poderão encontrar na documentação.

```python
vinhos = pd.read_excel(´vinhos.xlsx´)
```

O processo pode ser tão simples quanto isso, mas o método permite especificar um grande número de parâmetros que nos ajudam a lidar com as características especiais de cada ficheiro.

Vamos ver o que criámos de forma rápida, utilizando uma amostra aleatória de três linhas da Dataframe:

|   classificacao numerica |   preco | selo boa escolha   | guarda   | nome             | regiao                    | castas    |
|-------------------------:|--------:|:-------------------|:---------|:-----------------|:--------------------------|:----------|
|                     16   |   16.5  | SEM ESCOLHA        | B        | Casal Sta. Maria | Reg. Lisboa               | Malvasia  |
|                     16   |    5.49 | BOA ESCOLHA 2017   | A        | Vila Nova        | Vinho Verde               | nan       |
|                     16.5 |   35    | SEM ESCOLHA        | A        | Comendador Costa | Reg. Península de Setúbal | Encruzado |


Encontramos exemplos dos valores das diferentes variáveis para cada um dos vinhos - números, texto, siglas.

Também podemos saber o tamanho da dataframe, ou seja o seu número de linhas e colunas:

```python
vinhos.shape
(2328, 18)
```

Assim, cada linha corresponde a um vinho e cada coluna a uma **variável** que caracteriza o vinho. No momento da leitura, o *Pandas* fez algumas 'suposições' sobre o **tipo** de cada variável.

```python
vinhos.dtypes

classificacao numerica      float64
preco                       float64
selo boa escolha             object
guarda                       object
nome                         object
regiao                       object
castas                       object
designativo de qualidade     object
tipo                         object
ano                           int64
produtor                     object
descricao da prova           object
grau                        float64
provador                     object
mes                          object
ano_pub                       int64
idade                         int64
relacao                     float64
dtype: object
```
Para já podemos fazer uma distinção simples entre:
* variáveis **qualitativas** (ou nominais, "categoricals", em inglês) que são representadas com um tipo **object**, e sobre as quais é possível apenas estabelecer comprações e
* variáveis **quantitativas** que são representadas com um tipo **float** ou **int**, e sobre as quais é possível fazer um conjunto mais alargados de operações matemáticas.

No que diz respeito às variáveis numéricas, é fácil conseguir um "resumo" dos seus conteúdos:

```python
vinhos.describe()
```

||   classificacao numerica |     preco |      ano |       grau |     ano_pub |     idade |   relacao |
|-|-------------------------:|----------:|---------:|-----------:|------------:|----------:|----------:|
|count|              2328        | 2207      | 2328     | 2328       | 2328        | 2328      |  2207     |
|mean|                16.454    |   17.587  | 1939.42  |   13.7073  | 2017.3      |   77.8763 |   inf     |
|std|                 0.980051 |   34.7815 |  377.123 |    3.06619 |    0.457905 |  377.133  |   nan     |
|min|                 0        |    0      |    0     |    0       | 2017        |    1      |     0     |
|25%|                16        |    6      | 2014     |   12.5     | 2017        |    1      |     0.905 |
|50%|                16.5      |    9.99   | 2015     |   13.5     | 2017        |    2      |     1.65  |
|75%|                17        |   18.5    | 2016     |   14       | 2018        |    4      |     2.67  |
|max|                21        |  900      | 2017     |   55.8     | 2018        | 2018      |   inf     |

Podemos assim, para já saber algumas coisas interessantes:
* que não temos toda a informação sobre todos os vinhos - basta verificar que a linha **count** não é igual para todos
* que existem erros a corrigir - a variável **grau** tem um valor mínimo de **0**
* que o preço médio de um vinho é 17,59 €

Continuaremos o nosso trabalho no pŕoximo post.
