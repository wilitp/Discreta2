Probar la complejidad $O(n^4)$ del algoritmo Hungaro y dar una idea de como se la puede reducir a $O(n^3)$.

## Prueba

### Idea global del costo

Con el método que hacemos en papel, usamos E-K sobre la matriz para ir aumentando el matching inicial. Esto lo vamos a hacer a los sumo n veces(pues hay n lados en el matching perfecto que buscamos.)

Como el matching inicial cuesta $O(n^2)$(que es lo que cuests restarle el mínimo a cada fila y luego el mínimo a cada columna y luego obtener el matching inicial de ceros.) y **luego** haremos $O(n)$ extensiones a este matching, el costo del húngaro es a priori $O(n^2) + O(n)$, si ignoramos el costo de extender el matching(incluyendo los cambios de matriz).

¿Cual es la complejidad de extender en un lado el matching? Si solo pensamos en la búsqueda de un camino aumentante de tamaño mínimo, tenemos que el costo es $O(m) = O(n^2)$(costo de BFS).

Hasta ahora, la complejidad total del húngaro sería $O(n^2) + O(n) * O(n^2) = O(n^3)$

Pero todavía tenemos que tener en cuenta que para cada vez que extendemos en 1 el matching, también es posible que tengamos que agregar un lado haciendo una serie de cambios de matriz.

Sea CM el costo de un cambio de matriz y T la máxima cantidad de cambios de matriz necesarios para agregar un lado, **el costo total del algoritmo es**:

$$O(n^2) + O(n) * (O(n^2) + CM * T)$$
**Aclaración:** Los cambios de matriz están entre medio de cada búsqueda, **no se hace una búsqueda por cada cambio de matriz, sino que se pausa y se continúa ante cada cambio de matriz**. 

### CM
CM consiste en
- Calcular la constante $m$
- Restar $m$ de S 
- Sumarlo $m$ a $\Gamma(S)$

El cálculo de $m$ consiste de calcular el mínimo de potencialmente todos los elementos de la matriz, así que su complejidad es $O(n^2)$

Restarlo de las filas es $O(n) * \text {filas etiquetadas} = O(n^2)$

Sumarlo a $\Gamma(s)$ también es $O(n^2)$

Por lo tanto la complejidad de CM es $O(n^2)$

### T
Ahora veamos de acotar T.

**Propiedad clave:** después de un cambio de matriz, o crecen las filas etiquetadas o extendemos el matching(o ambas).

Eso lo podemos ver si analizamos que pasa cuando calculamos que $m = C_{x, v}$: tendremos un nuevo 0 en la entrada $C_{x,v}$ y por lo tanto cuando revisemos las filas, x etiquetará a v. Si v está libre, extendemos el matching. Si v no está libre, entonces agrega a alguna fila z y quizá extendemos el matching. Si terminamos no pudiendo extender el matching, entonces tenemos que S crece en al menos 1(el z que agregamos).

Con esta propiedad tenemos que $T \le n$ 


### Conclusión
Entonces, reemplazando:

$$O(n^2) + O(n) * (O(n^2) + CM * T)$$
$$O(n^2) + O(n) * (O(n^2) + O(n^2) * O(n))$$
$$O(n^2) + O(n^3) + O(n^4) = O(n^4)$$




### Complejidad mejorada: n^3

Dada la cuenta de arriba, vemos que si CM costara O(n), entonces tendríamos una complejidad de n^3. Para lograr esto, podemos hacer que el cálculo de m sea O(n) y también lograr que restar a las filas S y sumar a las $\overline{\Gamma(S)}$ sea O(n).

Para lo primero, podemos tener pre-calculado el mínimo de cada fila de S, por ejemplo, esto se podría hacer cuando se está revisando una fila en la búsqueda anterior al cambio de matriz.

Por otro lado podemos en lugar de restar/sumar a todas las entradas, mantener un array con los valores que habría que sumarle/restarle a cada fila y columna. Esto nos da un costo O(n). Luego al buscar 0's, lugar de la guarda $C_{x, v} == 0$ tendríamos $C_{x, v} - ArrayFilas[x] + ArrayColumnas[v] == 0$


La complejidad queda:
$$O(n^2) + O(n) * (O(n^2) + CM * T)$$
$$O(n^2) + O(n) * (O(n^2) + O(n) * O(n))$$
$$O(n^2) + O(n^3) + O(n^3) = O(n^3)$$

