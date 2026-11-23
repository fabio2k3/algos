# Ejercicio 5 solución

Sea M el emparejamiento obtenido por Dinic depués de algunas fases y sea M* un emparejamiento máximo

## Inciso A

Después de la primera fase, Dinic ha encontrado un flujo bloqueante en la red de niveles. Por lo tatno ya no existe ningún camino de aumento de longitud mínima. 

En la red bipartita los camino de aumento de longitud 1 corresponden a aristas que conectan dos vértices libres. Como la primera fase encuentra todos los caminos de aumento de longitud mínima, no puede quedar ninguna arista cuyos dos extremos estés libres

Por lo tanto M es maximal.

Sea M* un emparejamiento máximo, CAda arista de M* debe compartir al menos un extremo con alguna arista de M, pues M es maximal, además cada arista de M puede compartir extremos con dos aristas de M* como máximo

Por ende:

|M*| <= 2|M|

=> |M| >= 1/2 * |M*|

Dinic garantiza después de la primera fase al menos la mitad del emparejamiento máximo.

Esto coincide con la garantía del algoritmo goloso. El goloso también garantiza una solución de tamaño al menos mitad del óptimo.

## Inciso b

Sea j el número de aristas de M en un camino de aumento más corto. Por tanto, dicho camino contiene j + 1 aristas que no pertenecen a M.

Consideramos la descomposición de M △ M* en caminos y ciclos alternantes. 
Los caminos de aumento son las componentes que permites que M* tenga más aristas que M. Cada uno de estos caminos contiene al menos j aristas de M, pues j es el número de aristas de M en un camino más corto.

Sea q el número de componenetes de aumento de la descomposición. Como son disjuntas, cada una contiene al menos j aristas de M y por lo tanto:

q <= |M| / j

La diferencia entre los tamaños de los emparejamientos está acotado por el número de componentes de aumento:

|M*| <= |M| + q

sustituyendo q:

|M*| <= |M| + |M|/j

|M*| <= |M|* (1 + 1/j)

=> M >= j/(j + 1) * |M*|

## Inciso C

Por el lema que plantea: la distnacia de s a t en la red residual aumenta al menos en 1 después de cada fase

En la red bipartita , las distancias de los caminos de aumento tienen paridad fija, son impares. Por lo tanto cada vez que la distancia aumenta , aumenta al menos en 2

Inicialmente, la distancia es al menos 1, después de p fases:

d(s,t) >= 2p + 1

Un camino de aumento de longitud 2j 9 1 contiene j aristas del emparejamiento actual, por ende:

2j + 1 >= 2p + 1
j >= p

si aplicamos lo ontenido en el inciso anterior (b):

|M| >= j/(j + 1) * |M*| >= p/(p + 1) * |M*|

=> |M| >= p/(p + 1) * |M*|

Por lo tanto después de p fases, Dinic garantiza al menos: p/(p+1) del emparejamiento