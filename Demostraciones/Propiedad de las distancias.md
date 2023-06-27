Probar que si, dados vértices x, z y flujo f definimos a la distancia entre x y z relativa a f como la longitud del menor f-camino aumentante entre x y z, si es que existe tal camino, o infinito si no existe o 0 si x = z, denotandola por df (x, z), y definimos dk(x) = dfk (s, x), donde fk es el k-ésimo flujo en una corrida de Edmonds-Karp, entonces dk(x) ≤ dk+1(x).

**Suposicion**: Asumimos para esta prueba que si existe el lado xz entonces no existe el lado zx. Esto ya que por lo que vimos en el práctico, de cualquier network podemos definir uno nuevo en el que ponemos en cada arco paralelo "un vértice intermedio" y así tener un problema sin esta propiedad que tiene la misma solución max-flow.

## Definición: fFF Vecino
decimos que z es fFF vecino de x si desde x podemos enviar flujo a z o devolver flujo a z.

## Estructura

- Asumimos que $A = \{y : d_{k+1}(y) < d_k(y)\} \ne \emptyset$
- Tomando algún $y$ en $A$
- Puntualmente tomaremos al $x$ tal que $d_{k+1}$ sea mínimo.
- Probamos que existe un $z$ anterior a $x$ desde el que antes no podías llegar a x pero ahora si.
**- Vemos que dada esa situación, $z \notin A$ y por lo tanto $d_k(x) > d_k(z) +1$ ESTA ES LA PARTE DIFICIL**
- Luego resta ver que para que esto haya ocurrido, antes tomamos un camino s ... x z ... t y por lo tanto $d_k(z) = d_k(x) + 1$
- Usando las conclusiones de los últimos dos pasos llegamos a que 0 > 2
## Prueba
Por hipótesis tenemos que $d_{k+1}(x) \lt d_k(x) \le \infty$ y por lo tanto existe camino $f_{k+1}$ aumentante de menor longitud hasta x.

**Observación**: $s$ no pertenece a $A$, pues la distancia a si mismo no puede bajar de 0. Por lo tanto, en el camino que consideramos existe un $z$ directamente anterior a x.

Tenemos entonces que $d_{k+1}(z) = d_{k+1}(x) - 1$, pues x es fFF vecino de z.
Entonces $d_{k+1}(z) < d_{k+1}(x)$ y por lo tanto $z \notin A$

**Por la definicón de $A$, $d_{k}(z) \le d_{k+1}(z)$**

Entonces tenemos:
$$d_k(x) \gt d_{k+1}(x) \text{ porque } x \in A = d_{k+1}(z) + 1 \text{ porque x es fFF vecino de z } \ge d_k(z)+1 $$
$$d_k(x) > d_k(z) + 1$$
Por lo tanto x  no es fFF vecino de z en el paso k.

Esto **solo puede pasar** si el camino que usamos para pasar de $f_k$ a $f_{k+1}$ incluye xz o xbackz.

Veamos cada caso:

- $\overrightarrow{xz}$
Tenemos que $f_k(\overrightarrow{xz}) = 0$ y   $f_{k+1}(\overrightarrow{xz}) \gt 0$ por lo que vimos de la vecindad de z a x en cada paso. Por lo tanto de k a k+1 ENVIAMOS flujo de x a z.

- $\overrightarrow{zx}$
Tenemos que $f_k(\overrightarrow{zx}) = c(\overrightarrow{xz})$ y   $f_{k+1}(\overrightarrow{xz}) \lt c(\overrightarrow{xz})$ por lo que vimos de la vecindad de z a x en cada paso. Por lo tanto de k a k+1 DEVOLVEMOS flujo de x a z.

En **ambos casos** la longitud del camino que usamos es mímina y por lo tanto 
$$d_k(z) = d_k(x) + 1$$
Pero entonces

$$d_k(z) = d_k(x) + 1 \gt (d_k(z) + 1) + 1$$
$$0 \gt 2$$
Absurdo. Lo único que asumismos hasta ahora fue que $A$ no era vacío, y por lo tanto lo es.

## Notas
Por qué $d_k(z) = d_k(x) + 1$?
- Porque si bien tendríamos sólo que $d_k(z) \le d_k(x) + 1$ si tuvieramos que z es $f_k$FF vecino de x, sabemos también en ese punto de la demostración que en el paso k ELEGIMOS un camino s ... xz ... t y por lo tanto la longitud de s ... xz es la mínima posible.
