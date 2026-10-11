# Solución Ejercicio 10

Tenemos que demostrar que: El par más cercano en una dimensión requiere Ω(nlogn) en árboles de decisión algebraicos.

Lo haremos por reducción desde distinción de elementos, dados n reales decidir si hay dos iguales, que por el teorema de Ben-Or requiere Ω(nlogn) en este modelo

=> Sea un árbol A que resuelve el par más cercano con profundidad T(n). Una entrada de distinción de elementos x1, x2, ..., xn ya es una entrada válida de par más cercano en la recta, así que la ejecutamos directamente en A.
Cada Hoja de A devuelve un par (i,j) y a le añadimos un nodo que pruebe el signo de xi - xj, si es 0, hay repetidos y si no, todos son distintos

Si hay valores iguales, la distancia mínima es 0, por lo que el par devuelto cumple xi = xj. Si todos son disitntos, todo par tiene una distancia positiva, incluido el devuelto, por ende es Correcto.

El árbol resultatne resuelve distinción de elementos con profundidad T(n) + 1, que por teorema visto anteriormente esta profundidad es Ω(nlogn).

Por lo tanto T(n) = Ω(nlogn)