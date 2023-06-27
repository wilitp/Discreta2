¿Cual es la complejidad del algoritmo de Dinic? Probarla en ambas versiones: Dinitz original y Dinic-Even. (no hace falta probar que la distancia en networks auxiliares sucesivos aumenta).

## Estructura
- Enunciamos que la longitud de los sucesivos networks auxiliares crece.
- Primero mostramos los aspectos generales de la complejidad de algoritmos "tipo Dinic"
- Luego vemos cuánto cuesta conseguir un flujo bloqueante en cada implementación

## Prueba
Como sabemos que los networks auxiliares crecen en longitud, tenemos que a lo sumo abrán $n$ networks auxiliares.

Luego, también sabemos que la complejidad de construir un network auxiliar es la de BFS: O(m) por lo tanto tenemos que la complejidad de un algoritmo tipo dinic es 
$$n * (O(m) + CFB) = O(n * (m+CFB))$$

### Dinitz
Para ver la complejidad de la versión de dinitz es necesario entonces ver el costo CFB.

CFB en dinitz va a consistir del costo de:
- hacer una búsqueda DFS
- podar antes de cada búsqueda

La búsqueda tiene la propiedad de que nunca vamos a hacer backtracking, ya que hemos podado deadends anteriormente. Por lo tanto el costo de buscar un camino en dinitz es O(n)

Ahora debemos ver cuántos caminos pueden haber y cuánto cuesta podar. 

A lo sumo pueden haber $m$ caminos.

Para analizar el costo de podar, debemos analizar no una sola poda sino todas las podas de un CFB en conjunto. De esta forma, podemos ver las podas como dos operaciones separadas: 
- revisar los vértices de niveles más altos a más bajos para ver si borrarlos(PV)
- Borrar los vértices que no tengan lado(s) de salida(B).

La compjejidad de cada PV es O(n), pues mira los vértices nada más.

La complejidad de un único B(x) es O(m) pues tiene que borrar a todos los vecinos del vértice x. Pero si lo vemos en conjunto, el costo de todos los B es $\sum_{i=1}^n \Gamma(x_i) = 2m$

Por lo tanto la complejidad de CFB nos queda:

$$buscarcaminos + \text{revisar por cadacamino} + \text{borrar vertices revisados}$$
$$O(nm) + O(nm) + O(2m) = O(nm)$$
Por lo tanto la complejidad total de Dinitz es

$$n * (O(m) + CFB) = O(n * (m+CFB)) = O(mn^2)$$
### Even

