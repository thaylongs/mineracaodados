
Mineração de Dados - UFT
===================

Gráficos Bivariados,  Exercício - 3
-------------

Para responder a pergunta: Como é que vamos examinar a associação entre duas variáveis graficamente? Iniciamos fazendo uma outra pergunta referente ao tipo de variável de resposta, ou seja, qual é o tipo da variável resposta? É categórica ou quantitativa? Lembrando que usaremos de exemplo a seguinte questão de pesquisa: se a altura de espécies de árvores são dependentes da distância de corpos d'água?. Para a nossa questão de pesquisa da amostra, a variável de resposta ou dependente, é a altura da espécie de árvore, que é quantitativa.

A variável quantitativa é muito interessante de trabalhar pois podemos transformá-la em categórica, fazendo agrupamentos.Para converter uma variável quantitativa em uma variável categórica, começamos por verificar a tabela de frequência da variável explicativa. Por exemplo, vamos pegar a variável dist_agua que é uma variável quantitativa e vamos transformá-la em uma variável categórica, para tentar relacionar se a distância da árvore de corpos d'água tem relação com a circunferência ou com a altura da árvore. Usaremos o procedimento PROC FREQ para examinar essa variável, dist_agua. O código do SAS  é esse abaixo:

```sas
LIBNAME mydata "/folders/myfolders" access=readonly;
DATA new; set mydata.savana;
PROC FREQ; TABLE DIST_AGUA;
```
Aplicando tal formula, é  possível obter o seguinte tabela de frequência:

| Dist_Agua | Frequency | Percent | CumulativeFrequency | CumulativePercent |
|:---------:|:---------:|:-------:|:-------------------:|:-----------------:|
|     50    |    578    |   8.50  |         578         |        8.50       |
|    100    |    360    |   5.29  |         938         |       13.79       |
|    200    |    1151   |  16.92  |         2089        |       30.71       |
|    300    |    857    |  12.60  |         2946        |       43.30       |
|    400    |    1429   |  21.01  |         4375        |       64.31       |
|    500    |    1243   |  18.27  |         5618        |       82.58       |
|    600    |    323    |   4.75  |         5941        |       87.33       |
|    700    |    243    |   3.57  |         6184        |       90.90       |
|    1000   |    402    |   5.91  |         6586        |       96.81       |
|    1400   |     71    |   1.04  |         6657        |       97.85       |
|    1500   |    146    |   2.15  |         6803        |       100.00      |

Podemos observar que a percentagem de distribuição de dividir em grupos mais ou menos equivalentes. Então vamos dividir em três grupos, para demonstração. Até 200m é um grupo, entre 300 e 400m é outro grupo, e acima de 500m é outro grupo. Bem, agora já temos nossa variável explicativa categorizada (porém, relacionadas entre si), impositiva causal para explicar a altura das árvores. Então, vamos gerenciar, agora, a nossa variável de resposta, *h_tot_m*, altura da árvore, variável quantitativa. Vamos tentar categorizar está variável em binária (conforme sugerimos para a variável de resposta na visualização do gráfico de barras), árvores grandes e pequenas. Para isso, vou usar o procedimento *PROC UNIVARIATE* que fornece informações sobre a média aritmética, que será meu corte, dividindo nosso conjunto de dados em dois, árvores grandes e pequenas. Para fazer isso usaremos o seguinte  código no SAS:
```sas
LIBNAME mydata "/folders/myfolders" access=readonly;
DATA new; set mydata.savana;
IF DIST_AGUA LE 200 THEN PACKDISTAGUA = 1;
ELSE IF DIST_AGUA LE 400 THEN PACKDISTAGUA = 2;
ELSE PACKDISTAGUA = 3;
PROC UNIVARIATE; VAR h_tot_m;
```
Esse *script* produziu a seguinte saída: Esse script produziu a seguinte saída: [Resultado.html](https://htmlpreview.github.io/?https://github.com/thaylongs/mineracaodados/blob/master/exec3/result.html). 

Podemos observar que a média aritmética é aproximadamente 6. Então vamos agrupar a altura utilizando o seguinte comando SAS.

```sas
LIBNAME mydata "/folders/myfolders" access=readonly;
DATA new; set mydata.savana;
IF DIST_AGUA LE 200 THEN PACKDISTAGUA = 1;
ELSE IF DIST_AGUA LE 400 THEN PACKDISTAGUA = 2;
ELSE PACKDISTAGUA = 3;
IF h_tot_m LE 6 then PACKHTOT = 0;
ELSE PACKHTOT = 1;
PROC gCHART; VBAR packdistagua/DISCRETE TYPE=MEAN SUMVAR=packhtot;
```
Assim, gerando o seguinte gráfico:
![](https://github.com/thaylongs/mineracaodados/blob/master/exec3/graph1.png)


O gráfico mostra realmente uma relação entre altura das árvores e a distância das árvores até o corpo d'água. Podemos constatar que quanto menor a distância do corpo d'água, maior a altura da árvore. Usando a mesma lógica, é possível verificar se existe uma relação entre a distância da árvore ao corpo d'água e a circunferência do tronco da árvore, com os seguintes comando SAS.
```sas
LIBNAME mydata "/courses/df47fa15ba27fe300" access=readonly;
DATA new; set mydata.savana;
IF DIST_AGUA LE 200 THEN PACKDISTAGUA = 1;
ELSE IF DIST_AGUA LE 400 THEN PACKDISTAGUA = 2;
ELSE PACKDISTAGUA = 3;
IF circ_cm LE 37 then PACKCIRCCM = 0;
ELSE PACKCIRCCM = 1;
PROC GCHART; Vbar packdistagua/Discrete TYPE=MEAN sumvar=packcirccm;
```

Assim, gerando o seguinte gráfico:
![](https://github.com/thaylongs/mineracaodados/blob/master/exec3/graph2.png)


Entretanto, é possível observar que não existe uma relação entre a distância das árvores aos seus corpos d'água e a circunferência do tronco da árvore. Uma outra forma de visualizar o dados é através de um gráfico de dispersão. Para isso precisamos de duas variáveis quantitativas. Então, tentar relacionar a altura das árvores e a distância das árvores até o corpo d'água, porém, agora, sem categorizar as duas variáveis, apenas com os dados brutos. Para isso utiliza-se do seguinte código no SAS:

```sas
LIBNAME mydata "/courses/df47fa15ba27fe300" access=readonly;
DATA new; set mydata.savana;
PROC GPLOT; plot h_tot_m*dist_agua;
```
Desta forma, termos o seguinte gráfico de dispersão:
![](https://github.com/thaylongs/mineracaodados/blob/master/exec3/graph3.png)

Nesse gráfico ainda não ficou clara a relação entre a altura das árvores e sua distância aos corpos d'água. O agrupamento no gráfico de barras demonstrou mais nitidamente esta relação. Vamos testar a relação entre a altura da copa da árvore e a altura da árvore.  Utilizamos o seguinte comando do SAS:

```sas
LIBNAME mydata "/courses/df47fa15ba27fe300" access=readonly;
DATA new; set mydata.savana;
PROC GPLOT; plot h_tot_m*H_galha_m;
```
![](https://github.com/thaylongs/mineracaodados/blob/master/exec3/graph4.png)

Como pode ser observado, não há uma relação muito forte entre a altura da copa da árvore e a altura da árvore. Vamos construir, agora, esse mesmo gráfico de dispersão com bolhas. As bolhas fazem uma terceira dimensão para um melhor entendimento dos gráficos de dispersão, pois, assim, podemos observar melhor a relação do tamanho das bolhas. Utilizamos o seguinte comando SAS:
```sas
LIBNAME mydata "/courses/df47fa15ba27fe300" access=readonly;
DATA new; set mydata.savana;
C_D = H_TOT_M + H_GALHA_M;
PROC GPLOT; BUBBLE H_TOT_M*h_galha_m=c_d / bfill=solid bcolor=vibg BLABEL bsize=50;
```

![](https://github.com/thaylongs/mineracaodados/blob/master/exec3/graph5.png)

Um outro exemplo seria relacionar a altitude com distância de corpos d'água. Utilizamos o seguinte comando SAS:
```sas
LIBNAME mydata "/courses/df47fa15ba27fe300" access=readonly;
DATA new; set mydata.savana;
c_d = dist_agua + cotafisico;
PROC GPLOT; BUBBLE COTAFISICO*DIST_AGUA=c_d / bfill=solid bcolor=vibg BLABEL bsize=80;
```
Resultado:
![](https://github.com/thaylongs/mineracaodados/blob/master/exec3/graph6.png)

Como pode ser observado, há um vazio na parte superior direita do gráfico, ou seja, em grandes altitudes, não foram encontradas espécies de árvores longe de corpos d'água.
