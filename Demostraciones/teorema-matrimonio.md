## Estructura
- Planteamos un subconjunto cualquiera $W\subseteq X$
- Planteamos el conjunto de lados $E_W = \{zw : w \in W\}$
- Vemos que para este conjunto, $|E_W| = \sum\{d(w) : w \in W\} = \Delta *|W|$
- Vemos que todo esto se cumple tambien para $W \subseteq Y$
- Vemos que si $W = X, E_X = E$ y $|E| = \Delta * |X| = \Delta * |Y|$ y por lo tanto $|X| = |Y|$ 
- Ahora basta probar que existe un matching completo, y será también perfecto.
- Vemos que si tomamos $S \subseteq X$, entonces cada lado $l \in E_S$ tambien cumple $l \in E_\Gamma(S)$
- Por lo tanto $E_S \subseteq E_\Gamma(S) => |E_S| \leq |E_\Gamma(S)|$
- Por lo tanto $\Delta *|E_S| \leq \Delta *|\Gamma(S)| => |E_S| \leq |\Gamma(S)|$
- Se cumple la condición de Hall y por lo tanto hay matching perfecto.
## Prueba

Sea $W \subseteq X$, y $E_W = {zw : w \in W}$, tenemos que $|E_W| = \sum_{w \in W} d(w)$, pues como no hay lados entre vértices de W, no estamos contando lados dos veces. Como G es regular, tenemos también que $|E_W| = \Delta|W|$

Observemos que esto **también se cumple para cualquier W subconjunto de Y**, pues vale todo lo que dijimos hasta ahora.

Si consideramos que todos los lados en E son de la forma xy, con $x \in X$, vemos que $E_X = E$ y por ende vemos que $|E| = \Delta|X|$

Devuelta, lo mismo vale para Y, entonces $|E| = \Delta|Y|$ y por lo tanto $|X| = |Y|$

Tenemos entonces que si tuvieramos un matching completo de X a Y, ese matching sería también perfecto. Basta ver que se cumple la condición de Hall.

Consideremos $S \subseteq X$, tenemos que para todo lado $l \in E_S$, este lado es de la forma xy, donde $x \in S, y \in \Gamma(S)$, y por lo tanto $l \in E_{\Gamma(S)}$. Entonces vemos que $E_S \subseteq E_{\Gamma(S)}$

Entonces tenemos:
$$|E_S| \leq |E_\Gamma(S)|$$
$$\Delta|S| \leq \Delta|\Gamma(S)|$$
$$|S| \leq |\Gamma(S)|$$

Concluimos que existe matching perfecto.