Para esto vamos a probar que $3Color <=_p 3SAT$.

Para una instancia $B$ con variables $x_1 \dots x_n$ $B = D_1 \land \dots \land D_m$, y con cada disjunción $D_j = l_{1,j} \lor l_{2,j} l_{3,j}$, construimos un grafo G tal que $\exists \vec x : B(\vec x) = 1 \iff \chi(x) = 3$

### Vértices

- $v_l \ y \ \overline{v_l}$, por cada literal $l$ (osea la afirmación y la negación de la variable)
- $\{e_{k,j}\}_{\stackrel{k=1,2,3}{j=1,\dots,m}}$ y $\{a_{k,j}\}_{\stackrel{k=1,2,3}{j=1,\dots,m}}$ por cada disjunción ( a esto le decimos garra)
- Dos vértices especiales s y t


### Lados

Vamos a tener dos estructuras disjuntas más algunos lados extras que las unen.

Primero muestro las estructuras, luego los lados extra.

Por un lado, un abanico con "la afirmación" y "negación" de cada variable, centrado en t:
![[3color-np-completo 2023-07-01 16.40.43.excalidraw]]
Por otro lado, unas "garras", que consisten en los $a$s y $e$s que dijimos arriba. Para una disjunción dada, tenemos:

![[3color-np-completo 2023-07-01 16.47.13.excalidraw]]
Con estas garras simbolizamos cada disjunción, no hay conexión entre garras, solo entre los dedos de las garras y $s$

Ahora vamos con los "lados extra". Con estos lados representaremos cuál es el literal l1, l2 y l3 en cada garra, uniendo $e_{k,j}v_k$, si $l_{k,j} = x_k$ o $e_{k,j}\overline{v_k}$, si $l_{k,j} = \overline{x_k}$. Aparte habrá un lado entre s y t

![[3color-np-completo 2023-07-01 17.04.28.excalidraw]]

### Nomenclatura de asignaciones
- $\overrightarrow b$ es una asignación de las variables en $B$.
- B($\overrightarrow b$) es el valor de la expresión entera con esa asignación
- D($\overrightarrow b$) es el valor de la disjunción $D$ con esa asignación
- x($\overrightarrow b$) es el valor de la variable $x$ con esa asignación
- l($\overrightarrow b$) es el valor del literal $l$ con esa asignación

### Prueba $B SAT \Longrightarrow \chi(G) = 3$

#### Abanicos
Primero definamos el coloreo para los $v_l$.
$$c(v_l) = l(\overrightarrow b)$$

Veamos ahora que no causa ningún problema, viendo todos los lados posibles que los involucran:

$v_xv_{\overline x}$ no crea problema, ya que $c(v_x) = v_x \ne 1 - v_x =  c(v_{\overline x})$

Coloreamos $c(t) = 2$ y $c(s) = 1$, claramente $st$ no crea problemas. Y también tenemos que $c(t) \ne c(v_l)$ y por lo tanto $tv_l$ no crea problemas.

Listo coloreado correctamente la parte de los abanicos, s y t. Ahora resta colorear las garras.

#### Garras(Acá se usa la hipótesis!)
Tenemos que $B(\overrightarrow b) =1 \implies D_j(\overrightarrow b) =1 \implies \exists k_j : l_{k_j,j} = 1$. En criollo, que en todas las disyunciones hay un $l = 1$. Si hubiera más de uno, lo ignoramos y nos quedamos sólo con ese.

Coloreamos entonces $c(a_{k_j,j}) = 2$ y a los otros dos "as", de la forma $c(a_{r,j}) = 1$ y $c(a_{z,j}) = 0$. Esto significa que el triangulo no causa problemas.

Quedan los $e$, los coloreamos:

$c(e_{r,j}) = c(e_{z,j}) = 2$
$c(e_{k_j,j}) = 0$

Viendo los lados $ea$, vemos que no se crean problemas. Listo, las garras no tienen problemas internos.

#### Lados extra: ¿causan problemas?
Ahora veamos los lados extra.

Los lados extra son de la forma $ev_l$ y $es$. Como $c(s) = 1 \ne 0,2$, los lados $es$ no causan problemas. Veamos los $ev_l$; tenemos:

$$c(v_{l_z}) = c(v_{l_r}) = 2 \ne 0,1$$
Por lo tanto no hay problemas en esos lados. Ahora, tenemos el caso de $e_kv_{l_k}$
$$c(v_{l_k}) = l_k(\overrightarrow b) = 1 \ne 0 = c(e_k)$$

Listorti la ida.

### Prueba $B SAT \Longleftarrow \chi(G) = 3$

Sea $c : V -> \{0,1,2\}$, definimos $b_i = 1 \iff c(v_{x_i}) = c(s)$

Sea $l : c(v_l) = c(s)$ 
Tenemos que si $l = x_i$, entonces $c(v_{x_i}) = c(s)$ y por lo tanto $l(\vec b) = x_i(\vec b) = 1$
Ahora, si tenemos que si $l = \overline{x_i}$, entonces $c(x_i) \ne c(v_{\overline{x_i}}) = c(s)$ y por lo tanto $l(\vec b) = 1 - x_i(\vec b) = 1 - 0 = 1$

En cualquier caso, probamos que si dentro de un $D_1$, existe $l : c(v_l) = c(s)$ entonces $D_i(\vec b) = 1$ y si además esto es verdad para todo de $D_j$ entonces $B(\vec b) = 1$.

Veamos que para todo $D_j$, tenemos algún  $l_{k, j} : l_{k, j}(\overrightarrow b) = 1$

Es claro que en el triángulo de $a$'s en cada garra están presented los tres colores, pues es un triángulo. En particular, digamos que $c(a_{q,j}) = c(t)$, que sabemos es distinto de $c(s)$ dado que existe el lado $st$. Tenemos entonces que $c(e_{q,j}) \ne c(s), c(t)$ y por lo tanto debe tener un tercer color.

Ahora, veamos que valor puede llegar a tomar $c(v_{l_{q,j}})$, tenemos:

$$c(v_{l_{q,j}}) \ne c(t)$$
$$c(v_{l_{q,j}}) \ne c(e_{q,j})$$

Sabiendo que últimos que mencionamos son colores distintos entre si, y que son los dos distintos a $c(s)$, concluimos que $c(v_{l_{q, j}}) = c(s)$. Esto vimos que ocurre en todas las garras, y por lo tanto tenemos que 
$$\forall j=1\dots m, \exists k:l_{q, j}(\vec b) =1$$
Ya vimos que esto implica que $B(\vec b) = 1$. Fin de la prueba.


