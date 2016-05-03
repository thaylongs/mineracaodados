


Mineração de Dados - UFT
===================

Introdução ao programa SAS,  Exercício - 1 
-------------

Nesse exercício será utilizada uma base de dados de espécies de peixes do rio Tocantins, chamado de  “Lajeado”. Esse execício consiste em responder as seguintes perguntas: 

> - Como é a distribuição de peixes de Lajeado? 
> - Existe uma diversidade muito grande de espécies?
> - Existem espécies que dominam o cenário? 
> - Existem espécies que indicam uma ameaça de extinção?

#### **Como  é a distribuição de peixes de Lajeado?**
Para resolver essa questão, oi utilizado o seguinte script:

```sas
LIBNAME mydata "/courses/df47fa15ba27fe300" access=readonly;
DATA new; set mydata.lajeado;
LABEL especie="Espécies de Peixe";
PROC SORT; by especie;
PROC  FREQ;  TABLES especie;
RUN;
```
Esse script  produziu a seguinte saída: [Resultado.html ](https://htmlpreview.github.io/?https://github.com/thaylongs/mineracaodados/blob/master/Exec1-Peixes.html) . Fazendo uma análise da tabela de resultados, pode se observar que a distribuição dos peixes é desigual.

#### **Existe uma diversidade muito grande de espécies?**
Possui uma grande diversidade, com 335 especies diferentes.
#### **Existem espécies que dominam o cenário?** 

Sim, sendo as 9 mais numerosas listados na tabela abaixo, onde juntos representam mais de 39 % da população;

<table class="tg">
  <tr>
    <th  colspan="5">Espécies de Peixe</th>  </tr>
  <tr>
    <td >especie</td>
    <td >Frequency</td>
    <td >Percent</td>
    <td >Cumulative Frequency</td>
    <td >Cumulative Percent</td>
  </tr>

  <tr>
    <td >A.nuchalis</td>
    <td >22019</td>
    <td >7.10</td>
    <td >22019</td>
    <td >7.10</td>
  </tr>
  <tr>
    <td >L.batesii</td>
    <td >19173</td>
    <td >6.18</td>
    <td >41192</td>
    <td >13.27</td>
  </tr>
  <tr>
    <td >M.dichrour</td>
    <td >14025</td>
    <td >4.52</td>
    <td >55217</td>
    <td >17.79</td>
  </tr>
  <tr>
    <td >M.loweae</td>
    <td >13489</td>
    <td >4.35</td>
    <td >68706</td>
    <td >22.14</td>
  </tr>
  <tr>
    <td >H.microlep</td>
    <td >12939</td>
    <td >4.17</td>
    <td >81645</td>
    <td >26.31</td>
  </tr>
  <tr>
    <td >H.unimacul</td>
    <td >12044</td>
    <td >3.88</td>
    <td >93689</td>
    <td >30.19</td>
  </tr>
  <tr>
    <td >R.vulpinus</td>
    <td >10991</td>
    <td >3.54</td>
    <td >104680</td>
    <td >33.73</td>
  </tr>
  <tr>
    <td >P.amazonic</td>
    <td >10103</td>
    <td >3.26</td>
    <td >114783</td>
    <td >36.99</td>
  </tr>
  <tr>
    <td >P.squamosi</td>
    <td >8315</td>
    <td >2.68</td>
    <td >123098</td>
    <td >39.67</td>
  </tr>
</table>

#### **Existem espécies que indicam uma ameaça de extinção?**

Sim, existem diversas espécies ameaçadas de extinção, a maioria dessas espécias foram contabilizados no máximo 10 indivíduos da população total que é mais de 100 mil. 
