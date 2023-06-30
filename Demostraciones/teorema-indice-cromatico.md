Sea G un grafo bipartito, $\chi'(G)=\Delta$

## Estructura
- Primero probamos, usando el teorema del matrimonio y por inducción, que se puede colorear con Delta colores un grafo bipartito regular.
- Luego mostramos que cualquier grafo bipartito G con cierto Delta puede incluirse dentro de un grafo bipartito H regular con el mismo Delta.
- Esto lo hacemos dando la siguiente construcción de un grafo $G'$, que tiene $\delta(G') = \delta(G)$, y de esa forma mostramos que podemos hacer que eventualmente lleguemos a un grafo H, con $\delta(H) = \Delta(H) = \Delta(G)$ que será regular.
- Como G es subgrafo de H, se puede colorear G con Delta de G colores

![[teorema-indice-cromatico 2023-06-29 11.50.17.excalidraw]]

## Prueba

Primero probamos que un grafo bipartito regular G se puede colorear con Delta colores.

Usamos inducción sobre Delta.

Si $\Delta = 1$, entonces todos los lados no comparten vértices, pues sino para algún vértice compartido x, d(x) > 1. Entonces podemos pintar a todos con el mismo color.

Ahora para el caso inductivo, como G es un grafo bipartito regular, tenemos que existe un matching perfecto. Si tomamos los lados de un matching perfecto y los quitamos, entonces tenemos un grafo bipartito regular con Delta = Delta(G) - 1.

Tenemos por hipótesis inductiva, que este grafo reducido se puede colorear con Delta(G)-1 colores. Si ahora usamos ese coloreo para colorear G, y coloreamos los lados del matching con un nuevo color, entonces tenemos un coloreo de lados propio, pues los lados del matching no comparten vértices. Queda probado el caso inductivo.

Ahora para el caso regular, basta con probar que todo grafo bipartito G se puede incluir en un grafo bipartito G' con $\delta(G') = \delta(G) + 1$. Iterando esta construcción, podemos llegar a un grafo $H : \delta(H) = \Delta(H) = \Delta(G)$, es decir un grafo bipartito regular con igual Delta que G, con G subgrafo de este. De esta forma quedaría probado que se puede colorear G con Delta colores.

Sea G grafo tal que $G = (X \cup Y, E)$, podemos definir G' como:

$$G' = (X' \cup Y', E')$$
donde 
$$X' = X \cup Y^*, Y' = Y \cup X^*$$
$$E' = E \cup \{x'y' : xy \in E\} \cup \{xx' : x \in X \land d(x) < \Delta(G)\} \cup \{yy' : y \in Y \land d(y) < \Delta(G)\}$$
donde X* e Y* son "copias" de X e Y(notese también que x' es la copia del vértice x en X)

Este nuevo grafo G' tiene como subgrafo a G. Pero tamién tiene que para cada vértice de G cuyo grado era menor a Delta, ahora su grado es aumentado en 1. También, como no hay lados entre X' e Y', tenemos que G es bipartito.

Concluimos que existe H regular con Delta igual a Delta de G y con G subgrafo de este. Por lo tanto se puede colorear G con Delta(G) colores.