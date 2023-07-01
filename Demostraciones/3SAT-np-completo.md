
Para probar que 3-SAT es NP completo basta con reducir polinomialmente SAT a 3-SAT.

Es decir, dada una instancia de SAT $B = D_1 \land .. \land D_m$, tenemos que construir una expresión booleana $B = E_1 \land .. \land E_m$, donde los E son expresiones en forma 3-CNF. Nosotros lo haremos de forma tal que para cada $i \le k$, $D_i \equiv E_i$.

Entonces debemos, para un D dado, dar una expresión E equivalente en forma 3-CNF.

Lo hacemos por casos:
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
Si en D estan las variables $l_1, l_2, ..,l_k$, agregaremos las variables $y_1, y_2, ..,y_{k-3}$

### Si $D$ tiene 3 literales
$$E = D$$
### Si $D$ tiene $k \ge 4$ literales

$$E = (l_1 \lor l_2 \lor y_1) \land (l_3 \land \overline{y_1} \land y_2) ... (l_{k-2} \lor \overline{y_{k-4}} \lor y_{k-3}) \lor (l_{k-1} \lor l_{k} \lor \overline{y_{k-3}})$$
Veamos que son equivalentes viendo:
$$\exists \overrightarrow{l} : D(\overrightarrow{l}) = 1 \iff \exists \vec{l}, \vec y : E({\vec{l}, \vec{y}}) = 1$$
Veamos primero la vuelta, dada una asignación, tenemos:
$$1 = E = (l_1 \lor l_2 \lor y_1) \land (l_3 \lor \overline{y_1} \lor y_2) ... (l_{k-2} \lor \overline{y_{k-4}} \lor y_{k-3}) \land (l_{k-1} \lor l_{k} \lor \overline{y_{k-3}})$$
Asumamos que $D(\vec l) = 0$. Veamos que entonces
$$1 = E = (y_1) \land (\overline{y_1} \land y_2) ... (\overline{y_{k-4}} \lor y_{k-3}) \lor (\overline{y_{k-3}})$$

Entonces tengo que $y_1$, entonces en la segunda implica que $y_2$. Continuando esto, llegamos a que $y_1 = y_2 = .. = y_{k-3} = 1$, pero por el último término que $y_{k-3} = 0$. Por contradicción, tenemos que $D(\vec l) = 1$

Ahora la ida. Asumismos $\exists \overrightarrow{l} : D(\overrightarrow{l}) = 1$ y entonces tenemos que algun $l_i = 1$. Sea $l_r$ el primero que es 1. Podemos construir la asignación:

$$
y_j =
\left\{
	\begin{array}{ll}
		1  & \mbox{si } j \le r-2 \\
		0  & \mbox{si } j \ge r-1 \\
	\end{array}
\right.
$$
De esta forma, la primera disyunción es 1 si l1 o l2 son 1, o por defecto ya que entonces y1 = 1.

La última disyunción es verdadera si lk-1 o lk son 1, y sino también ya que entonces r<=k-1 y por lo tanto $\overline{y_{k-3}}=0$.

Las disyunciones intermedias son, de forma general:


$$

(l_{j+1} \lor \overline{y_{j-1}} \lor y_{j}) =
\left\{
	\begin{array}{ll}
		(l_{j+1} \lor \overline{1} \lor 1) = 1 & si \ j \le r-2, \text{ pues } y_j \text{ es 1} \\
		(1 \lor \overline{1} \lor 0) = 1  & si \ j = r-1 \text{, pues } l_{j+1} \text{ es 1}\\
		(l_{j+1} \lor \overline{0} \lor 0) = 1  & si \ j \ge r\text{, pues } \overline{y_{j-1}} \text{ es 1} \\
	\end{array}
\right.
$$
Por lo tanto por cada disyunción $D_i$ en $B$, podemos dar una expresión $E$ equivalente. Por la regla de Leibniz, tenemos que si $\tilde B = B[D_i \mid E_i]$, entonces $B \equiv \tilde B$ y $\tilde B$ es una instancia de SAT en la que si la respuesta "si" entonces también lo es en 3-SAT y vice-versa. 

La complejidad de la transformación dada es $O(m*k)$, donde $m$ la cantidad de disyuncinoes y k la máxima cantidad de literales y por disyunción:

$$SAT \le_p 3-SAT$$



