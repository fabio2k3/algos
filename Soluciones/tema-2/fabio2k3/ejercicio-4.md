# Solución ejercicio 4

## Inciso A

Un sistema de independencia debe cumplir dos propiedades:

1. El conjunto vacío pertenece a la familia de independientes, ya que no contiende intervalos que puedan solparse

2. Si B es un conjunto independiente, cualquier subconjunto A ⊆ B también es independiente, porque eliminar intervalos no puede crear solapamientos.

Por lo tanto, se cumplen ambas propiedads y los intervalos forman un sistema de inpendencia

Ahora demostremos que no es un matroide.

Un matroide debe cumplir además la propiedad de intercambio

Si A, B ∈ I , y |A| < |B|, debe existir algún elemento q ∈ B \ A, tal que: A U {q} ∈ I

Vamos a construir un contraejemplo:

A = {[1,5)}  y  B = {[0,2), [4,6)}

Podemos observar que A es independiente porque tiene un solo intervalo, B es independiente porque sus intervalos no se solapan.

|A| = 1 < 2 = |B|
Sin embargo el intervalo [1,5) se solapa con ambos intervalos de B:

[1,5) ∩ [0,2) != VACÍO
[1,5) ∩ [4,6) != VACÍO  

Por lo tanto no podemos agregar ninguno de los elementos de B \ A a A sin perder independencia

Por es un sistema de independencia pero no es un matroide ya que no cumple la propiedad de intercambio.


## Inciso B

Teorema:
-------- 
Si un sistema de independencia no es un matroide, existe una función de pesos no negativos para la cual el algoritmo goloso que selecciona los elementos por peso decreciente no obtiene un independiente de peso máximo.

Sin embargo el problema de selección de intervalos sin pesos busca maximizar la cantidad de intervalos seleccionados, no maximizar la suma de pesos.

La regla de tomar el intervalo que termina primero utiliza un criterio diferente, selecciona el intervalo que deja la mayor disponibilidad de tiempo para los siguietnes. 

Por lo tanto no existe contradicción, porque el Teorema s refiere a la optimzación por pesos para cualquier función de peso, mientras que el algoritmo de selección de intervalos optimiza la cantidad de intervalos.

=> Los objetivos y los criterios golosos son diferentes.

## Inciso C

Caso 1: falla el goloso por peso
-------

Intervalo                    Peso
-----------------------------------
I1 = [0, 10)                    10
I2 = [0, 5)                      6   
I3 = [5, 10)                     6

El algoritmo goloso por pesos selecciona primero I1 porque tiene mayor peso. Como I1 se solapa con I2 e I3 no puede seleccionar ninguno de ellos.

El resultado es: Cg = 10

Sin emgargo , la solución óptima slecciona I2 e I3 , que no se solapan: C_optimo = 6 + 6 = 12

Por lo tanto 10 < 12, el goloso por peso no obtiene la solución óptima.


Caso 2: falla el goloso que termina primero
-------

Intervalo                      Peso
------------------------------------
I1 = [0, 2)                     1
I2 = [1, 3)                     100  

El algoritmo que selecciona el intervalo que termina primero eleige I1 porque termina en el instante 2. Como ambos intervalos se solapan, descarta I2

Entonces el resultado es: Cg = 1
Sin embargo la solución óptima es seleccionar I2, C_optimo = 100

Por lo tanto 1 < 100, el goloso termina primero tampoco garantiza maximizar el peso total.


## Inciso D:

Para resolver nuestro problema utilizamos programación dinámica siguiendo el principio de optimalidad

Ordenamos los intervalos por tiempo de finalización creciente:

f1 <= f2 <= ... <= fm

Definimos: p(j) = max{i < j tal que fi < sj}

Es decir que p(j) es el índice del último intervalo anterior que no se solapa con el intervalo j, si no existe ninguno entonces definimos p(j) = 0

Sea: OPT(j) el máximo peso total seleccionando entre los primeros j intervalos

Para cada intervalo j tenemos dos posibilidad:

- No seleccioonar el intervalo j. En ese caso el mejor resultado es OPT(j - 1).
- Seleccionar el intervalo j. En ese caso podemos seleccionar los intervalos compartible anteriores, cuyo resultado es OPT(p(j)), sumamos el peso w_j

Por lo tanto la recurrencia sería:

OPT(j) = max{POT(j - 1), w_j + OPT(p(j))}

donde el caso base es: OPT(0) = 0


Ahora demostremos el principio de optimalidad:
----------------------------------------------

Sea S una solución óptima para los primeros j intervalos.

Consideremos estos dos casos:

Caso #1: el intervalo j no pertenece a S
--------

=> S es una solución formada por los primeros (j - 1) intervalos.

Necesariamiente debe ser óptima para ese conjunto. Si no lo fuera existiriía otra solución de mayor peso entre los primeros (j - 1) intervalos que pdoríamos utilizar para mejorar S, contradiciendo su optimalidad. Por lo tanto su peso es: OPT(j - 1)

Caso #2: el intervalo j pertenece a S
--------

Como los intervalos están ordenados por finalización , todos los demás intervalos sleccionados deben pertenecer a los primeros p(j) intervalos. La solución restatne debe ser óptima para ese subproblema, de lo contrario podríamos sustituirla por otra de mayor peso y obtener una solución mejor que S, lo cual contradice su optimalidad.

Por lo tanto el peso de esta solución es: w_j + OPT(p(j))

como estos dos son los únicos posibles casos, la solución óptima es el máximo de ambos: OPT(j) = max{POT(j - 1), w_j + OPT(p(j))}


Costo del algoritmo:
--------------------

1. ordenar los intervalos por finalización => O(nlon)
2. Calcular cada p(j) mediante búsqueda binaria => O(nlogn) en total.
3. Llenar la tabla de programación dinámica cuestra O(n), ya que cada estado requiere una operación constante.

Por lo tanto el costo total es => O(nlogn)

el espacio utilizado es O(n)

=> el peso máximo obtenido es: OPT(n)