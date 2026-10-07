# Solución ejercicio 1:

Partamos que f pertenece a Θ(g) si existe c1, c2 y n0 tal que f >= c1*g(n) y f <= c2*g(n) para todo n >= n0

Como Θ solo nos dice cómo crece el costo, no su valor exacto, vamos a modelarlo como c*g(n) operaciones

En nuestro caso como tenemos una máquina que es mil veces más rápida que la original, entonces esto implica que si la vieja hace c*g(n) operaciones la otra hará 1000*c*g(n) que es todo lo que le cabe en la hora es decir es igual a c*g(n').

Por lo tanto tenemos que: c*g(n') = 1000*c*g(n) 
                            g(n') = 1000*g(n)

Las máquinas hacen T operaciones por hora, en la vieja c*g(n) = T donde n es el tamaño máximo, y en la rápida como es 1000 veces más rápida será 1000 * T y aquí viene nuestro objetivo de encontrar n' que es el nuevo máximo.

Ahora vamos a analizar cada caso del ejercicio:

# Caso 1: Θ(n^2)

Como ya vimos anteriormente g(n') = 1000*g(n), solo nos queda sustituir cada variable:   g(n') = (n')^2
                                                                                        g(n) = n^2

=> (n')^2 = 1000*(n^2)
    n' = sqrt(1000) * n
    n'/n = sqrt(1000)  [sqrt(1000) es aproximadamente 31.6]
    n'/n es aproximadamente 31.6

Por lo tanto el tamaño se multiplica unas 31.6 veces, es decir una máquina mil veces más rápida el tamaño se multiplica por casi 32, sin importar cuál era n.

# Caso 2: Θ(n*logn)

Aquí tenemos que g(n) = n*logn y g(n') = (n')*log(n')

No podemos despejar n' ya que aprece normal como n' y dentro del logaritmo por lo que aplicaremos una sustitucion n' = k*n, donde k es el factor que buscamos.

=>  k*n*log(k*n) = 1000*n*log(n)  / dividmos por n
    k*log(k*n) = 1000*log(n)
    k(log(k) + log(n)) = 1000 * log(n) / dividimos por log n
    k*(log(k)/log(n) + 1) = 1000

Como podemos observar no podemos aislar k, pero es una ecuación que tiene solución, así que podemos probar valores.

log(k)/log(n) + 1 > 1 , por lo que k tiene que ser menor que 1000



