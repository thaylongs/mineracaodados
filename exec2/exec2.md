
Mineração de Dados - UFT
===================

Gerenciamento de Dados,  Exercício - 2
-------------

Gerenciamento de dados envolve a tomada de decisões sobre os dados. O livro de códigos e a frequência de distribuição são um excelente guia para a tomada de decisões. Há várias etapas comumente consideradas ao conduzir o gerenciamento de dados. As vezes você precisa considerar apenas um subconjunto delas. Pode até ser que suas variáveis já estejam adequadas e nenhum gerenciamento de dados seja necessário. As outros casos não, imagine uma base de dados  que tem  diveros dados de área em centimetro,  e a partir desses dados vc que calcular o volume em metros cúbicos, nesse tipo de situação é necessário um gerencimento dos dados para poder mudar a unidade de medida de cm^2 -> m^3 .
### Exercícios
#### *Quantidade de madeira correspondente a uma árvore em metros cúbicos*
A base de dados utilazada foi a savana. Nesse  banco, existem duas variáveis, o  *Diam_cm* e *H_com_m*. O  *Diam_cm* é uma variável quantitativa que corresponde ao diâmetro em centímetro do tronco da árvore. *H_com_m* é uma variável quantitativa que corresponde a altura do tronco da árvore em metros.

Para calcular o volume de um cilidro usamos a seguinte formula:
```
VOLUME = 3.14 * raio^2 * altura
```

Como a váriável *Diam_cm* está em centímetro, e queremos calcular o volume me metros cúbicos, devemos transformar essa variável para metrose iremos chamala de *Diam_m*. E como para calcular o volume precisamos do raio, deveremos dividir a variável *Diam_m* por 2 e atribuido esse valor a variável *Raio_m* . Assim demos o seguinte código do SAS.

```sas
LIBNAME mydata "/folders/myfolders" access=readonly;
data new; set mydata.savana;
Diam_m = Diam_cm/100;
Raio_m = Diam_m/2;
VOLUME = 3.14 * (Raio_m * Raio_m) * H_com_m;
PROC SORT; PROC PRINT; VAR Raio_m H_com_m VOLUME;
RUN;
```

Rodando esse código, foi possível obter o seguinte resutado: [Resultado.html ](https://htmlpreview.github.io/?https://github.com/thaylongs/mineracaodados/blob/master/exec2/resultados.html). Onde cada linha linha rem o volume de cada árvore presente no banco de dados.
