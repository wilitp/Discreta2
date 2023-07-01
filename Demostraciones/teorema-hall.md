Sea $G = (X \cup Y, E)$ un grafo bipartito, 

$$|S| \le \Gamma(S), \forall S \subset X => \exists \text{ matching completo}$$

## Estructura de prueba
Vemos la contrarecíproca y usamos lo que sabemos de Edmonds-Karp. 

- Separamos el corte minimal entre los de un lado y el otro
- Vemos que E-K agrega primero a algunos de la izquierda(S0) y esos agregan a sus vecinos a la derecha(T1).
- Luego vemos que esos vecinos de la derecha agregarán exáctamente la misma cantidad de vértices a la izquierda(S1). Esto se da generalmente.
- entonces hacemos las cuentas y vemos que $|S| = |S_0| + |S - S_0| = |S_0| + |T| = |S_0| + |\Gamma(s)| > |\Gamma(s)|$

## Prueba

Asumiendo que no hay matching completo, y sea C el corte minimal que obtenemos al correr Edmonds-Karp, definimos:

$$S = C \cap X$$
$$T = C \cap Y$$
Si pensamos en la útlima cola E-K que construye el algoritmo, tenemos $S_0$, los vértices en S agregados por $s$, luego $T_1$, los vértices agregados por los vértices en $S_0$ y en general $S_i$ agregado por $T_{i}$ que a su vez es agregado por $S_{i-1}$. 

**Observación 1: todos los $T_i$ agregan tantos vértices a la cola como vértices tenga, por lo tanto $|T_i| = |S_i|, i>1$**

**Observación 2: S es la unión de los S_i T es la unión de los T_i y estos son disjuntos entre si.**

Entonces tenemos:
$$|S| = |S_0 \cup S_1, \cup ..\cup S_k|$$
$$= |S_0| + (|S_1| + ... + |S_k|)$$
$$= |S_0| + (|T_1| + ... + |T_k|)$$
$$= |S_0| + (|T_1 \cup ... \cup T_k|)$$
$$= |S_0| + (|T|)$$
$$= |S_0| + (|\Gamma(S)|)$$
$$> |\Gamma(S)|$$
Queda probado por contrarrecíproca