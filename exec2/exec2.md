
Mineração de Dados - UFT
===================

Gerenciamento de Dados,  Exercício - 2
-------------

Gerenciamento de dados envolve a tomada de decisões sobre os dados. As vezes é preciso considerar apenas um subconjunto de uma base de dados. Pode até ser que as variáveis já estejam adequadas e nenhum gerenciamento de dados seja necessário. EM outros casos não, imagine uma base de dados que tem diversos dados de área em centímetro, e a partir desses dados queria calcular o volume em metros cúbicos, nesse tipo de situação é necessário um gerenciamento dos dados para poder mudar a unidade de medida de cm^2 -> m^3 .

### Exercícios
#### *Quantidade de madeira correspondente a uma árvore em metros cúbicos*
A base de dados utilizada foi a savana. Nesse banco, existem duas variáveis, o *Diam_cm* e *H_com_m*. O *Diam_cm* é uma variável quantitativa que corresponde ao diâmetro em centímetro do tronco da árvore. *H_com_m* é uma variável quantitativa que corresponde a altura do tronco da árvore em metros.

Para calcular o volume de um cilindro usamos a seguinte fórmula:
```
VOLUME = 3.14 * raio^2 * altura
```

Como a variável *Diam_cm* está em centímetro, e queremos calcular o volume me metros cúbicos, devemos transformar essa variável para metros e iremos chamá-la de *Diam_m*. Para calcular o volume, precisamos do raio, assim deveremos dividir a variável *Diam_m* por 2 e atribuindo esse valor a variável *Raio_m* . Essa lógia pode ser traduzido no seguinte código do SAS.


```sas
LIBNAME mydata "/folders/myfolders" access=readonly;
data new; set mydata.savana;
Diam_m = Diam_cm/100;
Raio_m = Diam_m/2;
VOLUME = 3.14 * (Raio_m * Raio_m) * H_com_m;
PROC SORT; PROC PRINT; VAR Raio_m H_com_m VOLUME;
RUN;
```

Rodando esse código, foi possível obter o seguinte resultado: [Resultado.html ](https://htmlpreview.github.io/?https://github.com/thaylongs/mineracaodados/blob/master/exec2/resultados.html). Onde cada linha linha rem o volume de cada árvore presente no banco de dados.

#### *Agrupar Resultados*
Existem situação que foi feita uma pesquisa onde os questionários eram quantitativos, entretanto é de interesse da pesquisa uma resposta categórica. Imagine a seguinte situação, em um questionários, foi perguntado a distância da caso do entrevistado até o trabalho, em quilômetros. Entretanto é de interesse da pesquisa classificar esse resultado em perto, mediano ou longe. Novamente o Gerenciamento de Dados entre no contexto para poder fazer essa conversão.


Na base savana existe a variável *Dist_Agua* que representa a distância da árvore até o até o riacho mais próximo. Então, queremos transformar essa variável quantitativa em categórica em 3 níveis. Classificando ela em distância pequena (1) quando a distância for menor que 300 metros, distância média quando a distância é menor que 600 metros e distância grande caso a distância é maior que 600 metros. Utilizando o seguinte código SAS é possível obter o resultado classificado:

```sas
LIBNAME mydata "/folders/myfolders" access=readonly;
data new; set mydata.savana;
IF DIST_AGUA LE 300 THEN DIST_AGUA_CAT = 1;
ELSE IF DIST_AGUA LT 600 THEN DIST_AGUA_CAT = 2;
ELSE DIST_AGUA_CAT = 3;
PROC FREQ; TABLES Dist_Agua_CAT;
```
Executando o código é possível obter o seguinte resultado:

| DIST_AGUA_CAT | Frequency | Percent | Cumulative Frequency | Cumulative Percent |
|---------------|-----------|---------|----------------------|--------------------|
| 1             | 2946      | 43.30   | 2946                 | 43.30              |
| 2             | 2672      | 39.28   | 5618                 | 82.58              |
| 3             | 1185      | 17.42   | 6803                 | 100.00             |

#### *Gráficos*
Os gráficos de barras (bar charts) são mais comumente usados para examinar a distribuição das variáveis individuais. Para exemplificar um exemplo, iremos utiizar o resultado catégorio agrupado do exercício anterior. Para isso, utilizaremos o seguinte código:

```sas
LIBNAME mydata "/home/thaylongs0/my_courses/ddnprata0" access=readonly;
data new; set mydata.savana;
IF DIST_AGUA LE 300 THEN DIST_AGUA_CAT = 1;
ELSE IF DIST_AGUA LT 600 THEN DIST_AGUA_CAT = 2;
ELSE DIST_AGUA_CAT = 3;
PROC GCHART; Vbar DIST_AGUA_CAT/Discrete type=PCT width=30;
```

Desta forma é possível obter o seguinte gráfico resultante:

![](https://github.com/thaylongs/mineracaodados/blob/master/exec2/graph1.png)
