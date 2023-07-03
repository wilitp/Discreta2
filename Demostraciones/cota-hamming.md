Sea C un código de longitud $n$ que corrige $t$ errores,

$$|C| \le \frac{2^n}{\sum^{t}_{k=0} {n \choose k}}$$
## Estructura

- Primero planteamos la idea de "bola alrededor de una palabra del código".
- Después vemos que si $A = \bigcup_{i=1}^{|C|} B$ , entonces $|C| = \frac A {|B|}$ 
- Calculamos $|B|$
- Vemos que $A \le 2^n$
- Concluimos la cota

## Prueba
Sea $B_i$ el la bola $\{w : w \in \{0, 1\}^n \land d(v_i, w) \le t\}$ donde $v_i$ es la i-ésima palabra del código.

También podemos verlo como la bola de radio $t$ alrededor de una palabra del código.

Y sea $A = \bigcup_{i=1}^{|C|} B_i$

Tenemos que las bolas son disjuntas, pues de no serlo entonces el código no corregiría $t$ errores. Además tenemos, como C corrige t errores, que en cada bola hay una única palabra del código.

Además tenemos que las bolas tienen todas el mismo tamaño(radio $t$).

en conclusión
$$|A| = |\bigcup_{i=1}^{|C|} B_i| \stackrel{\text{bolas son disjuntas}}= \sum_{i=1}^{|C|} |B_i| \stackrel{\text{bolas de igual cardinal}}= |C||B|$$

Osea que tenemos
$$|A| = |C||B|$$
$$|C| = \frac{|A|}{|B|}$$
Si pensamos en $|B|$ vemos que lo podemos ver en capas de 0 a t de palabras. En la capa k-ésima, las palabras varían en $k$ dígitos del centro(la palabra que si pertenece al código). Por lo tanto tenemos que

$$|B| = \sum^{t}_{k=0}{n \choose k}$$
Como sabemos que $A \subseteq \{0, 1\}^n$, tenemos que $|A| \le |\{0, 1\}^n| = 2^n$

concluimos entonces

$$|C| = \frac{|A|}{\sum^{t}_{k=0} {n \choose k}} \le \frac{2^n}{\sum^{t}_{k=0} {n \choose k}}$$
