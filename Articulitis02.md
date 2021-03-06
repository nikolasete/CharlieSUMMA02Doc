# Articulitis 2
## Stroke Codes in the Region of Madrid during COVID-19 pandemic

### Analysis of second wave

#### Nicolás Riera
##### Proyecto de investigación sobre la influencia de la segunda ola de COVID-19 en la activación de códigos ictus en la región de Madrid

### `r as.character(Sys.Date())`

##### v 2021 01 18. Git Branch "Master"

Introducción
--------------------------------------------
#### SELECCIÓN DE PERÍODOS COVID

Tras revisar la de nuevo la incidencia de COVID-19 bajando los datos de la web de [Datos del Gobierno de España](https://datos.gob.es/es/catalogo/e05070101-evolucion-de-enfermedad-por-el-coronavirus-covid-19) (concretamente el CSV "**Serie histórica de casos por Comunidad Autónoma**"):

 1. Ya que vamos a hablar del SUMMA, no considero los datos de España, sino solo los de la Comunidad de Madrid.

> columna CCAA_ISO = MD

 2. Decido considerar dos series mirando la curva de incidencia de infección por COVID-19, ya que la curva en 2019 tiene dos crestas. `Explicarlo bien en el apartado que sea.`
 3. ¿Primera serie desde el 1 de enero de 2020? A favor es que en la serie hay diagnósticos desde esa fecha. En contra que se solapa con la serie de Gripe. El primer caso "publicado en España" según las noticias se produjo el 31 de enero. `Decido desde 1 de enero.`
 4. Después el primer máximo se produce el 20-3 con 3219 casos. Después el primer mínimo se produce el 27 de junio con 26 casos. Ese sería el primer período y la **mediana es de 111 casos**. Y por tanto el período con una frecuencia diaria superior a la media sería **del 28/02 al 2/05**, teniendo en cuenta que una semana después hay *otros muchos días con casos superiores a la mediana (hasta el 15/06)*. Si consideramos el período "estrecho" son 65 días y si consideramos el periodo ancho son 109 días. Si consideramos el primer período el primer semestre del año, la mediana es de 124 y no cambia nada). `Explicar que mirando la curva casi es por semestres.`
 5. La segunda oleada comenzaría el día siguiente 28/06 con 29 casos, hasta el máximo del 18/9 con 6.743 casos y hasta el mínimo del 5/12 con 735 casos. La **mediana del segundo período sería 1477 casos** y por tanto el período con una frecuencia superior a la mediana sería del 10/8 al 11/11 (en este caso incluyendo hasta el último día en que la mediana supera, 94 días). Si consideramos el segundo período como el segundo semestre, la mediana sería de 1.340 y no cambiaría nada, excepto que volvería a salir oleada a partir del 9 de diciembre (comienzo de la tercera oleada).
 6. Entiendo que deberíamos ser "homogéneos" en la selección de los períodos. Osea que el primer período debería ser el "ancho" de 96 días.

> Período 1: del 28/02 al 15/06: 109 días
> Período 2: del 10/08 al 11/11: 94 días

#### SELECCIÓN DE PERÍODOS GRIPE
Los que tenía en el trabajo anterior.
52 días solo (frente a 96 y 106 de los dos períodos COVID).

#### Algunos razonamientos
1. La secuencia temporal más o menos es: infección (d), síntomas (d+5), hospitalización (d+12), UCI (d+20).
2. Lo que vamos a estudiar es la incidencia de códigos ictus en extrahospitalaria. Nuestra sobrecarga es como unos días después del aumento de la detección de síntomas. Pero no una semana y pico después (cuando se produce la sobrecarga hospitalaria y sería más probable que se afectase la atención al ictus agudo).
3. Por ello es mejor trabajar con márgenes amplios. Quizás con un percentil 75 podría valer: 

> Primera Oleada COVID 19: 04/03 a 22/04 (50 d)
> Segunda Oleada COVID 19: 18/08 a 09/10 (53 d)
4. En fin. No sería congruente usar el percentil 75 en COVID-19 y el 50 en Gripe, excepto que expliquemos que como la gripe es de casos centinela, son muchos menos... y quizás tampoco, porque el hecho de que sean casos centinela, la mediana es con respecto a esos pocos casos...

#### PRUEBAS
Con la subrutina de selección de los períodos de tiempo, puedo probar a usar los períodos cortos o los períodos largos:

 - Percentil 50 Gripe, percentil 75 de COVID: n=1213, 285 días a estudio.

    Diferencias significativas en edad durante la primera oleada, en sexo. NO diferencias en número de CI.

- Percentil 50 de todo: n=2083, 484 días a estudio.


|  |Percentil 75|Percentil 50|
|--|--|--|
|Días|50 - 53|109 - 94|
|n|1213|2083|
|Percentil Gripe|No|Si|
|__Número de CI diarios__
|ANOVA  |Influenza vs 2 Waves & Precovid  | =
|Kruskal  |= |=
|__Sexo__| **2 Waves: Invierten proporción**| =
|CHI2  | 1Wave frente a Influenza y a Precovid. Más % Hombres | No DIF, Ajuste Bonferroni
|__Edad__
|ANOVA  | 2Wave frente a Influenza y a Precovid | Influenza frente a 2 olas
|Kruskal  | 2Wave frente a Influenza y a Precovid | 1Wave frente a Influenza y Precovid
|__Minutos__
|ANOVA  | 1Wave frente a Precovid | Influenza y 2 olas frente a Precovid
|Kruskal  | 1Wave frente a Precovid | Influenza y 2 olas frente a Precovid

- Parece más sensato usar el percentil 50 ya que tiene más "n" y parece algo más fácil de interpretar los resultados.


#### Missing values
* __Variable Sex__ Faltan seis valores. Sustituyo los "D" de desconocido por datos en blanco, para que "D" no aparezca en la tabla "tableby"
* __Variable Minutos__ Hay 395 datos que faltan. Están en blanco y así no se analizan.
* 

> 
> Written with [StackEdit](https://stackedit.io/).


<!--stackedit_data:
eyJoaXN0b3J5IjpbNjM3MjUzMTg5LDgyOTMzNjEwOSwtMjA1MD
cxNzY5OCwtMTE3NTE5NTQ3NiwxMjA4NzU5MzkyLC00NDE3MDA0
MjEsMTg3OTIzNTQyLC0yMTIyNTU1MzIzLC0xNTM0NDgxNTYyLC
0xNzc3NjY5MDkyLC05NjM5MjM1NzIsNTM3NzIxNjE4LC0yMTEx
MjcyMjMwLDE0MTg3MTg0NTMsMTAzNDExOTU0NiwyMTIxNTQwOT
czLDU2MTg3NjU5OCwtMTk1OTA3MTE2MF19
-->