# Solución Ejercicio 3

## Inciso A

Vamos a utilizar el algoritmo de Monte carlo M para generar soluciones y el verificador determinista para comprobarlas. Si una solución es incorrecta, repetimos el proceso

por lo tanto nuestro algoritmo sería:
-------------------------------------

Las_Vegas(entrada):
    while:
        x = M(entrada)
        if Verificador(entrada, x) == correcto:
            return x

Ahora demostremos su correctitud:

Por hipótesis el algoritmo Monte Carlo (M) devuelve un objeto correcto con probabilidad al menos p > 0 para cualquier entrada. El verificador es determinista, por lo que siempre identifica correctamente si el objeto generado es válido.

Por lo tatno nuestro algoritmo solamente devuelve un objeto cuando la condicional confirma que es correcto. Esto garantiza que el algoritmo "Las_Vegas" siempre devuelve una solución correcta.

Además como cada ejecución de M tiene una probabilidad de éxito de al menos p, la probabilidad de necesitar más de k ejecuciones está acotada pr:

P(N > k) <= (1 - p)^k

El número esperado de ejecuciones es: E[N] <= Σ(1 - p)^k  (con k desde 0 hasta infito)

Aplicando la suma de la serie geométrica obtenemos que: E[N] <= 1/p

Cada intento cuesta como máximo T + T' porque ejecutamos M y posteriormente el verificador, por lo tanto el tiempo esperado total es:

E[T_total] <= (T + T') / p

La condición que deben cumplir las corridas de M es la siguiente: las ejecuciones deben utlizar monedas aleatorias nuevas e indepenientes. Más precisamente, cada nueva ejecución debe conservar una probabilidad de éxito de al menos p, incluso condicionada a los fallos anteriores. Esto permite utlizar la distribución geométrica para calcular el número esperado de intentos

## Inciso B
### ¿Por qué no se puede aplicar a Freivalds?

El algoritmo de Freivalds permite verificar probabilísticamente si el producto de dos matrices A y B es igual a una amtriz C

Su funcionamiento consiste en generar un vector r y comprobar si: A(B*r) = C*r

Si AB = C, siempre responde sí. 
Sin embargo si AB != C, puede responder incorrectamente que sí con probabilidad de hasta 1/2.

El problema para aplicar el inciso anterior es que no disponemos de un verificador determinista eficiente que compruebe una respuesta afirmativa.

Una respuesta negativa viene acompañada de un vector que sirve como testigo de que los productos son diferentes. En cambio, una respuesta afirmativa no proporciona una garantía de que las matrices son iguales. Para verificarlo determinísticamente tendríamos que calcular el producto compelto AB y comprobarlo con C, lo cual cuesta O(n^3) utilizando multiplicación tradicional.

Por lo tanto aunque podemos realizar la transformación formalmente, el verifivador tendría un costo elevado y perderíamos la ventaja de Freivalds.