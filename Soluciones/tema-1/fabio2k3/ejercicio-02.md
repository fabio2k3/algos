# Solución ejercicio 2:

Tenemos el problema de búsqueda binaria que es: Dado un arreglo Q con sus elementos ordenados y un valor x, devolvemos el índice donde se encuentra x en Q o devolvemos -1 en caso de que x no se encuentre en Q

Código de Nuestro Algoritmo:
----------------------------

def busqueda_binaria(Q, x):
    l = 0
    r = len(Q) - 1

    while l <= r:
        m = (l + r) // 2

        if Q[m] == x:
            return m

        elif Q[m] < x:
            l = m + 1

        else:
            r = m - 1

    return -1


Analicemos ahora su invariante:
--------------------------------

Antes de cada vuelta de nuestro ciclo se que cumple que: todo i < l cumple que Q[i] < x, y todo i > r cumple que Q[i] > x. Esto quiere decir en pocas palabras que todo lo que esté fuera de nuestro rango [l,r] no puede contener al valor que estamos buscando, es decir, x.

Al iniciar el algoritmo tenemos que l = 0 y que r = n - 1 (donde n es el tamaño de nuestro arreglo Q), así que nuestra condición que vimos anteriormente se cumple.

Luego al iniciar el ciclo vamos a suponer que nuestra condición se cumple, pero en este caso Q[m] != x (l <= r), pueden ocurrir dos situaciones distintas:

1- Q[m] < x => como el arreglo está ordenado entonces podemos afirmar que: todo i <= m cumple que Q[i] <= Q[m] < x, luego con el  nuevo l = m + 1, todo i < l cumple qué Q[i] < x. La parte derecha no cambia.

2- Caso opuesto Q[m] > x => es exactamente lo mismo pero en otro sentido i >= m cumple que Q[i] >= Q[m] > x, entonces con el nuevo r = m - 1, todo i> m cumple Q[i] > x, por lo tanto se sigue cumple la condición que planteamos al inicio.

Por lo tanto podemos decir que el ciclo termina de dos formas: la primera es con A[m] = x, donde devuelve el indíce m, y la segunda es con l > r donde todo índice i cumple que i > m o i < l, así que ningún valor del arreglo vale x por ende nuestro algoritmo devuelve -1

