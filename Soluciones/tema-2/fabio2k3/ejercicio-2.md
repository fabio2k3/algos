# Solución ejercicio 2

Utilizareoms la recurrencia del árbol binario de búsqueda óptimo

c(i,j) = w(i,j) + min(c(i, k - 1) + c(k,j))

donde:
- c(i,j): costo mínimo del árbol que contiene las claves i + 1, ..., j
- w(i,j) = fi+1 + ... +fj : suma de sus frecuencias
c(i,i) = 0 para el árbol vacío

## Inciso A
### Encontrar frecuencias para las que cada regla no obtiene el óptimo

Regla 1: elegir la calve más buscada.
--------

Consideremos las sigueintes frecuencias:  f = (1, 2, 3, 4, 5)

Todas son distintas, por lo que no existen empates

Aplicando la regla golosa, elegimos sucesivamente la calve con mayor frecuencia:

Raíz: clave 5
Subárbol izquierdo: clave 4
Subárbol izquierdo: clave 3
Subárbol izquierdo: clave 2
Finalmente: clave 1

Así obtenemos un árbol degenerado
Costo del árbol goloso mediante la recurrencia

cg(1,1) = 1
cg(1,2) = 3 + 1 = 4
cg(1,3) = 6 + 4 = 10
cg(1,4) = 10 + 1= = 20
cg(1,5) = 15 + 20 = 35

Por lo tatno Cg  = 35


Costo del árbol óptimo: elegimos como raíz la calve 4, el subárbol izquierdo contiene las calves 1,2 y 3, y el derecho contiene la calve 5.

Aplicando la recurrencia:

c(0,3) = 6 + 4 = 10
c(4,5) = 5

c(0,5) = 15 + 10 + 5

por lo tanto Coptimo = 30

 -------
|35 > 30| 
 -------

La regla de elegir siempre la calve más buscada no garantiza obtener el árbol óptimo.

Regla 2: elegir la calve que deja más liviano el más pesado de sus dos subárboles
-------

f = (1, 2, 3, 4, 5)

Todas las frecuencias son distintas. Para elegir la raíz, calculamos el máximo entre la suma de las frecuencias del subárbol izquierdo y del derecho

Raíz candidate     Peso izquierdo          Peso derecho       Máximo
---------------------------------------------------------------------
1                   0                       14                 14
2                   1                       12                 12  
3                   3                       8                   8
4                   7                       5                   7
5                   10                      0                  10

La regla elige la calve 4 como raíz

Aplicamos recursivamente la misma regla:

- Subárbol izqueirdo: elige 3
- Siguiente sunárbol: elige 2
- La clave 1 queda como hijo iquierdo de la calve 2
- La clave 5 queda como hijo derecho de la raíz

Costo del árbol goloso mediante la recurrencia:

cg(1,1) = 1
cg(1,2) = 3 + 1 = 4
cg(1,3) = 7 + 4 = 11

como la raíz es la clave 4:  cg(0,5) = 15 + 11 + 5 = 31

=> Cg = 31

Costo del árbol óptimo:
Elegimos como raíz la clave 3. El subárbol izquierdo contiene las claves 1 y 2, mientras que el derecho contiene las claves 4 y 5.

Aplicando la recurrencia:

c(0,2) = 3 + 1 = 4
c(3, 5) = 8 + 3 = 11
c(0, 5) = 15 + 4 + 11

por ende Cóptimo = 30

-----------
| 31 > 30 |
-----------

La segunda regla golosa tampoco garantiza obtener el árbol óptimo

## Inciso B 
### Intentar un argumento de inercambio para la regla(i)

Supongamos que tenemos un árbol binario de búsqueda óptimo cuya raíz es una clave k, y que existe otra clave x con la mayor frecuencia de búsqueda.

Queremos intercambiar la raíz k con la clave x de manera que x pase a ser raíz. En el argumento de intercambio, se transforma una solución óptima en otra que conserva la factibilidad y cuyo costo no aumenta.

Sin embargo, aquí tenemos un problema:
Intercambiar directamente la raíz con una clave arbitraria no garantiza que el árbol resultante siga siendo un árbol binario de búsqueda válido. Esto se debe a que deben mantenerse las siguientes propiedades:

- Todas las calves menores que la raíz deben estar en el subarbol izqueirdo
- Todas las claves mayores que la raíz deben estar en el subárbol derecho

Al intercambiar las claves, estas condiciones pueden dejar de cumplirse. Por lo tamto no podemos garantizar que el árbol obtenido después del intercambio sea una solución factible.

No se puede garantizar que el intercambio preserve la propiedad de árbol binario de búsqueda