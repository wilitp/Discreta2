¿Cuál es la complejidad del algoritmo de Edmonds-Karp? Probarlo.(Nota: en la prueba se definen unas distancias, y se prueba que esas distancias no disminuyen en pasos sucesivos de EK. Ud. puede usar esto sin necesidad de probarlo)

## Enunciado
Sea n la cantidad de vértices y m la cantidad de lados, E-K tiene complejidad $O(nm^2)$

## Estructura de la prueba

Supondremos que en el network no existen arcos paralelos xy e yx. Esta propiedad no es restrictiva, ya que para cualquier network N que presente arcos paralelos, podemos dar un N' tal que sea como N PERO con vértices "intermedios" adicionales en medio de cada arco paralelo.

Primero queremos ver que los flujos parciales $f_0, f_1, f_2,...$ son finitos y daremos una cota para ellos.

Como la búsqueda y construcción de cada flujo parcial se hace con BFS, cada incremento tiene complejidad $O(m)$ (máximo vas a tener que ver todos los lados hasta llegar a $t$)

Si probamos que solo puede haber $O(nm)$ búsquedas, entonces habremos probado la complejidad.

**Estructura:**
- Damos lema y definiciones
- Acotamos la cantidad de veces que se puede volver crítico un lado ($O(n)$)
- Concluímos que como todo lado puede volverse crítico $O(n)$ veces, y siempre se vuelve crítico un lado en un nuevo paso de E-K, la cantidad de pasos es $O(nm)$
- La complejidad total es entonces $O(nm^2)$

**Las definiciones están despúés de la prueba.**

## Prueba
Vemos que se puede hacer crítico un lado (n-1)/2 veces viendo que entre dos pasos $k$ y $r$ la f-distancia entre s y t debe haber aumentado en al menos 2.

Supongamos que en el paso $k$ **se satura xy** para obtener el flujo $f_{k+1}$, por lo tanto existe un camino de longitud mínima s ... xy ... t. Entonces 
$$d_k(y) = d_k(x) + 1 (\text{i})$$
Luego para que vuelva a hacerse crítico xy en un paso $r$ tiene que haber un paso intermedio $l$ tal que $r \ge l > k$ en el que se vacíe al menos un poco. **Ya sea para que se vuelva a saturar, o bien para que luego (o en esa misma instancia, si r = l) se vacíe por completo.** Tenemos entonces un camino s ... ybackx ... t y por lo tanto
$$d_l(x) = d_l(y) + 1 \text{ (ii)}$$
Ahora hacemos cuentas para ver cuanto tiene que aumentar la distancia a $t$ entre cada evento de criticalidad sobre un lado xy:
$$d_l(t) = d_l(x) + b_l(x)$$
$$d_l(t) = d_l(y) + 1 + b_l(x) \text{ por (ii)}$$
$$d_l(t) \ge d_k(y) + 1 + b_k(x) \text{ por lema distancias}$$
$$d_l(t) \ge d_k(x) + 1 + 1 + b_k(x) \text{ por (i)}$$
$$d_l(t) \ge d_k(t) + 2$$
Ahora veamos el caso en el que se **vacía xy** para obtener el flujo $f_{k+1}$:
Mismo planteo con $r \ge l \gt k$ pero en este caso tenemos que en el paso k tenemos el camino s ... ybackx ... t y por lo tanto
$$d_k(x) = d_k(y) + 1 \text{ (iii)}$$
Luego en el paso $l$ tenemos que se debe saturar del todo o un poco el lado xy. Tenemos:

$$d_l(y) = d_l(x) + 1 \text{ (iv)}$$
Hacemos las cuentas otra vez:
$$d_l(t) = d_l(y) + b_l(y)$$
$$d_l(t) = d_l(x) + 1 + b_l(y) \text{ por (iv)}$$
$$d_l(t) \ge d_k(x) + 1 + b_k(y) \text{ por lema}$$
$$d_l(t) \ge d_k(y) + 1 + 1 + b_k(y) \text{ por (iii)}$$
$$d_l(t) \ge d_k(t) + 2$$
En ambos casos vemos que $d_r(t) \ge d_l(t) => d_r(t) \ge d_k(t) + 2$

Como la máxima distancia hasta t es n-1, tenemos que un lado puede hacerse crítico $\frac{n-1}{2}$ veces: $O(n)$. 

Por lo tanto la complejidad total es $O(flujos * BFS) = O(m * n * m) = O(nm^2)$

## Definiciones / lemas internos


### Lema de las distancias (no se pide la prueba)

las distancias $d_k(x)$ y $b_k(x)$ son <= a $d_{k+1}(x)$ y $b_{k+1}(x)$  respectivamente.


### Lado crítico
Un lado xy se vuelve crítico si:
- se satura completamente
- se vacía completamente

### Distancias
$$d_k(x) = \text{ longitud del menor } f_k\text{-camino aumentante de s a x}$$
$$b_k(x) = \text{ longitud del menor } f_k\text{-camino aumentante de x a t}$$
