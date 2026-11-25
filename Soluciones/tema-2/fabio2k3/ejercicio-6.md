# Ejercicio 6 Solución

Sea E = {1, ..., n}, donde cada tarea i tiene duración t_i >= 1 y plazo di. Un conjunto S ⊆ E es factible si existe un orden en que todas sus tareas terminan a tiempo

## Inciso A

Ordenamos las tareas S por plazo creciente

Por el teorema del retraso máximo, este orden minimiza el retraso máximo, por lo que S es factible <=> todas las tareas terminan a tiempo en dicho orden

Algoritmo
---------

factible(S):
    ordenar S por plazo creciente
    T = 0
    for each tarea_i in S:
        T = T + tarea_i
        if T > d_i:
            return False
    return True

Ordenar cuesta O(n log n) y recorrer las tareas O(n) por lo tanto  T(n) = O(n log n)

## Inciso B

Consideremos la siguiente instancia de tres tareas:

Tarea    |    Duración t_i    |    Plazo d_i
-----------------------------------------------
  1      |        1           |       1  
  2      |        1           |       2  
  3      |        2           |       2  


Tomemeos los conjuntos: A = {3}, B = {1,2}

Ambos son factibles: la tarea 3 termina en el instante 2, y las tareas 1 y 2 terminan en ese orden, terminan en los instatnes 1 y 2

Sin embargo A U {1} = {1, 3}

no es factible pues la tarea 3 termina como mínimo en el instatne 3, superando su plazo 2. Igual con A U {2} = {2, 3} tampoco es factible , pues ambas tareas terminan como mínimo en el instatne 3, superando el plazo de la tarea 2

Por lo tanto |A| < |B|, para todo e que ∈ a B\A, A U {e} ∉ I

se viola la propiedad de intercambio de los matroides, en consecuencia (E, I) no es un matroide

## Inciso C

Como A = {3} B = {1,2} tenemos:

a = |A| = 1,  b = |B| = 2, c = |𝐴 ∩ 𝐵⁠| = 0

Por el teorema visto en el capítulo 10, definimos los peosos como 
 
w(e) =>  |A| + 2 = 3  v ∈ B
        |A| + 1 = 2   v ∈ B\A
        0             en otro caso

por lo tanto: w1 = 2, w2 = 2, w3 = 3

la ejecución del goloso ordena las tareas por peso decreciente:

- Seleciona la tarea 3 , de peso 3, pues factible
- intentea añadir la tarea 1 , de peso 2, pero {1, 3} no es factible, por ende la rechaza
- intentea añadir la tarea 2 , de peso 2, pero {2, 3} no es factible, por ende la rechaza

El goloso devuelve G  = {3}, con peso w(G) = 3, sin embargo , B = {1,2} es factible y su peso es w(B) = w1 + w2 = 2 + 2 = 4

por lo tanto w(G) < w(B) ya qye 3 < 4

el goloso no obtiene un conjunto de peso máximo tal como garantiza la construcción del Teorema

## Inciso d

supongamos que t_i = t > 0 para toda tarea, un conjunto S es factible <=> ordenando sus tareas por plazo crecientem cada tarea i cumple:

t*pos(i) <= d_i, donde pos(i) es su posición en dicho orden.

Definimos el plazo equivalente q_i = ⌊ d_i / t ⌋. 

La factibilidad se reduce entonces al problema de tareas unitarias con plazos q_i, un consjunto S es factible <=> |{i ∈ S: q_i <= k}| para todo k >= 1

Esta es exactamente la caracterización de los conjuntos independientes del matroide de tareas unitaria con plazos. La transformación de los plazos a q_i no cambia la estructura del problema, sino que lo reduce al caso ya demostrado. 

Por lo tanto la propiedad de intercambio se mantiene y si todas las tareas tienen igual duración, los conjuntos factibles forman un matroide
⁠
⁠