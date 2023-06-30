Sea C un código cíclico de dimensión $k$ y longitud $n$ y sea $g(x)$ su polinomio generador. Probar que:
i) C esta formado por los multiplos de g(x) de grado menor que n:
$$C = {p(x) : gr(p) < n \land g(x)|p(x)}$$

ii) $C = \{v(x) \odot g(x) : \text{v es un polinomio cualquiera}\}$

iii) $gr(g(x)) = n − k$
iv) $g(x) | 1 + x^n$

## Estructura

Probar primero que el conjunto dado en ii) esta en C, luego que C esta en el conjunto dado en i) y luego que este último está en el de ii). Ayuda memoria en cada caso:



## Prueba

### i) y ii)
sean 
$C1 = {p(x) : gr(p) < n \land g(x)|p(x)}$
$C2 = \{v(x) \odot g(x) : \text{v es un polinomio cualquiera}\}$

Tenemos la propiedad:
$$w \in C => w \odot v \in C$$
por lo tanto, tenemos que $C2 \subseteq C$

Veamos $C \subseteq C1$

Sea $p(x) \in C$, tenemos que $gr(p(x)) < n$.

Aplicando el algoritmo de división de polinomios, tenemos:

$p(x) = q(x)g(x) + r(x), gr(r) < gr(q) < n$
por lo tanto 
$r(x) = p(x) + q(x)g(x)$

Como gr(p) < n , $p(x) = p(x) mod (1 + x^n)$
Como gr(r) < n, $r(x) = r(x) mod (1 + x^n)$

Entonces
$r(x) = r(x) mod (1 + x^n)$
$r(x) = p(x) + q(x)g(x) mod (1 + x^n)$
$r(x) = p(x) mod (1 + x^n) + q(x)g(x) mod (1 + x^n)$
$r(x) = p(x) mod (1 + x^n) + q(x) \odot g(x)$
$r(x) = p(x)+ q(x) \odot g(x)$

como ambos términos son parte del código, el resto es parte del código.

Pero si es parte del código y tenemos que $gr(r) < gr(g)$ entonces $gr(r) = 0$, pues g es el polinomio no nulo de menor grado en C. 

Concluimos entonces que $C \subseteq C1$

Ahora resta ver que $C1 \subseteq C2$

Digamos que $p(x) \in C1$, entonces $p(x) = p(x) mod(1+x^n) = q(x)g(x) mod(1+x^n) = q(x) \odot g(x)$
Por lo tanto $C1 \subseteq C2$

### iii)

Sea p cualquier palabra del codigo, tenemos por i) que $gr(p) = gr(q) + gr(g), \text{para algún polinomio q}$ y también $gr(q) + gr(g) < n$

la cantidad de posibles p van a ser entonces la cantidad de q que cumplan $gr(q) < n - gr(g)$

Esta cantidad es $2^{n-gr(g)}$. Y como C es lineal, entonces la dimensión es $n-gr(g)$ y por lo tanto:

$$gr(g(x)) = n − k$$
### iv)

Aplicamos el algoritmo de división y despejamos el resto r(x): 

$$1+x^n = q(x)g(x) + r(x)$$
$$r(x) = q(x)g(x) + (1+x^n)$$

Si tomamos mod (1+x^n) tenemos
$$r(x) mod(1+x^n) = q(x)g(x) mod(1+x^n)$$
$$r(x) = q(x) \odot g(x)$$

por lo tanto tenemos que r está en el código y que $gr(r) < gr(g)$, y por lo tanto r es 0.

### Idea de la propiedad del principio

**No hace falta probar esto en esa demostración**, pero una intucición es que si rotamos una palabra en un código cíclico entonces la palabra rotada también es parte del código. Multiplicar modularmente por una palabra no es más que por cada término no nulo de la palabra por la que multiplicamos, rotar cierta cantidad de veces y luego sumar; al ser nuestro código lineal, la suma también está en el código.



