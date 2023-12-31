Dados dos networks auxiliares sucesivos, $NA$ y $NA'$, ya tenemos por la prueba de Edmonds-Karp que $d_f(s, x) \le d_{f'}(s, x)$. Ahora queremos probar que ahí vale siempre un $\lt$.

## Estructura
- Asumir que en ambos networks llegamos a t, sino es trivial que la distancia aumenta.
- Hay un camino en NA' que no está en NA, y hay dos formas de que eso pase
- Vemos para cada forma que la distancia aumenta
- Forma 1: falta un vértice
	El vértice que falta en NA tiene que tener una distancia f mayor o igual a t.
	En NA', tiene una distancia estrictamente menor a t.
	Por lo tanto crece la distancia hasta t.
- Forma 1: falta un lado
	Vemos que si falta el lado xi -> xi+1, es porque d(xi+1) <= d(xi). Luego tenemos d(xi+1) <= d(xi) <= d'(xi) = i < i+1 = d'(xi+1). Como la distancia hasta xi+1 crece estrictamente luego de actualizar el flujo, pero sigue siendo parte de un camino de menor longitud hasta t, entonces la distancia a t crece.


## Prueba
Si $t \notin NA'$ terminamos.

Asumamos entonces que $t \in NA'$:
- Hay un camino dirigido $x0, x1,...,x_{r-1}x_r$
- Este camino no pertenece a $NA$, pues sino hubiera sido saturado y no podría estar en $NA'$

Como el camino no está en $NA$, puede ser por dos razones:
- Algún vértice del camino no está
- Algún lado no está.

### Caso 1: falta un vértice

Si un vértice $x_i$ no está, entonces sabemos que $x_i \ne t$ 
- La única forma de que $x_i$ no esté en NA es que $d_f(t) \le d_f(xi)$
- Al ser $NA'$ un layered network, tenemos que $d_{f'}(xi) = i$
- Como $x_i \ne x_r = t$, tenemos que $d_f(t) \le d_f(xi) \le d_{f'}(xi) = i < r$
Por lo tanto hemos probado que en este caso que la longitud aumenta.

### Caso 2: falta un lado

Digamos que el primer lado que falta es $\overrightarrow{x_ix_{i+1}}$.

Como es el primer lado que falta, entonces el camino $x0, x1, \dots, x_i$ si está en NA y por lo tanto $d_f(x_i) = i$.

Dado que por E-K sabemos que $d_f(x_{i+1}) \le d_{f'}(x_{i+1})$, asumamos el caso $d_f(x_{i+1}) = d_{f'}(x_{i+1})$.

Si este fuera el caso, tenemos que $x_i$ y $x_{i+1}$ están en niveles consecutivos, pero no existe el lado $\overrightarrow{x_ix_{i+1}}$. Deducimos entonces que el lado $\overrightarrow{x_ix_{i+1}}$ representa un lado saturado forward del N original o un lado vacío backward. Sabemos entonces que la única forma de que este lado esté presente en NA', es que durante la construcción de $f'$, usemos un lado $\overrightarrow{x_{i+1}x_i}$, pero tampoco puede existir en NA, porque no sería legal dados los niveles. Por lo tanto queda descartado $d_f(x_{i+1}) = d_{f'}(x_{i+1})$.

Nos queda entonces que $d_f(x_{i+1}) \lt d_f'(x_{i+1})$

Entonces es claro que la distancia aumenta, pues 
$$d_f(t) = d_f(x_{i+1}) + b_{f}(x_{i+1})$$
$$ \le d_f(x_{i+1}) + b_{f'}(x_{i+1})$$
$$ \lt d_{f'}(x_{i+1}) + b_{f'}(x_{i+1})$$
$$= d_{f'}(t)$$




