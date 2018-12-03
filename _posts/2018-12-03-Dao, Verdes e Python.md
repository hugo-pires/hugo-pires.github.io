---
published: true
---

Vamos continuar a olhar os dados das edições que vão de Junho de 2017 a Maio de 2018, da ["Vinho Grandes Escolhas"](https://grandesescolhas.com/). Continuámos no [post anterior]({% post_url 2018-11-18-É preciso continuar em movimento %}) a utilizar o **Pandas** e hoje vamos avançar um pouco mais.


```python
import pandas as pd
%matplotlib inline

vinhos = pd.read_excel('output_analise/vinhos.xlsx')
```

Vamos caminhar um pouco pelas regiões produtoras de vinhos. Devemos ter em atenção que pode existir, por motivos de qualidade, mais do que uma denominação por cada uma das regiões.


```python
vinhos['regiao'].value_counts().head(10)
```




    Douro              467
    Reg. Alentejano    342
    Reg. Lisboa        196
    Alentejo           161
    Dão                138
    Vinho Verde        122
    Reg. Tejo          121
    Porto              100
    Bairrada            78
    DO Tejo             66
    Name: regiao, dtype: int64



Vemos aqui quais são as **10** primeiras denominações quanto ao número de vinhos.


```python
round(vinhos['regiao'].value_counts().head(10).sum() / len(vinhos['regiao']), 2)
```




    0.77



E concluímos qque correspondem a **77%** dos vinhos. Para tal utilizámos uma expressão um pouco comprida - o Python é acusado de abusar destes *one liners* - mas onde já encontramos uma pequena amostra do verdadeiro potencial do **Pandas**.

Agora, um pouco de gosto pessoal aqui e nada de conhecimento técnico - vamos comparar Vinhos do Dão com Vinhos Verdes.


```python
vinhos[vinhos['regiao'] == 'Dão']['tipo'].value_counts()
```




    branco    67
    tinto     63
    rosé       4
    Name: tipo, dtype: int64




```python
vinhos[vinhos['regiao'] == 'Vinho Verde']['tipo'].value_counts()
```




    branco    97
    tinto      8
    rosé       7
    Name: tipo, dtype: int64



Para encontrar o número de vinhos de cada tipo para cada uma das regiões, filtramos a **dataframe** usando uma condição aplicada à coluna **regiao**, e de seguida usamos o já conhecido método `value_counts`. Podemos concluir que há maior equilíbrio entre *brancos* e *tintos* na Região do *Dão*.


```python
vinhos[vinhos['regiao'] == 'Dão']['grau'].mean()
```




    13.22463768115942




```python
vinhos[vinhos['regiao'] == 'Vinho Verde']['grau'].mean()
```




    13.073770491803279



Utilizando um processo semelhante, e calculando a **média** podemos concluir que o **grau** dos vinhos difere muito pouco entre as regiões...


```python
vinhos[vinhos['regiao'] == 'Dão']['preco'].mean()
```




    15.824264705882356




```python
vinhos[vinhos['regiao'] == 'Vinho Verde']['preco'].mean()
```




    7.765042016806723



... mas o **preço** sim.

Para a  **classificação numerica** dada pelos provadores da revista, vamos fazer de forma ligeiramente diferente, tornando o código mais legível e tentando obter mais informação - a **média** pode ser insuficiente.


```python
vinhos_do_dao = vinhos[vinhos['regiao'] == 'Dão']
vinhos_verdes = vinhos[vinhos['regiao'] == 'Vinho Verde']
```


```python
classificacao_dos_vinhos_do_dao = vinhos_do_dao['classificacao numerica']
classificacao_dos_vinhos_verdes = vinhos_verdes['classificacao numerica']
```

Na prática construímos **dataframes** intermédias, às quais podem ser dados nomes com significado e que podem ser usadas (e reutilizadas) numa abordagem por etapas.


```python
classificacao_dos_vinhos_do_dao.mean(), classificacao_dos_vinhos_do_dao.std()
```




    (16.681159420289855, 0.787544527730836)




```python
classificacao_dos_vinhos_verdes.mean(), classificacao_dos_vinhos_verdes.std()
```




    (15.737704918032787, 0.7692787078743544)



Os **Vinhos do Dão** são, em média, considerados melhores do que os **Vinhos Verdes**, o que é, numa primeira análise confirmado por um **desvio padrão** semelhante.
