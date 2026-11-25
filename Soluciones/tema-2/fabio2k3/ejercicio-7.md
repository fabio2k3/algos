# Solución ejercicio 7

## Inciso a

Consideremos un camino de tres vértices: 

graph LR
    v1((v₁)) --- v2((v₂)) --- v3((v₃))

Tomamos los conjuntos: A = {v2} y B = {v1, v3}

Ambos son independientes y cumplen: |A| = 1 < 2 = |B|

Sin embargo, no existe ningún vértice v ∈ B que pueda añadirse a A manteniendo la independencia ya que vq y v3 son adyacentes a v2. Por lo tanto , falla la propiedad de intercambio, lo que demuestra que el sistema de conjuntos independientes del árbol no constituye un matroide

Construimos los pesos:

w(x) =>  |A| + 2 = 3  v ∈ B
         |A| + 1 = 2  v ∈ B\A
          0           en otro caso

En consecuencia => w(v1) = 2, w(v2) = 3, w(v3) = 2 

graph LR
    v1((v₁<br/>2)) --- v2((v₂<br/>3)) --- v3((v₃<br/>2))

El algoritmo goloso selecciona v2, elimina a sus vecinos y obtiene: 

S_g = {v2}  ,   w(S_G) = 3

Sabemos que: tom(v) = w(v) + ∑ no(c)

no(v) =  ∑ max(tom(c), no(c))

Enraizando el árbol en v2 obtenemos:
tom(v2) = 3
no(v2) = 2 + 2 = 4

Por lo tanto el óptimo es: S* = {v1 , v2} , w(S*) = 4

El goloso obtiene 3 mientras que la programación dinámica obtiene 4

## Inciso B

Consideremos una familia de árboles estrella T_n formada por un vértice central c y n hojas

asignamos => w(c) = 3/2  w(vi) = 1

Para n >= 2, el algoritmo goloso selecciona el centro porque tiene mayor peso individual que cualquier hoja. Por lo tanto w(S_G) = 3/2

sin embargo el conjunto independiente formado por todas las hojas es óptimo S* = {v1,v2,..,vn}  w(S*) = n

Ejemplo
-------

graph TD
    c((c: 1.5))
    v1((v₁: 1))
    v2((v₂: 1))
    v3((v₃: 1))
    v4((v₄: 1))
    v5((v₅: 1))
    c --- v1
    c --- v2
    c --- v3
    c --- v4
    c --- v5

la razón entre el goloso y el óptimo es: w(S_G) / w(S*) = 3 / 2*n

Cuando n crece, esta razón tiende a cero, por ende el algoritmo goloso puede obtener una fracción arbitrariamente pequela del óptimo

## Incis0 C

Consideremos una estrella con un centro de peso 2 y tres hojas, cada una de peso 1.5

graph TD
    c((c: 2))
    v1((v₁: 1.5))
    v2((v₂: 1.5))
    v3((v₃: 1.5))
    c --- v1
    c --- v2
    c --- v3


El goloso selecciona el centro ya que su peso individual es mayor que el de cada hoja: w(S_G) =  2. Pero el conjunto independeinte formado por las tres hojas tiene peso: w(S*) = 1.5 * 3 = 4.5

Por lo tanto => las estrella sí atrapa al algoritmo goloso

La respuesta es distinta a la del error planteado en el capítulo porque aquel error consiste en obligar a seleccionar todos los hijos cuando no se selecciona al padre. En una estrella cuando se excluye el centro, los hijos son hojas y seleccionarlos a todos es precisamente lo óptimo. Por eso el error de la recurrencia no se detecta en las estrellas, mientras que el goloso sí falla al comparar únicamente pesos individuales, sin considerar el peso total de los vecinos
