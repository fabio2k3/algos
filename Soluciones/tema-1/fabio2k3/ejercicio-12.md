# Solución Ejercicio 12 ( Gale Shapley)

Tenemos n proponentes y n receptores. Cada proponente a tiene una lista estricta e incompleta L(a) de receptores, de mejor a peor, y prefiere quedarse solo antes que con uno que listó

Vamos a definir nuestro emparejamiento M:
Cada proponenete queda solo o con un receptor de L(a) y cada receptor tiene a lo sumo un proponente. Ya no tiene por qué ser perfecto.

Un par (a,b) con M(a) != b es bloqueante si:
. b pertenece a L(a)
. a prefiere b a su situación en M, es decir está solo o ranquea b por encima de M(a)
. b prefiere a  a su situación, está solo o ranquea a por encima de M(b)

m es estable si no tienen pares bloqueantes. La 1ra condición es lo que cambia => un receptor que a no listó nunca puede bloquear con a, porque a prefiere quedarse solo.

DEfinamos nuestro algoritmo (adaptado)
---------------------------------------

Cada proponente a mantiene siguiente[a], el lugar de L(a) al que va a proponer:

Mientras haya un porponente libre a:

- Si siguiente[a] = !L(a)!, la lista se agotó y a se queda solo, es decir sale del juego.
- Si no, a le propone a b = L(a)[siguiente[a]] y avanza siguiente[a]. Si b está libre, acepta. Si ya tiene pareja y prefiere a a, lo acepta y su pareja anterior queda libre, si no rechaza a a.

Terminación:
------------

Q = Σ (|L(a)| - siguiente[a]), el número de propuestas posibles que aún no se hicieron.

Empieza en m = Σ|L(a)| <= n^2, es un entero >= 0, y cada propuesta lo baja exactamente en 1, porque sigueinte[a] solo avanza no se repite ninguna.

Descartar a un proponente de lista agotada no cambia Q, pero un descartado nunca vuelve a quedar libre y eso ocurre a lo sumo n veces.

=> Hay a lo sumo m propuestas y n descartes, el ciclo termina

