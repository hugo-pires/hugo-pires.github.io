---
published: true
---
Vamos continuar a olhar os dados das edições que vão de Junho de 2017 a Maio de 2018, da ["Vinho Grandes Escolhas"](https://grandesescolhas.com/). Começámos no [post anterior]({% post_url 2018-10-26-Todo o começo %}) por utilizar o **Pandas** para importar os dados para memória. Vamos dar-lhes mais atenção.

```python
import pandas as pd
vinhos = pd.read_excel('vinhos.xlsx')
```
Tal como já perceberam, uma *dataframe* é formada por **colunas** que correspondem a cada uma das variáveis disponíveis e **linhas** que são registos distintos, neste caso, cada vinho.

Por exmplo, se quiserem aceder aos valores da **coluna** *tipo* basta utilizar a seguinte notação:

```python
vinhos['tipo']

0    branco
1     tinto
2    branco
3     tinto
4    branco
Name: tipo, dtype: object
```
Entretanto, já entendemos o que quer dizer *tipo*. Já agora, que tipos existem?

```python
vinhos['tipo'].unique()

array(['branco', 'tinto', nan, 'rosé'], dtype=object)
```

Antes que fiquem preocupados, não inventámos um tipo novo de vinho.

*nan* significa *not a number*, mas poderia significar *missing value*, a coisa mais assustadora que existe em *data science*, a falta de dados que nos pode impedir de trabalhar. Se a variável fosse numérica, como o preço...

```python
vinhos['grau'].unique()

array([13. , 14.5, 13.5, 14. , 12. , 12.5, 20. , 40. ,  0. , 15. , 15.5,
       16.5, 13.3, 11.5, 10.5, 11. , 19.5, 20.5, 17.5, 18. , 38.5, 49. ,
       16. , 14.3, 38. , 39.5,  9. ,  9.5, 14.8,  8.5, 55.8, 17. , 19. ,
       10. , 21. ])
```
seria importante lembrar que *nan* é um valor em falta e não é mesma coisa que *0.*.

Neste caso quer dizer que houve um erro no processo de importação ou registo, por exemplo, uma vez que não existem vinhos com graduação *0.*.

Mais tarde, iremos abordar técnicas para remediar a ocorrência de valores em falta.

Mas quantos vinhos há de cada tipo?

```python
vinhos['tipo'].value_counts()

tinto     1129
branco     897
rosé       122
Name: tipo, dtype: int64
```
O **rosé** está cada vez mais na moda, mas ainda com uma certa distância.
