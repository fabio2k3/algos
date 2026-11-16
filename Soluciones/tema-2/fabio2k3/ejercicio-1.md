# Solución ejercicio 1

## Inciso A

(1 + 2x + 3x^2)(4 + 5x) = 16 + 10x + 23x^2 + 15x^3

Ahora evaluamos ambos lados en r = 4

Lado Izquierdo:
---------------

(1 + 2*4 + 3*(4)^2)(4 + 5*20)

= (1 + 8 + 48)(4 + 20)
= 57 * 24
= 1368

En Z17 se cumple que: 1368 ≡ 8 (mod 17)


Lado derecho:
-------------

6 + 10*4 + 23*(4)^2 + 15*(4)^3
= 6 + 40 + 368 + 960
= 1374

En Z17 1374 ≡ 14 (mod 17)

Por lo tanto como 8 != 14 (mod 17) podemos decir que la afirmación es falsa



## Inciso B

tenemos que encontrar todas las r que pertenecen a Z17 para los que la comprobacion es cierta

Primero desarrollemos el polinomio:
(1 + 2x + 3x^2)(4 + 5x) = 4 + 13x + 22x^2 + 15x^3

Igualamos ambbos polinomios:
4 + 13r + 22r^2 + 15r^3 = 6 + 10r + 23r^2  + 15x^3

r^2 - 3r + 2 = 0  (mod 17)

(r - 1)(r - 2) = 0 (mod 17)

r1 = 1, r2 = 2

Por lo tanto r ∈ {1,2}

Por ende existen dos valores que hacen que la comprobación acepte afirmación. La fracción de valroes que producen una aceptación es incorrecta es: (2 / 17)

La probabilidad de error es:

P(error) <= d / p (donde d es el grado de la diferencia entre los polinomios y p el tamaño del campo).

En nuestro caso d = 2 y p = 17

Por lo tanto P(error) <= 2/17



## Inciso C

Queremos dos polinomios diferentes coincidan en la mayor cantidad posible de valores de Z17.

Sabemos que un polinomio no nulo de grado d tiene como máximo d raíces, como queremos construir un polinomio de grado 3 podemos hacer que la diferencia entre ambos tenga tres raíces distintas

Podemos elegir: r1 = 1, r2 = 2, r3 = 3

Siguiendo esto podemos construir el siguiente polinomio: 

D(x) = (x - 1)(x - 2)(x -3)

donde D(1) = D(2) = D(3) = 0

Ahora construimos un segundo polinomio:

Q2(x) = P(x) + D(x)

Q2(x) = 4 + 13x + 22x^2 + 15x^3 + (x - 1)(x - 2)(x - 3)

Q2(x) = 4 + 13x + 22r^2 + 15x^3 - 6 + 11x - 6x^2 + x^3

Q2(x) = -2 + 24x + 16x^2 + 16x^3

Ahora comprobamos si pasa la comprobación:

P(r) = Q2(r) ???

pero como hicimos a Q2 de tal forma que se cumple:
Q2(x) - P(x) = (x - 1)(x - 2)(x - 3)

ambos coinciden cuando: r ∈ {1,2,3}

Por lo tanto: P(error) <= 3/17

¿Alcanzamos la cota?
--------------------

Aquí aplicamos el lema de Schwartz-Zippel:

P(R(r) = 0) <= d / |S|

donde:
- R es la diferencia entre lo polinomios
- d es el grado
- S conjunto del que elegimos los valores aleatorios

R(x) = Q2(x) - P(x) 
d = 3
|S| = 17

por ende P(error) <= 3 / 17, pero hemos conseguido exactamente tres raíces. Por lo tanto Sí alzancamos la cota máxima

¿Qué afirmaciones falsas sobre los eneros nunca detectaría la comprobación módulo 17?

Al trabajar con Z17 todos los cálculos se realizan módulo 17

ejemplo: 17*x ≡ 0 (mod 17)

Por ende esta afirmación 17*x ≡ 0 es falsa para cualquier entero distinto de 0

## Inciso D

La diferencia entre el producto verdadero y el producto afirmado es:

R(x) = -x^2 + 3x - 2

como el grado es, la probabilidad de error en una ronda es:

P(error) <= 2 / 17

con K rondas independientes, la probabilidad de error queda acotada por:

P(error) <= (2 / 17)^k

queremos que: (2 / 17)^k  < 10^(-6)

aplicando logaritmo obtenemos:

k > log(10^(-6)) / log(2/17)  => k > 6.13

Por lo tanto k = 7 rondas independientes


¿Usan todas las rondas el mismo r?
----------------------------------

Las comprobaciones no son independientes, ya que se evalúan siempre en el mismo punto, si ese valor es una raíz de la diferencia entre los polinomios, todas las rondas aceptarán incorrectamente, por lo tanto la probabilidad de error no disminuye, independientemente del número de rondas.