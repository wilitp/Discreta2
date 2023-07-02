Probar que el valor de todo flujo es menor o igual que la capacidad de todo corte y que si f es un flujo, entonces las siguientes afirmaciones son equivalentes:
i) Existe un corte S tal que $v(f) = cap(S) = c(S, \overline{S}) )$ . (y en este caso, S es minimal)
ii) f es maximal.
iii) No existen f-caminos aumentantes.
(puede usar sin necesidad de probarlo que si f es flujo y S es corte entonces $v(f) = f(S, \overline{S}) − f(\overline{S}, S) )$


## Estructura
Primero probamos $v(f) \le cap(S), \forall f, S : \text{f flujo y S corte}$ usando $v(f) = f(S, \overline{S}) − f(\overline{S}, S) )$ (es cortito)

Después probamos la equivalencia de esta forma:
$1 => 2 => 3 => 1$
Y queda probada la ida y la vuelta entre todos.

- 1=>2: $v(f) = cap(S) \le v(g) \forall g \text{ flujo}$
- 2=>3: contrarrecíproca - existiría un flujo de valor más grande si existiera un f-camino aumentante
- 3=1: Construimos S y vemos que los limítrofes están saturados y que en $\bar{S}$ los limítrofes no envían nada hacia atrás. Por lo tanto $f(S, \bar{S}) - f(\bar{S}, S) = c(S, \bar{S}) - 0 = cap(S)$

## Prueba
### 1 => 2

Fácil, $v(f) = cap(S) \ge v(g) \forall g \text{ flujo}$

### 2 => 3

Por contrarrecíproca. Si existe un camino p f-aumentante, entonces habría un flujo g tal que

$$g(\overrightarrow{xy}) =
\left\{
	\begin{array}{ll}
		f(\overrightarrow{xy})  & \mbox{si } \overrightarrow{xy} \in p \\
		f(\overrightarrow{xy}) + \mathcal E & \mbox{caso contrario } 
	\end{array}
\right.$$
En particular habrían lados $\overrightarrow{sx}$  y $\overrightarrow{yt}$ en $p$ y por lo tanto $v(g) = v(f) + \mathcal{E}$. Entonces no sería maximal f. 

### 3 => 1
Si no hay caminos f-aumentantes, probaremos que existe un corte S tal que cap(S) = v(f).

Construimos S de la siguiente manera:

$$S = \{s\} \cup  \text {\{x : existe camino f-aumentante de s a x\}}$$
- Como vale 3, $t \notin S$. S es corte.
- tenemos que v(f) = $f(S, \bar{S}) - f(\bar{S}, S)$
Para los x "limítrofes" en S, todas sus salidas están saturadas, sino tendríamos caminos a un nivel más allá y no serían limítrofes.
Los y en $\bar{S}$ no envian nada hacia ningún x en $S$, de lo contrario, como vimos antes, habría un camino f-aumentante hacia $y$ y por lo tanto $y \in S$, lo que sería absurdo.

Por lo tanto $v(f) = c(S, \bar{s}) - 0 = cap(S)$

**Para mayor formalidad podemos usar las sumatorias que definen a f(S) y demás; pero lo que decimos de x e y es lo mismo: x tiene todas las salidas saturadas e y no le manda nada a ningún x**
