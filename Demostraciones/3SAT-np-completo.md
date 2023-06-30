
Primero probamos que $(\le 3)$ SAT se reduce a 3-SAT, luego mostramos que SAT se reduce a $(\le 3)$ SAT y por lo tanto transitividad, que 3-SAT es np-completo.

Primero reducimos $\le 3$ SAT a 3-SAT. Para esto por cada disyunción D en una instancia de <= 3 sat, debemos conseguir una disyunción o serie de disyunciones que se satisfacen en el mismo universo o asignación de variables. Para el caso de que D tenga 3 literales, esto es trivial. Basta ver que hacer con los casos de 1 y 2 literales.

### Si $D$ tiene 2 literales
Entonces damos una expresión 
$$E = (D \lor x_D) \land (D \lor \overline{x_D})$$
donde $x_D$ es es un literal nuevo no presente en $B$. 

Veamos que si E es satisfacible, entonces D también lo es.

$$E = (D \lor x_D) \land (D \lor \overline{x_D})$$
$$\stackrel{Distributividad}= D \lor (x_D \land \overline{x_D})$$
$$\stackrel{No contardiccion}= D \lor (False)$$
$$\stackrel{Neutro de la disyuncion}= D$$


### Si $D$ tiene 1 literal

Entonces construimos
$$E = (D \lor x_D \lor y_D) \land (D \lor x_D \lor \overline{y_D}) \land (D \lor \overline{x_D} \lor y_D) \land (D \lor \overline{x_D} \lor \overline{y_D})$$
Veamos que es equivalente a D:


$$E = (D \lor x_D \lor y_D) \land (D \lor x_D \lor \overline{y_D}) \land (D \lor \overline{x_D} \lor y_D) \land (D \lor \overline{x_D} \lor \overline{y_D})$$
$$\stackrel{Distributividad}= D \lor ((x_D \lor y_D) \land (x_D \lor \overline{y_D}) \land (\overline{x_D} \lor y_D) \land (\overline{x_D} \lor \overline{y_D}))$$
$$\stackrel{Asociatividad y Distributividad}= D \lor ((x_D \lor (y_D \land \overline{y_D})) \land (\overline{x_D} \lor (y_D \land \overline{y_D}))$$
$$\stackrel{No contradiccion + neutro de la disyuncion}= D \lor ((x_D ) \land (\overline{x_D})$$
$$\stackrel{Idem}= D$$
Listo, sabemos entonces que si tenemos una expresión B en forma (<= 3)CNF entonces podemos dar una expresión equivalente B' en forma 3CNF.

Sea n la cantidad de $D_i$s en B, tenemos que el algoritmo para pasar de B a B' es $O(n)$

Queda probado que $(\le3)-SAT \le_p 3-SAT$

Ahora basta probar que 

$$SAT \le_p (\le3)-SAT  $$
Hacemos un procedimiento similar, usando variables nuevas para construir expresiones E por cada expresión D en B, para así construir $B' = E_1 \land E_2 \land .. \land E_m$
Si en D estan las variables $l_1, l_2, ..,l_k$, agregaremos las variables $y_1, y_2, ..,y_{k-3}$

si $k\le3$ tomamos simplemente
$$E = D$$
pero si $k \ge 4$ tomamos

$$E = (l_1 \lor l_2 \lor y_1) \land (l_3)$$
