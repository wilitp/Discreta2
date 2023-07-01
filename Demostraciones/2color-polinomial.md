Dado un grafo G, tomamos un vertice x cualquiera y lo coloreamos con 0. Luego, hacemos BFS y coloreamos cada vértice con 0 ssi su distancia a x par, 1 caso contrario. Luego vemos si este coloreo es propio. Esto hay que hacerlo con un x, y si al terminar BFS, faltan vértices por colorear, entonces hacemos lo mismo con otro x' que falte, hasta terminar.

Si al terminar, el coloreo es propio entonces G es bipartito, sino no.

BFS es O(m) -> el algoritmo es polinomial

Este algoritmo es correcto, ahora lo probamos:

si al terminar de colorear, encontramos que hay 2 vértices vecinos $v$ y $z$ que tienen el mismo color, tendremos que el ciclo w ... v ... z ... w(donde w es el último ancestro común de v y w en el árbol BFS) tiene distancia:

$$d(w, v) + d(v, z) + d(z, w)$$
$$d(w, v) + 1 + d(z, w)$$

**Observación:$d(w,v) \equiv d(w,z) (mod2)$**: 
prueba:
$$d(x,v) \equiv d(x,z) mod \ 2$$
$$d(x,w) + d(w,v) \equiv d(x,w) + d(w,z) mod \ 2$$
$$d(w,v) \equiv d(w,z) mod \ 2$$
si tomamos módulo 2 a la suma de antes:
$$d(w, v) + 1 + d(z, w) mod 2$$
$$(d(w, v) mod 2) + 1 + (d(z, w) mod 2) mod 2$$
$$(d(w, v) mod 2) + 1 + (d(w, v) mod 2) mod 2$$
$$2(d(w, v) mod 2) + 1mod 2$$
$$1mod 2$$
Es decir, tenemos un ciclo impar.

Resumiendo: si el coloreo es propio entonces G es bipartito, si el coloreo no es propio, entonces tenemos un ciclo impar como certificado de que no es bipartito.